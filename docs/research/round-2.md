# Research round 2

10 read-only delegates (6 Muse Wonder Full, 4 GPT-6.1 Sol, all at high effort), run after the v2 requests: roster instances, A/B/C recon with deep research, and initiatives.

## Matt Pocock (mattpocock/skills at 4ae2317d)

- Research is **one** primary-source subagent writing one cited file. No question approval, no pipeline.
- Facts are the agent's job. Never block the question frontier on a fact.
- No initiative tier: spec → tracer-bullet tickets. Oversized work goes through `wayfinder`, then collapses back to one spec.
- "Fog of war": don't pre-slice what you can't phrase sharply yet.
- Ticket = demoable end to end, fits one fresh context window, blocking edges explicit. The user quizzes the granularity before publishing.
- No multi-model plan review. For interface choices, "Design It Twice": 3+ subagents with different constraints.

## Andrej Karpathy

- Verification is the bottleneck: small chunks, concrete prompts.
- Ask for approaches with pros and cons before code.
- Partial autonomy, a human-set slider. Deep research is a first draft, not an answer.
- Verifiability predicts where AI works, so every phase should name its verifier.
- Use mixed models only to re-check contested, load-bearing claims.
- LLM Wiki: keep raw sources separate from synthesis; flag contradictions.

## Theo / tstack at 1085050f

- No public research or planning skill. All 9 tstack skills are build, review, or PR work.
- Council = provider diversity, one flagship each, no instances, no round cap upstream.
- Scales by composing flat skills, never tiers.
- Planning interviews use `grilling`.
- T3 Code: don't depend on native plan mode (per-provider). Durable delegate threads and HTML renders exist.

## YouTube (Cole Medin, Boris Cherny / Cat Wu, IndyDevDan, Sean Grove, BMAD tutorials)

- Research subagents, then force questions back to the human: "reduce the number of assumptions".
- Phases planned separately, each with a validation strategy written before code. The plan is the only context a fresh builder gets.
- "Poke holes" second wave to kill false positives (Cherny's review setup).
- "The plan is the prompt" (IndyDevDan); specs are the unit of programming (Grove).
- A BMAD user threw out an entire epic built on a wrong schema: sign off on architecture before slicing.
- Cherny later moved away from plan mode for small PRs. The one-commit off-ramp covers that end.

## Open-source deep research (open_deep_research, gpt-researcher, STORM, dzhng/deep-research)

- One clarification, then a standalone research brief.
- Supervisors delegate distinct, non-overlapping subtopics; default max ~5 concurrent.
- Curate sources: primary first, max ~10. Deep-read = structured summary + verbatim excerpts.
- A separate writer; one citation number per URL.
- "Stop when you can answer confidently."
- None of them resolve conflicts explicitly. Keeping `contested` visible is ahead of them.
- Proposed the finder, reader, and synthesis brief templates used in `deep-research.md`.

## Official deep research (OpenAI, Anthropic, Google, Perplexity)

- OpenAI separates clarification, prompt rewriting, and research; caps tool calls; warns about prompt injection.
- Anthropic: objective, format, tools, and boundaries per child; scale effort; citation pass; primary sources over content farms.
- Google Gemini: the user edits the research plan before "Start research". This is the approval gate.
- Proposed: C is offered, not automatic; 2 finders, 6 sources max, 2 readers by default.

## Big-name developers (Willison, Harper Reed, Kent Beck, Osmani, Huntley, Steinberger, Hashimoto)

- One authoritative plan; human gates; small steps.
- Harper Reed: spec → "blueprint" → prompt_plan → todo → build. A name overlap only.
- Kent Beck: agents add unrequested complexity; intervene actively.
- Hashimoto: research prepares decisions, it doesn't make them.
- Make C conditional; `instances` defaults to 1; defer initiative machinery.

## GitHub planning skills (superpowers, Anthropic feature-dev and doc-coauthoring, OpenAI skills, GSD)

- Discovery questions about intent stay open; recommendations are for technical choices.
- A fresh-reader test for plans.
- The research brief ends with implications for phases.
- Keep the core short, with details in references.

## Roster and the A/B/C split

- One list per group; synthesis uses the first `research` entry.
- One unit per delegate, round-robin; never invent units; warn on cost.
- A full lineup (10 finders + 10 readers + 1 synthesis) could reach 21 delegates.
- Keep machine-specific provider ids out of synced defaults.

## Initiatives and epics

- BMAD: epic = one coherent outcome over several sessions; initiative = several epics. Epics are written thin, detail added just in time.
- Shape Up: appetite caps scope. spec-kit and Kiro detail one feature (epic level). Linear's initiatives are tracking, not planning.
- Proposed rule: one plan while every phase can get files, steps, and checks today; otherwise an initiative map with an epics table, and one blueprint run per epic later.
- 5 of 10 delegates said defer or keep it light. Adopted compactly.
