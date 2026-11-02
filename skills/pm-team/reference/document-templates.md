# Document templates

Section headings are fixed so reviewers and the consistency checker can reference them. Write content in the user-facing language from STATE.md; keep IDs (US-, D-, R-, P-) unchanged across languages.

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
Exactly the MVP items from product.md §6 (reference IDs).

## 2. Phases & milestones
| Phase | Goal | Output | Exit criterion | Range |

## 3. Tasks
| ID | Task | Story | Size | Depends on | Owner role |

## 4. Dependencies & critical path
Internal and external (APIs, vendors, approvals, content). Critical path stated.

## 5. Estimates
Range per phase with basis (comparable work / spike / assumption). Total range.

## 6. Capacity
Assumed team, availability, what changes if team differs.

## 7. Budget
Range with drivers (people, infrastructure, third-party services, contingency); or "needs user input" → U-id.

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
