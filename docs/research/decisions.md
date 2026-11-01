# Decisions

Each entry: what we chose, why, and what we rejected. Reopen one only with new evidence.

## Scope

| # | Decision | Why | Rejected |
|---|---|---|---|
| D1 | Stop after the plan. No build, no code inspection | The goal is a plan file. Every harness ties "approve plan" to "start building" (Cursor Build, Antigravity Proceed, Gemini approve), so the skill has to stop itself | claudex-loop's build and inspect phases |
| D2 | Take claudex-loop's **workflow**, not its engineering | The interview, plan, and review loop is the value. Its CLI runners, model pins, and session plumbing tie it to two providers | Runner scripts, `--resume`, Codex CLI flags |
| D3 | Provider and model agnostic | Models change. Recon models live in `roster.yaml`; the council skill picks reviewers | Hardcoded model names in the skill |
| D4 | Write only the plan, plus the research brief when C runs | Fewer files, less drift. The plan links the brief and copies the decisions it needs | A separate review log, glossary or ADR writes, per-phase files |

## Trigger and name

| # | Decision | Why | Rejected |
|---|---|---|---|
| D5 | Name `blueprint`; trigger only on the word "blueprint" | It starts a paid multi-provider run, so it shouldn't fire by accident. No clash with "plan mode" or Muse Code's `/plan` | Model-invoked description; `plan-loop`, `plan-first` |
| D6 | The name overlap with Harper Reed's "blueprint" step is fine | His is an intermediate doc in a build flow; this is a standalone skill | Renaming |

## Intake and level

| # | Decision | Why | Rejected |
|---|---|---|---|
| D7 | Intake = goal, done-when, out of scope, asked once | Enough to aim recon without an interview first | A long upfront interview |
| D8 | One-commit changes get an inline plan instead | Planning ceremony on trivial work is waste | Always running the full skill |
| D9 | Initiative level: only when a later part can't be detailed today | BMAD's thin epics, written just in time. 5 of 10 round 2 delegates said defer or keep it light, so it's compact: a map file, and one blueprint run per epic later | BMAD's ticket tree, Linear-style tracking, deferring entirely |
| D10 | Epic runs keep each map decision's source | Otherwise defaults turn into "the user decided" and escape council review | Treating all map decisions as `user` |

## Recon

| # | Decision | Why | Rejected |
|---|---|---|---|
| D11 | Three groups: A codebase, B stack and docs, C deep research | Requested. B answers "what does this API do"; C answers "which approach, and why" | One generic web group |
| D12 | A runs only when the plan must fit existing code | Greenfield has nothing to read | Always running A |
| D13 | C runs only when an approach decision is open that research could change; otherwise one skip line | Every vendor and dev source says scale effort to need. Making you wait on a packet the agent would skip wastes a round trip | Always drafting and waiting on a packet |
| D14 | You approve C's 3-5 questions before any search | Google Gemini's editable research plan, and claudex-loop's deep tier. Concrete questions are verifiable; vague ones spin | Letting the agent research freely |
| D15 | C = find, curate (coordinator), deep-read, one synthesis | Open-source deep-research tools converge on this. One writer avoids mixed voices | A recursive breadth/depth tree, a separate citation agent, STORM personas |
| D16 | At most 6 sources; sources numbered and carried through to synthesis | Keeps reading load sane, and citations can't be made up | Source counts as a quality target |
| D17 | Synthesis tries to refute each decision-bearing claim | Cherny's "poke holes" wave, at low cost | A second review wave |
| D18 | The interview continues while C runs; the brief merges before the wrap-up and the plan | Only decisions that need C's answers wait (Matt Pocock's frontier rule) | Blocking everything on C |
| D19 | Briefs carry the goal, paths, and settled decisions. Pages are data, not instructions | Delegates have no history. Vague briefs cause duplicated and wrong research (Anthropic). Prompt injection risk | Short "research X" prompts |

## Roster

