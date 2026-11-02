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
- Phase: 0-intake | 1-research | 2-draft | 3-review (round N) | 4-judge | 5-consistency | 6-handoff | 7-decisions | done | acceptance
- Last updated: <YYYY-MM-DD HH:MM>

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

Append-only. Never delete entries; supersede them.

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

Everything that changes the user's money, obligations, deadlines or core business direction. Agents recommend; the user decides. Silence is never approval.

```markdown
## U-003: Budget range for MVP
- Status: open | answered (<date>, <answer>)
- Blocking: yes, the delivery plan cannot be finalized without it
- Question: <one sentence>
- Options:
  1. <option>: cost <range>, time <range>, risk <...>, consequence <...>
  2. <option>: ...
- Recommendation: <option N>, because <reason with evidence>
- What happens until you decide: <e.g. plan uses option 1 as a marked assumption>
```

Examples that always go here: budget, hiring, deadlines committed to third parties, choice of paid vendors, launching to real users, legal/compliance trade-offs, pivots of target segment or business model, killing or adding a major feature.
