# Getting started

## 1. Requirements

| Need | Why | Without it |
|---|---|---|
| An agent that loads `SKILL.md` skills | blueprint is a skill | Nothing runs |
| The [`council`](https://github.com/t3dotgg/tstack/tree/main/skills/council) skill | Reviews the plan with three providers | The plan stays `draft` and the hand-off says why |
| Delegation across providers | Recon delegates and the three council members | Recon runs inline; council can't run |
| Web access | Groups B and C | Say "no web": B and C are skipped |
| `find-docs` skill (optional) | Current library and API docs for group B | Delegates search the web instead |

Delegation works best in [T3 Code](https://github.com/pingdotgg/t3code), which can start delegates on any configured provider (`orchestrator_capabilities` + `delegate_task`). In other agents, blueprint uses the native subagents. Those usually run only your own model, so group work happens, but council needs three providers to reach `reviewed`.

## 2. Install

Copy the skill folder into your agent's skills folder:

```sh
git clone https://github.com/Steve524/blueprint-skill
cp -r blueprint-skill/skills/blueprint ~/.claude/skills/
```

| Agent | Folder |
|---|---|
| Claude Code | `~/.claude/skills/blueprint` |
| Codex | `~/.agents/skills/blueprint` |
| Cursor | `~/.cursor/skills/blueprint` |
| OpenCode | `~/.config/opencode/skills/blueprint` (also reads `~/.claude/skills`) |
| Antigravity | `~/.gemini/antigravity/skills/blueprint` |

Install `council` the same way from [tstack](https://github.com/t3dotgg/tstack/tree/main/skills/council).

Restart the agent so it picks up the new skill.

## 3. First run

In a project folder:

```
blueprint: <what you want built>
```

What to expect, in order:

1. Up to one message asking for the goal, done-when, or out-of-scope, if your request didn't say.
2. A note on which recon groups run and which are skipped.
3. An assumptions ledger. If deep research could help, a question packet comes first: approve, edit, or skip it in the same reply.
4. Up to 5 decision questions in one message, each with a recommendation. Reply by number (`1 yes, 2 B, 4 no: use X`); a skipped number takes the recommendation. Or say "accept all recommendations".
5. A wrap-up with the defaults it didn't ask about and a 5-line summary. Say "ok" or correct it.
6. The phase table. Say "ok" or "regroup".
7. Council rounds run on their own.
8. The hand-off: the plan path, the phases, rounds, the models that ran, and "Start with P1". Nothing is built.

## 4. Build from the plan

Start a new request, with any agent:

```
Build phase P1 of docs/plans/2026-11-01-offline-sync.md
```

Each phase is written so a builder with no chat history can run it from the plan file and the repo.

## Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| The plan stays `Status: draft` | Council couldn't reach three providers, or a delegate failed twice | Read the hand-off. It names what's missing |
| `Status: ready` | A dispute after two replies, or out of rounds | The coordinator settled it. The hand-off lists each call; correct any you disagree with |
| A delegate count warning | More than 3 delegates at once | Cut questions, or lower `instances` in `roster.yaml` |
| The skill doesn't trigger | Its trigger is the word "blueprint" | Start your message with `blueprint` |
