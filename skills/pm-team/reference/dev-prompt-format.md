# Dev prompt format

Each prompt is a self-contained task that the PAIASA DEV team (`/paiasa-dev:dev-team`) or a human developer can execute **without guessing**. It is written in the dev-prompt language from STATE.md (default English).

One prompt = one verifiable change. If it cannot be reviewed as a single pull request, split it.

## File naming

`.product/handoff/prompts/<NN>-<kebab-title>.md`, e.g. `03-booking-calendar.md`. `NN` follows the dependency order.

## Template

```markdown
---
id: P-03
title: Booking calendar for salon staff
mvp_story: US-04, US-05
depends_on: [P-01, P-02]
parallel_with: [P-04]
risk_flags: [architecture?, clarity?, performance?, novelty?, security?]   # keep only the flags that apply
size: S | M | L          # L must be justified; prefer splitting
suggested_agents: [implementer, test-engineer, ui-verifier, security-reviewer]
---

# Goal
<What the user gets from this task, 1–2 sentences.>

# Context
<Why we are doing this; link to MVP story and decisions (D-ids); what previous prompts built.>

# Requirements
1. <Precise, testable requirement>
2. ...

# Acceptance criteria
- AC1: Given <state>, when <action>, then <observable result>.
- AC2: ...
(Copied from the user story and made concrete. Every AC must be testable.)

# Technical constraints
- Stack / existing modules to use: <...>
- Security: <auth rules, data handling, secrets: "no secrets in code">
- Performance budget: <e.g. p95 < 300 ms for list endpoint with 10k records>
- Non-goals for the implementation approach: <e.g. no new infrastructure>

# Out of scope
- <What NOT to do in this task.>

# Data & interfaces
<Entities, fields, API contracts, events, or "define in this task and document">

# How to verify
1. <Test steps; what to run; what to show at the end (screenshot, test output, staging URL)>

# Assumptions & open questions
- [ASSUMPTION] <...>: if wrong, stop and ask PM team.
- Q: <question the developer must not guess>

# If you see a better approach
You may propose a different solution if it better meets the goal and acceptance criteria. Explain the trade-off in the PR description; do not silently change scope. The proposal goes back to the PM team's decision log.

# Definition of done
- All acceptance criteria covered by automated tests that pass.
- Reviews passed (code; plus security/architecture/performance if flagged).
- Evidence package produced (diff link, test results, screenshots, staging link).
```

## Index file

`.product/handoff/README.md`:

```markdown
# Handoff: <project>
Generated: <date>, from decisions up to D-0xx

## How to use
Give prompts to the DEV team in order: `/paiasa-dev:dev-team <path to prompt>` (or the whole folder).

## Order and parallelism
| # | Prompt | Depends on | Can run in parallel with | Risk flags |
|---|---|---|---|---|

## Project rules for the dev team
<Stack, conventions, environments, compliance notes: becomes CLAUDE.md content>

## Team recommendation
See team.md
```

## Executability check (Tech Skeptic, criterion H2)

A prompt fails if any of these is true:
- An acceptance criterion cannot be turned into a test.
- A required interface, entity or rule is referenced but not defined anywhere.
- It depends on a decision still open in decisions-for-you.md (then mark it blocked instead).
- It would take more than one reviewable PR.
- Security or data-handling rules are missing for a task that touches auth, payments or personal data.
