# Document templates

Section headings are fixed so reviewers and the consistency checker can reference them. Write content in the user-facing language from STATE.md; keep IDs (US-, D-, U-, T-, R-, M-, TA-, S-, P-) unchanged across languages.

## Single source of truth

Every shared number and list has exactly **one owning section**. Only that section states the value. Any other document that needs it writes a reference, e.g. `Budget: → delivery-plan.md §7` or `Must stories: → product.md §7`, optionally with the ID it depends on. Never copy the value "for convenience": copies go stale on the next revision and turn into review findings.

| What | Owning section | Others write |
|---|---|---|
| MVP scope, in/out list | product.md §6 | `→ product.md §6` |
| Stories, priorities, Must/Should/Could counts, acceptance criteria | product.md §7 | story IDs only; prompts copy ACs (the one allowed copy, checked in handoff) |
| NFR targets (load, latency, availability) | product.md §11 | `→ product.md §11` |
| Tasks, task sizes | delivery-plan.md §3 | task IDs only |
| Phase ranges, milestones, total duration | delivery-plan.md §2 / §5 | `→ delivery-plan.md §5` |
| Team composition, availability, capacity (person-days) | delivery-plan.md §6 | `→ delivery-plan.md §6` |
| Total budget range (people + services + contingency) | delivery-plan.md §7 | `→ delivery-plan.md §7` |
| Infra and third-party service costs | tech-assessment.md §6 | delivery-plan.md §7 lists `services: → tech-assessment.md §6` as an input to its total (a derived value; when the input changes, the total is re-synced mechanically) |
| Architecture and stack choice | tech-assessment.md §2 | `→ tech-assessment.md §2` |
| Decisions | decisions.md (D-id) | `per D-0xx` |
| Open user decisions and their option costs | decisions-for-you.md (U-id) | `[ASSUMPTION] → U-xx` |

If the tech assessment is inactive, its rows move to delivery-plan.md §7.

## Precision rules

Precision must match the decision it supports. False precision creates findings that change nothing.

| Quantity | Write as | Tolerance (a difference inside it is not a finding) |
|---|---|---|
| Effort | range in whole person-days (≥ 10 pd: round to 5 pd) | ± 1 pd or 5% of the total, whichever is larger |
| Duration | range in weeks, rounded to 0.5 week | ± 0.5 week |
| Money | range, 2 significant figures (e.g. 18–24k EUR) | ± 5% of the total |
| Percentages, probabilities | whole numbers, or low / medium / high | ± 5 points |
| Counts (stories, tasks) | exact | 0 (but a stale copy elsewhere is mechanical) |

Show the arithmetic once, in the owning section (inputs → result). Other sections reference the result.

## `.product/product.md`: Product Owner

```markdown
# <Product name>: product definition
Version: <n>, updated <date>

## 1. Problem
Who, in what situation, has what pain; current workaround; evidence (links to research).

## 2. Users
Segments; primary segment and why; jobs-to-be-done; key pains and gains.

## 3. Value proposition
Why a user switches from the current alternative (incl. "do nothing").

## 4. Vision and positioning
One-paragraph vision; positioning vs top 3 alternatives.

## 5. Success metrics
| Metric | Baseline (or how to get it) | Target | How measured | When |

## 6. MVP scope
| Item | In MVP? | Maps to problem | Why |
Explicit "Not in MVP" list with reason.

## 7. Backlog
### US-01: <title>
As a <user>, I want <capability> so that <outcome>.
- Priority: must | should | could
- Acceptance criteria: AC1 Given/When/Then ...
- Notes / dependencies / related decisions

## 8. User flows
Step-by-step main flows incl. empty, error, edge states. Link Figma if exists.

## 9. Riskiest assumptions & validation plan
| Assumption | Why risky | Test (interview / data / prototype / experiment) | Kill/continue criterion | Owner |

## 10. Compliance & data
Personal data, payments, regulatory obligations; or "not applicable" with reason.

## 11. Non-functional requirements
Expected users and load, response times, availability, data volume, supported devices/browsers, languages.

## 12. Roadmap after MVP
Next 2–3 increments with the hypothesis each tests.
```

## `.product/delivery-plan.md`: Project Manager

```markdown
# <Product name>: delivery plan
Version: <n>, based on product.md v<n>

## 1. Scope
Exactly the MVP items from product.md §6 (reference IDs only; do not restate counts).

## 2. Phases & milestones
| Phase | Goal | Output | Exit criterion | Range |

## 3. Tasks
| ID | Task | Story | Size | Depends on | Owner role |

## 4. Dependencies & critical path
Internal and external (APIs, vendors, approvals, content). Critical path stated.

## 5. Estimates
Range per phase with basis (comparable work / spike / assumption). Total range. Rounded per the precision rules; arithmetic shown once.

## 6. Capacity
Assumed team, availability, capacity in person-days per phase; what changes if team differs. If team size is an open user decision, plan on the recommended option as `[ASSUMPTION] → U-xx` and refer to the other options with `→ U-xx` (their duration and cost deltas live in the U-item). Do not maintain parallel full plans.

## 7. Budget
Range with drivers (people, services `→ tech-assessment.md §6`, contingency); or "needs user input" → U-id.

## 8. Risks
| ID | Risk | Prob. | Impact | Owner | Mitigation | Trigger |

## 9. Quality & release
Environments (dev/staging/prod); QA approach; UAT: who accepts and how; release & rollback; post-release monitoring.

## 10. Change management
How changes are requested, evaluated (time/cost/risk), decided and logged.

## 11. Reporting
Cadence; what the user receives; escalation path.
```

## `.product/tech-assessment.md`: Tech Skeptic (when active)

```markdown
# Technical assessment
## 1. Key technical assumptions
| Assumption | Verified? | Evidence / doc link | If unverified: spike proposal |
## 2. Proposed architecture & stack
Option chosen, alternatives considered, why. Diagram in text if useful.
## 3. External dependencies
| Service/API | Purpose | Pricing | Limits | Terms/risks | Doc link, check date |
## 4. Security & data protection
Auth model, authorization, data storage & retention, secrets handling, short threat model (who could abuse what, how).
## 5. Non-functional feasibility
Can the stack meet the NFRs in product.md §11; what needs load testing.
## 6. Cost basis
Infra and service costs at MVP scale and at 10× scale.
## 7. Technical debt & constraints
Known shortcuts accepted for MVP and when to repay them.
```
