# Review rubric

Each criterion is marked **required** (R) or **conditional** (C, required only when the condition applies; otherwise `not-applicable`).

The gate passes when:
1. every required criterion and every applicable conditional criterion is `satisfied`, and
2. there are no open `critical` or `significant` findings from any reviewer.

`minor` findings never block. Numeric scores are informational only.

In the research phase, unknowns are acceptable **if** each has a verification plan (what to check, how, who/when). An unknown without a plan is `not-satisfied`.

## Product criteria: owned by Head of Product

| ID | Type | Criterion | Typical evidence |
|---|---|---|---|
| P1 | R | The user problem is stated concretely (who, situation, pain, current workaround). | product.md §Problem with links to research |
| P2 | R | Claims about the market, competitors and users are classified as fact / inference / assumption / proposal; facts have source + check date. | research/*.md |
| P3 | R | Target users and their main jobs are defined; primary segment is chosen and the choice is justified. | product.md §Users |
| P4 | R | Competitive landscape covers direct, indirect and "do nothing" alternatives, with what each does well and badly. | research/competitors.md |
| P5 | R | Value proposition states why a user would switch from the current alternative. | product.md §Value |
| P6 | R | MVP is minimal: each MVP item maps to the core problem; "nice to have" items are explicitly out of MVP. | product.md §MVP in/out table |
| P7 | R | Every MVP user story has measurable acceptance criteria (Given/When/Then or equivalent). | product.md §Backlog |
| P8 | R | Success metrics are defined with baseline (or how to get it), target and measurement method. | product.md §Metrics |
| P9 | R | Riskiest assumptions are listed with a validation plan (interview, data, prototype, experiment) and a kill/continue criterion. | product.md §Validation |
| P10 | C (UI exists) | Main user flows are described step by step, including empty, error and edge states. | product.md §Flows |
| P11 | C (personal/sensitive data, payments, regulated domain) | Legal, privacy and compliance obligations are identified (e.g. GDPR, PCI DSS, local law). | product.md §Compliance |
| P12 | R | Decisions that belong to the user (money, deadlines, direction) are listed in decisions-for-you.md and not assumed. | decisions-for-you.md |

## Delivery criteria: owned by Delivery Lead

| ID | Type | Criterion | Typical evidence |
|---|---|---|---|
| D1 | R | Scope of the plan matches the MVP exactly (no extra, nothing missing). | delivery-plan.md vs product.md |
| D2 | R | Work is broken into phases and tasks small enough to verify (one task ≈ one reviewable change). | delivery-plan.md §Tasks |
| D3 | R | Dependencies between tasks (and on external parties/APIs) are explicit, with a critical path. | §Dependencies |
| D4 | R | Every estimate states its basis (comparable work, spike result, assumption) and a range, not a single number. | §Estimates |
| D5 | R | Capacity assumption is explicit (team composition, availability) and the timeline is consistent with it. | §Capacity |
| D6 | R | Risk register: each risk has probability, impact, owner, mitigation and trigger. | §Risks |
| D7 | R | Budget is given as a range with its drivers, or explicitly marked as "needs user input". | §Budget |
| D8 | R | QA, UAT and release approach are defined (environments, who accepts, rollback). | §Quality & release |
| D9 | R | Change management: how scope changes are evaluated against time/cost. | §Change |
| D10 | R | Reporting cadence and what the user receives (progress, risks, decisions). | §Reporting |

## Technical criteria: owned by Tech Skeptic (when active)

| ID | Type | Criterion | Typical evidence |
|---|---|---|---|
| T1 | R | Key technical assumptions are listed and each is verified (doc link) or has a proposed spike. | tech-assessment.md |
| T2 | R | External dependencies (APIs, SDKs, vendors) are checked: availability, pricing, limits, terms. | tech-assessment.md |
| T3 | R | Proposed architecture/stack fits the team, scale and budget; alternatives considered. | tech-assessment.md |
| T4 | C (personal data, auth, payments, integrations) | Security & data protection approach: auth, authorization, data storage, secrets, threat model summary. | tech-assessment.md §Security |
| T5 | R | Cost basis for infrastructure and third-party services is stated. | tech-assessment.md §Cost |
| T6 | R | Non-functional requirements: expected load, response times, availability, data volume. | product.md / tech-assessment.md |

## Handoff criteria: checked in the handoff phase

| ID | Type | Criterion |
|---|---|---|
| H1 | R | Every MVP story is covered by at least one dev prompt; no prompt is outside MVP without being marked. |
| H2 | R | Every prompt follows dev-prompt-format.md and can be executed without guessing. |
| H3 | R | Prompt order respects dependencies; parallelizable prompts are marked. |
| H4 | R | team.md recommends human roles, agent team and models, with justification tied to project risk. |
