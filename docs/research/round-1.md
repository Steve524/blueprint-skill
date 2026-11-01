# Research round 1

16 read-only delegates (6 Muse Wonder Full, 8 GPT-6.1 Sol, 2 Claude Opus 5.5, all at high effort), one angle each. Condensed findings by topic. Sources: [sources.md](sources.md).

## The brief

- Use claudex-loop's workflow (interview, plan, plan review), not its engineering. Stop before building.
- Provider and model agnostic, with models from a roster.
- Recon in two delegate groups: codebase (if needed) and online.
- The `council` skill replaces Codex as plan reviewer, looping until members are satisfied.
- Ideas from BMAD-METHOD. Runs in T3 Code, with native subagents as the fallback.

## claudex-loop at f8c111de

- No runner scripts at this commit; the workflow is all in SKILL.md.
- **Phase 0, recon:** brownfield vs greenfield; a research gate (none / web / deep); one batched assumptions ledger with sources.
- **Phase 1, interview:** a visible decision map. Load-bearing decisions (migration, rewrite, security hole, user trust) are asked one at a time: question, why it matters, a committed recommendation, if wrong. A weak "if wrong" demotes the question to cosmetic. Facts found in code are logged, not asked. "Accept all remaining recommendations" is the escape hatch.
- **Plan:** Goal, Approach, Key decisions, Toolchain, Assumptions, Risks, Out of scope. No phases or acceptance commands (gap to fill).
- **Phase 2, review:** an adversarial reviewer; VERDICT APPROVED / REVISE; 5 rounds max; the host arbitrates with logged reasons; "a flagged disagreement beats a false approved".
- A later local version (2.1.0) added SHA256-bound approval and a BLOCKED verdict, and reversed "silence = approval".

## Interview (BMAD, mattpocock, local skills)

- BMAD: "elicitation, not direction"; reach a working mode in 2-3 turns; a fast path with `[ASSUMPTION]` tags. Personas, party mode, and the 71-method catalog are theater for this use.
- Inline the rules rather than call `grilling`: grilling stops only when everything is settled, and asks the whole frontier per round. `grill-with-docs` can't be called by another skill.
- Questions: at most ~4 lines, "yes" accepts the recommendation, the escape hatch in every footer.

## Recon (Anthropic, OpenAI, claudex)

- Order: quick intake → recon → ledger → interview → targeted recon on factual gaps.
- Briefs need an objective, an output format, sources, and boundaries (Anthropic). Vague briefs duplicate work.
- Effort scaling: 1 agent for simple, 2-4 for comparisons, 10+ only for complex research.
- Returns: claim | evidence | confidence, plus UNVERIFIED and gaps. Conflicts stay `contested`.

## Roster

- The [RimWorldModToolbox roster](https://github.com/Steve524/RimWorldModToolbox/blob/main/team/roster.yaml): provider (an exact instance id), model, effort, instances. Staffing is separate from the workflow; never substitute.
- Proposed: a roster beside the skill, `inherit` by default.

## Council for a plan

- Council has no verdict format and no round cap, and scores only for code review. Its pre-audit step (fix PR comments, run checks) doesn't apply to a plan.
- Wrap it with a plan-review brief: blocker / should / nit, APPROVE / REVISE, zero findings valid, additions name their requirement.
- BMAD's "at least 10 findings" quota caused endless nitpicking (BMAD issues #1332, #1815).

## Plan format (OpenAI, BMAD, spec-kit, Kiro, Taskmaster)

- One self-contained file (OpenAI ExecPlans: "Every ExecPlan must be fully self-contained").
- Stable requirement ids traced to phases (BMAD, spec-kit). EARS-style acceptance (Kiro) is useful, but still needs a runnable check.
- A phase is about one reviewable PR: thinnest end-to-end slice first, leaves the system working.
- Never record a check result that wasn't run.

## T3 orchestration

- `orchestrator_capabilities` once, `delegate_task` async per delegate, save task ids, end the turn, `task_status` on notice. No polling.
- Children get no parent history; `role` doesn't enforce read-only, the brief must. Fresh delegate per council round.
- No delegate concurrency cap found.

## Portability (Google, Cursor, OpenCode, Muse Code)

- Only `name` + `description` frontmatter is honored everywhere.
- Every harness ties plan approval to building, so the skill must stop itself.
- OpenCode's plan mode doesn't restrict bash, so don't rely on harness plan modes for read-only.
- Muse Code has built-in `/plan` and `/grill`; avoid those names.

## Failure modes (adversarial review)

| Failure | Guard |
|---|---|
| Delegate or round blowup | Small defaults, caps, no recursive delegation |
| Contextless children | Self-contained briefs |
| Hallucinated or stale sources | claim → source → date; the coordinator opens decision-bearing sources |
| Prompt injection from pages | Pages are data; read-only children |
| Sycophantic convergence | Independent first pass; evidence for findings |
| Endless nitpicking | Zero findings valid; severity; cap |
| Reviewer scope creep | Additions must name the requirement they protect |
| Plan drifts from user decisions | Decisions carried in the plan and the brief |
| Skill starts building | An explicit last-action rule |
| Provider unavailable | Report; never substitute |

## Two strawman drafts

- **Full draft (Opus):** ~150 lines in sol-loop's style. Budget section, explicit skip rule for codebase recon, brief templates, stop states agreed / stuck.
- **Minimal draft (Opus):** ~70 lines, leaning on `grilling` and `council`. It listed what to leave out (roster file, log file, plan hash, phase files, personas, research gate) and when each should come back.
