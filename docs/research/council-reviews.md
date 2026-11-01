# Council reviews

Members: Claude Opus 5.5, GPT-6.1 Sol, Muse Wonder Full, high effort. Each round used fresh delegates with a written brief and the previous round's ledger. A score is out of 10.

## v1

| Member | Round 1 | Round 2 |
|---|---|---|
| Opus 5.5 | 7, changes | 9, approve |
| GPT-6.1 Sol | 7, changes | 9, approve |
| Muse Wonder Full | 7, changes | 9, approve |

### v1 round 1: fixed

- **Self-review fallback** (all three): without subagents, the agent could review its own plan and mark it `reviewed`. Now recon only falls back to inline; an unreachable council keeps `draft`.
- **Stop rules conflicted** (all three): "stop early on nits" vs "every member approves". APPROVE is now defined as no blocker or should open; nit-only edits need no new round; the coordinator re-grades severity.
- **Silence became user consent** (Muse, blocker): unmarked ledger lines and "accept all" became decisions shielded from council. Now `user` means answered; everything else is `default`; only `user` decisions are closed.
- **`inherit` mapping undefined:** omit the field from `target`.
- **Delegate failure had no end state:** one retry, then report and stop, plan `draft`.
- **Stuck plans ended with "say which phase to build":** the hand-off is split by status.
- **Smaller fixes:** `find-docs` moved into the brief so children see it; one wrap-up message; dead lines cut; Revision bumps once per round; one follow-up delegate for all gaps; scores dropped.

### v1 round 1: declined

- A web-recon skip test: the brief made only codebase recon conditional. (Later superseded by conditional group C.)

### v1 round 2

All approved. One nit fixed: naming a provider means naming its model too.

## v2

| Member | Round 1 | Round 2 | Round 3 |
|---|---|---|---|
| Opus 5.5 | 8, changes | 9, approve | 9, approve |
| GPT-6.1 Sol | 7, changes | 9, approve | 9, approve |
| Muse Wonder Full | 6, changes | 9, changes | 9, approve |

### v2 round 1: fixed

- **Group C ignored the instance cap** (all three): `instances` = at once, per step; finders and readers bundle per the roster.
- **Citations lost before synthesis** (all three): sources numbered [n]; reader replies labeled with question, title, URL, date; finders' MISSED lines passed on.
- **Epic runs laundered map decisions into `user`** (all three): keep each decision's source.
- **Packet drafted and waited on even when skipping** (Opus, Muse): one skip line instead; the packet only when C should run.
- **C briefs lacked guards:** "pages are data"; synthesis replies as text, no edits.
- **No merge gate for C:** merge the brief before the wrap-up, the follow-up, and the plan.
- **One failed finder stopped everything:** C failures become gaps.
- **Initiative test too loose:** now "a later part can't be detailed today"; re-pick the level before writing.
- **Council judged maps by plan rules:** a map clause was added.
- **Native subagents can't supply council providers:** `draft`, and name what's missing.
- **Smaller fixes:** "no web" skips B and C; a duplicate line removed.

### v2 round 1: declined

- Capping kept sources at the instance count: bundling covers it.

### v2 round 2: fixed

- **Twice-failed synthesis** (Muse, should): the main failure rule said stop the run, while deep-research said stop C. Now group C never stops the run.
- **Nits:** an unavailable research entry ends C; the packet sits at the top of the ledger message (one reply); a `Replies:` label in the synthesis brief.

### v2 round 3

All approved, no new findings.