| # | Decision | Why | Rejected |
|---|---|---|---|
| D20 | `roster.yaml` beside the skill; groups `code`, `stack`, `research` are lists of `{provider, model, effort, instances}` | Requested. Staffing stays separate from the workflow, like [RimWorldModToolbox's roster](https://github.com/Steve524/RimWorldModToolbox/blob/main/team/roster.yaml) | No roster file |
| D21 | `instances` = delegates at once, per step | Without a definition, C's stages either overran the cap or ran out | "Total per run" |
| D22 | One unit per delegate, round-robin; spare instances idle; bundle when short | Duplicated angles add reading, not evidence | Filling seats with invented questions |
| D23 | Council isn't in the roster | The council skill already picks one flagship per provider | Council members in the roster |
| D24 | Defaults are `inherit`; machine-specific provider ids stay out of synced defaults | Provider instance ids differ per machine | Shipping account ids |
| D25 | Warn before launching more than 3 delegates at once | Anthropic saw ~15x tokens and 50-agent blowups. A full C can reach ~20 delegates | No warning |

## Interview

| # | Decision | Why | Rejected |
|---|---|---|---|
| D26 | Inline claudex-style rules; don't call `grilling` | grilling stops only when everything is settled, and asks the whole frontier per round. A calling skill can't override that | Calling `grilling` or `grill-with-docs` |
| D27 | Load-bearing questions one per message, at most 4 lines; "yes" takes the recommendation | ADD-friendly, and fast to answer | Multi-paragraph questions, option menus |
| D28 | Approach choices list 2-3 options first | Karpathy and Anthropic's feature-dev: compare before picking | A single recommendation only |
| D29 | "Accept all remaining recommendations" in every question message | The escape hatch from claudex-loop | Relentless grilling |
| D30 | `user` vs `default` source; only `user` decisions are closed to council | Silence isn't consent (council round 1 blocker) | "Unmarked = confirmed" |

## Plan

| # | Decision | Why | Rejected |
|---|---|---|---|
| D31 | One markdown file with R-ids, decisions with sources, phases | Cold builders need it self-contained (OpenAI ExecPlans). Stable ids trace requirements to phases (BMAD, spec-kit) | spec-kit or Kiro's three files |
| D32 | Phase = shown working on its own, fits one fresh builder session, leaves the system working; P1 is the thinnest slice | Tracer bullets (Pocock), small chunks (Karpathy) | Layered phases (all DB, then all API) |
| D33 | Every done-when names how it's checked; never record a check you didn't run | Verification is the bottleneck | "Tests pass" |
| D34 | Phases are written before council | Council has to review the phases. This changed the original order, "phases after council" | Writing phases after review |
| D35 | Show the phase or epic table before council: "Say ok or regroup" | Cheaper than a council round spent on slicing (Pocock's ticket quiz) | No check |

## Council

| # | Decision | Why | Rejected |
|---|---|---|---|
| D36 | Call the `council` skill with a plan-review brief and overrides | Reuse its provider diversity. Skip its code-review parts (pre-audit fixes, scores) | Writing a new reviewer |
| D37 | APPROVE / REVISE; blocker / should / nit; APPROVE = no blocker or should open | Council itself defines no verdict format | Scores as the gate |
| D38 | Any addition must name the requirement it protects; zero findings is valid | Stops scope creep and manufactured findings (BMAD's 10-finding quota caused endless loops) | Minimum finding counts |
| D39 | Coordinator re-grades severity; disputes need evidence | Neither rubber-stamp nor capture | Accepting labels as given |
| D40 | 3 rounds; 5 only for high-stakes areas with an open evidenced issue | Council upstream has no cap. Budget end is not approval | Unbounded "until satisfied" |
| D41 | Approval binds to a Revision number | Nothing consumes a hash yet; the revision echo does the job | SHA256 hashing and a separate log |
| D42 | Fresh delegates every round; the plan is frozen during review | Delegates have no history | Resuming the same session |
| D43 | No self-review fallback. Council can't run → `draft` | "reviewed" must mean independent review | Self-review outside T3 |

## Failure handling

| # | Decision | Why |
|---|---|---|
| D44 | One retry per failed delegate | Transient failures happen |
| D45 | Group C never stops the run. A failed finder or reader → a gap; a failed synthesis or unavailable research entry → C ends | C is optional |
| D46 | Other failures stop the run; the plan stays `draft`; never substitute | No silent model swaps |

## Declined ideas

- A web-recon skip test in v1: C later made deep research conditional anyway.
- An HTML render of the plan: the markdown is the source; add it if wanted.
- A research slider (off / quick / deep) beyond approve, edit, skip.
- Prototype phases, Consumes/Produces fields, a separate citation agent.
- Capping kept sources at the instance count: bundling covers it.
- Personas, party mode, method catalogs (BMAD); Postplan publishing (privacy).

## Open questions

- Real-run tuning: is the default `research` instances of 3 right? Is 6 sources enough?
- Does the initiative level earn its lines? Revisit after the first real initiative.
- Should a reviewed plan get an optional HTML view in T3?
- Should blueprint stay in the author's private skill toolbox (development lane), become a default skill there, or live only here?
- Muse Code sometimes reports "version check timed out" in T3 while still running delegates fine. Watch for false "unavailable" stops.
