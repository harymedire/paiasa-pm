# Findings format

Every reviewer (Head of Product, Delivery Lead, Tech Skeptic, Consistency Checker) reports findings in exactly this format. The orchestrator computes the gate from these fields, so do not add free-form verdicts.

## One finding

```markdown
### F-<round>-<reviewer-code>-<n>: <short title>
- Criterion: <rubric id, e.g. P3>  (or "consistency" / "prompt-executability")
- Status: satisfied | partially-satisfied | not-satisfied | not-applicable
- Severity: critical | significant | minor          (omit when Status = satisfied / not-applicable)
- Evidence: <exact section of the document, quote of ≤2 lines, source link, or test result>
- Problem: <what is wrong or missing, one or two sentences>
- Closure condition: <exactly what must be added, changed or proven to close this>
- Reopens: <decision id from decisions.md, or "no">
- Reopen basis: new-evidence | changed-assumption | error-in-prior-reasoning   (only if Reopens ≠ no)
```

Reviewer codes: `HOP` Head of Product, `DL` Delivery Lead, `TS` Tech Skeptic, `CC` Consistency Checker.

## Severity definitions (use the examples, not intuition)

**critical**: the plan would fail or cause serious harm if executed as written.
- MVP does not solve the problem the research identified.
- Deadline is impossible with the stated team and dependencies.
- A required legal, security or privacy obligation is ignored (payments, personal data, health data).
- Core technical assumption is unverified and the whole plan depends on it.
- Two documents contradict each other on scope, deadline or budget.

**significant**: the plan can proceed only after this is fixed, or it will cause rework.
- A user story has no measurable acceptance criteria.
- A risk is named but has no owner or mitigation.
- An estimate has no stated basis.
- A claim about the market or users has no source and is presented as fact.
- A dependency between tasks is missing from the plan.

**minor**: improves quality, does not change any decision.
- Unclear wording, missing cross-reference, formatting.
- A detail that would be nice but does not affect scope, cost or risk.

If in doubt between two levels, choose the higher one and explain why in Problem. Downgrading severity to make a document pass is a process violation; the judge spot-checks classifications.

## Reviewer file layout

`.product/reviews/round-<N>/<reviewer-code>.md`

```markdown
# Review round <N>, <role>
Reviewed files: <list with the STATE.md version/hash or timestamp>
Independent pass completed before reading history: yes

## Criteria summary
| Criterion | Status | Severity |
|---|---|---|
| P1 | satisfied | |
| P2 | not-satisfied | significant |

## Findings
<findings in the format above, only for criteria that are not satisfied, plus any extra issues>

## Reopened decisions
<list, or "none">

## Optional score
<0–10, informational only, never used for the gate>
```

## Author response format

Authors (PO, PM) answer every open finding in `.product/reviews/round-<N>/responses.md`:

```markdown
### F-2-HOP-3
- Action: fixed | justified | needs-user-decision | needs-experiment
- Change: <what changed and where>            (if fixed)
- Rationale: <why the finding should not be applied; evidence>   (if justified → also add D-entry to decisions.md)
- Question for user: <...>                     (if needs-user-decision → also add to decisions-for-you.md)
- Experiment: <smallest test that would settle it>   (if needs-experiment)
```
