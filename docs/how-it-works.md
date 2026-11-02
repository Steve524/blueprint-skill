# How it works

The full rules are in [`SKILL.md`](../skills/blueprint/SKILL.md) and [`deep-research.md`](../skills/blueprint/deep-research.md). This page explains them for people.

## The contract

- blueprint writes only the plan file, plus a research brief when deep research runs.
- Every delegate is read-only, and none starts more delegates.
- It stops after the hand-off, even if you said "and build it".
- It never swaps in a different model. A missing member is reported, not replaced.

## 1. Intake

blueprint needs three lines: the **goal**, **done when**, and **out of scope**. It takes them from your request, and asks once for whatever's missing.

Then it picks a level:

| Level | When | Output |
|---|---|---|
| Plan | Every phase can get files, steps, and an exact check today | `docs/plans/<date>-<slug>.md` |
| Initiative | A later part depends on what earlier work teaches you | `docs/plans/<date>-<slug>-initiative.md`, a map of epics, with E1 planned in full |
| Neither | It fits one obvious commit | A short inline plan instead |

## 2. Recon

Delegates get no chat history, so every brief carries the goal, the absolute paths, and the decisions made so far.

| Group | Asks | Runs when |
|---|---|---|
| A, codebase | What exists, what to reuse, what checks cover it | The plan must fit existing code |
| B, stack and docs | What does this library or API do, at which version? | There are stack questions and web is allowed |
| C, deep research | Which approach fits, and why? | An approach decision is open that research could change, and you approve |

Group C, step by step:

1. **Packet.** A topic, 3-5 questions (each names the decision it could change), what's excluded, and the delegate count per step. You approve, edit, or skip.
2. **Find.** One question per finder. Sources are ranked, primary first.
3. **Curate.** The coordinator keeps 6 sources at most and numbers them.
4. **Deep-read.** Readers return claims with verbatim excerpts.
5. **Synthesize.** One delegate writes the brief from reader notes only, and tries to refute each claim a decision rests on.
6. **Check and save.** The coordinator opens the sources behind key claims, then saves the brief.

The interview keeps going while C runs. Only decisions that need its answers wait.

## 3. Interview

- **Assumptions ledger:** each line has a source and a status: `confirmed`, `assumed`, `contested`, or `unverified`.
- **Decision map:** load-bearing decisions (a wrong answer costs a rewrite, a migration, a security hole, or trust) and cosmetic ones.
- **Questions:** up to 5 in one message, load-bearing first, at most 4 lines each, worded so "yes" takes the recommendation. Extra ones take the recommendation and show in the wrap-up.

Good question:

> Q2 Login: keep the existing session login, no new provider? Recommend yes, it works today. If wrong: accounts get rebuilt later.

Who decided what is tracked. `user` means you answered it. Anything accepted by silence, "ok", or "accept all" is `default`. The council can challenge defaults, but not your answers.

## 4. The plan

```markdown
# Plan: <outcome>
Revision: 1 | Status: draft | Date | Baseline: <repo @ sha>
Research: <brief path, or none>
## Goal / Done when / Out of scope
## Requirements       R1..Rn
## Decisions          choice | why | source
## Assumptions
## Phases             table, then one block per phase:
### P1: <outcome>     Covers, Files, Steps, Done when, Excludes
## Risks             no TBDs: open questions become decisions before council
## Review
```

Phase rules:

- P1 is the thinnest slice that works end to end.
- Each phase can be shown working on its own, fits one fresh builder session, and leaves the system working.
- Every done-when names how it's checked.

## 5. Council

blueprint runs the `council` skill with a plan-review brief:

- Reviewers find uncovered requirements, wrong assumptions, steps a builder can't follow, broken order, missing checks, simpler options, and scope creep.
- Any addition must name the requirement it protects.
- Zero findings is a valid answer.
- `blocker` builds the wrong thing. `should` is a gap a builder will hit. `nit` is the rest.
- **APPROVE** means no blocker or should is open.

The coordinator checks every finding itself and re-grades its severity. It fixes, disputes with evidence, or declines. Each round of edits bumps the plan's Revision.

| Outcome | Rule | Status |
|---|---|---|
| Agreed | Every member APPROVEs the current revision | `reviewed` |
| Settled | Disputed after two replies, or out of rounds | `ready`: the coordinator picks the smallest option that reaches every done-when, and logs both sides. A reopened `user` decision still goes to you |
| Can't run | Council members unreachable | `draft` |

Rounds: 3. Up to 5 only for auth, security, data loss, migrations, or money, while an evidenced blocker or should is open.

## 6. Hand-off

You get the plan path, one line per phase, the rounds used, and the models that ran. A `reviewed` or `ready` plan ends with "Plan ready. Start with P1: <one line>." A map starts with E1's P1. `ready` also lists each call the coordinator made.
