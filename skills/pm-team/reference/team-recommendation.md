# Team recommendation (`.product/handoff/team.md`)

Written in the handoff phase by the Project Manager agent, reviewed by the Delivery Lead (and Tech Skeptic when active). The DEV team's orchestrator reads it to extend its agent team and models. Recommend only what the project's risk and scope justify; every addition needs a reason.

## Template

```markdown
# Team recommendation: <project>

## Project profile
- Type: web app | mobile | API/backend | internal tool | data/AI | integration-heavy | other
- Complexity: low | medium | high, because <...>
- Risk flags present: architecture / clarity / performance / novelty / security (with reasons)
- Sensitive areas: <payments, personal data, health, auth, multi-tenant, ...>

## Human team
| Role | Engagement | Why | Must-have skills |
|---|---|---|---|
| Product owner (user) | ... | product decisions, user validation, acceptance | |
| Tech Lead who codes | full-time | architecture, risky reviews, merge | <stack> |
| Developer(s) | 1–2 | ... | |
| Product Designer | part-time | usability, consistency, user testing | |
| QA | assigned responsibility / specialist | depends on risk | |
| DevOps / security | external as needed | | |
Do not promise productivity multipliers. State what each role owns.

## Agent team (PAIASA DEV)
Default team is always available. List only changes:

### Extra specialist agents
| Agent name | Purpose | When it runs | Model tier | Key instructions |
|---|---|---|---|---|
| payments-specialist | Review PSP integration, idempotency, webhooks, reconciliation | every task with payments flag | top | follow PSP docs <link>; test mode only |

### Model overrides
| Agent | Default tier | Recommended | Reason |
|---|---|---|---|
| implementer | strong | top for P-03, P-07 | concurrency logic in booking |

### Mandatory gates for this project
- <e.g. security-reviewer on every task touching /auth or /payments>
- <e.g. load test before release: 200 concurrent bookings, p95 < 400 ms>

## Project rules (for CLAUDE.md)
- Stack and versions: ...
- Conventions: ...
- Environments: dev / staging / production, and who may deploy to each
- Compliance: ...
- Definition of done additions: ...

## Open items
- <anything the dev team must confirm with the user before starting>
```

## Model tiers

The DEV plugin maps tiers to concrete models (see its README). Use tiers here so the recommendation stays valid when models change:
- **top**: hardest reasoning, irreversible or high-risk decisions (architecture, security, concurrency, money).
- **strong**: standard implementation, testing, review.
- **fast**: mapping, summarizing, formatting, evidence assembly.
