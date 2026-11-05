# State, decision log and user decisions

## `.product/STATE.md`

Updated by the orchestrator at the end of **every** phase and before stopping for any reason. It is the only file needed to resume.

```markdown
# Project state
- Project: <name>
- Input: <original sentence / link / folder>
- Mode: new | resume | adopt-existing
- Languages: user-facing=<e.g. bs>, dev-prompts=<e.g. en>
- Tech Skeptic: active | inactive (reason) | activate-after-MVP
- Phase: 0-intake | 1-research | 2-draft | 3-review (round N) | 4-judge | 5-consistency | 6-handoff | 7-summary | waiting-on-user | not-ready | done | acceptance
- Gate: not-run | pass | pass-pending-user | fail (round N)
- Last updated: <YYYY-MM-DD HH:MM>

## Review budget used
- Review rounds: <0–2>/2 · Judge: <0–1>/1 · Post-judge verify: <0–1>/1 · Consistency: checker <0–1>/1, owner fix <0–1>/1
- Counted critical+significant per round: R1=<n>, R2=<n>   (convergence check: R2 must be lower)

## ID ranges
| Owner | D- | U- | Other |
|---|---|---|---|
| Orchestrator | D-001–D-099 | U-01–U-19 | |
| PO | D-100–D-199 | U-20–U-39 | US- |
| PM | D-200–D-299 | U-40–U-59 | T-, R-, M- |
| TS | D-300–D-399 | U-60–U-79 | TA-, S- |
| Judge | D-900–D-999 | U-90–U-99 | |
Next free IDs: <e.g. D-104, D-203, U-22, US-14, T-31, R-09>

## Done
- <phase>: <one line result, files>

## Next step
<exactly what the next run should do first>

## Waiting on the user
- <U-id>: <question> (blocking: yes/no)

## Open findings
<count by severity; link to latest review round>
```

## `.product/decisions.md`: decision log

Append-only. Never delete, renumber or reorder entries; supersede them. **Only the orchestrator writes this file**: agents propose entries in their own output files (using IDs from their assigned range) and the orchestrator appends them. This prevents parallel agents from overwriting each other.

```markdown
## D-007: MVP excludes online payments
- Date: 2026-11-02
- Status: active | superseded by D-0xx | reopened
- Decided by: PO | PM | judge | user
- Context: <what question was being decided>
- Decision: <what>
- Rationale: <why, with evidence references>
- Rejected alternatives: <option: why rejected>
- Related findings: F-1-HOP-4, F-2-DL-1
- Reopen only if: <the specific new evidence or changed assumption that would justify reopening>
```

Reviewers may reopen a decision **only** with new evidence, a changed assumption, or a concrete error in the earlier reasoning (state which in `Reopen basis`). Re-raising the same objection without one of these is recorded by the orchestrator as a loop signal.

## `.product/decisions-for-you.md`: decisions for the user

Everything that changes the user's money, obligations, deadlines or core business direction. Agents recommend; the user decides. Silence is never approval. **Only the orchestrator writes this file** (same rule as decisions.md).

This file is the owning section for option costs. Each option is costed **once**, at decision precision (precision rules in document-templates.md). Authors do not keep re-optimizing the plan while the item is open; they plan on the recommendation as `[ASSUMPTION] → U-xx`.

```markdown
## U-03: Budget range for MVP
- Status: open | answered (<date>, <answer>)
- Blocking: yes, the delivery plan cannot be finalized without it | no
- Question: <one sentence>
- Options:
  1. <option>: cost <range>, time <range>, risk <...>, consequence <...>
  2. <option>: ...
- Recommendation: <option N>, because <reason with evidence>
- What happens until you decide: <e.g. plan uses option 1 as a marked assumption>
- Affects: <owning sections that change with the answer, e.g. delivery-plan.md §5–§7>
- Findings waiting on it: <F-ids tagged Depends on: U-03>
```

Examples that always go here: budget, hiring, deadlines committed to third parties, choice of paid vendors, launching to real users, legal/compliance trade-offs, pivots of target segment or business model, killing or adding a major feature.
