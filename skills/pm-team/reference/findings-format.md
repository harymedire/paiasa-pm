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
- Class: substantive | mechanical | late          (reviewers write substantive or mechanical; the orchestrator may set late during triage)
- Depends on: <U-id from decisions-for-you.md, or "none">
- Reopens: <decision id from decisions.md, or "no">
- Reopen basis: new-evidence | changed-assumption | error-in-prior-reasoning   (only if Reopens ≠ no)
```

Reviewer codes: `HOP` Head of Product, `DL` Delivery Lead, `TS` Tech Skeptic, `CC` Consistency Checker.

## Severity definitions (use the examples, not intuition)

### Materiality test (apply before choosing critical or significant)
Ask: **if this is fixed, does any decision, scope item, date range, cost range, or what a developer builds change?**
- No → it is `minor`, however many times it appears.
- Yes → choose critical or significant by the examples below.

**critical**: the plan would fail or cause serious harm if executed as written.
- MVP does not solve the problem the research identified.
- Deadline is impossible with the stated team and dependencies (outside the stated range, not by rounding).
- A required legal, security or privacy obligation is ignored (payments, personal data, health data).
- Core technical assumption is unverified and the whole plan depends on it.
- An owning section commits to a scope, deadline or budget that is unapproved and presented as approved.

**significant**: the plan can proceed only after this is fixed, or it will cause rework.
- A user story has no measurable acceptance criteria.
- A risk is named but has no owner or mitigation.
- An estimate has no stated basis.
- A claim about the market or users has no source and is presented as fact.
- A dependency between tasks is missing from the plan.
- A **substantive** cross-document contradiction: two owning sections disagree on what will be built, when, or for how much, so a reader cannot tell which is intended.
- Capacity vs estimate gap larger than the precision tolerance (more than 10% of the total, or enough to move a milestone outside its range).

**minor**: improves quality, does not change any decision.
- Unclear wording, missing cross-reference, formatting.
- A detail that would be nice but does not affect scope, cost or risk.
- **Mechanical** inconsistency: a non-owning document has a stale copy of a number, an outdated or renumbered ID, a broken cross-reference, or a rounding difference, and the owning section is clear. The orchestrator fixes these directly; they never cost a review round.
- An arithmetic difference inside the rounding tolerance in `document-templates.md` (e.g. 37.5 vs 38 person-days).

If in doubt between two levels, apply the materiality test and explain in Problem. Downgrading severity to make a document pass is a process violation; reclassifying per these definitions is not. The judge spot-checks classifications in both directions.

### Findings that depend on a user decision
If the finding would disappear or change depending on how an open U-item is answered (e.g. "plan does not fit the budget" while the budget is U-03, still open), set `Depends on: U-03`, and in Closure condition write what the answer must be for it to close (or what changes per option). Do not ask the author to re-optimize the plan around the undecided value. These findings do not fail the gate; they keep the project in `waiting-on-user`.

### Round 2 discipline
In round 2, focus on (a) whether round-1 closure conditions are met and (b) sections that changed since round 1 (listed in your task). A new non-critical finding on unchanged text is recorded but counted as `late` (minor). Do not re-derive totals or capacity arithmetic that you already accepted in round 1 unless the inputs changed.

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

Each author answers every open finding addressed to it in its **own** file: `.product/reviews/round-<N>/responses-PO.md`, `responses-PM.md` or `responses-TS.md`. Never write another author's file, `decisions.md` or `decisions-for-you.md`.

```markdown
### F-2-HOP-3
- Action: fixed | justified | needs-user-decision | needs-experiment
- Change: <what changed and where>            (if fixed)
- Rationale: <why the finding should not be applied; evidence>   (if justified → also propose a D-entry below)
- Question for user: <...>                     (if needs-user-decision → also propose a U-entry below)
- Experiment: <smallest test that would settle it>   (if needs-experiment)
```

At the top of the file, list **Sections changed** (document + section number), so the next round's reviewers know where to look. At the bottom:

```markdown
## Proposed decision entries
<full D- and U-entries in the state-and-decisions.md format, using IDs from your assigned range; the orchestrator appends them>
```
