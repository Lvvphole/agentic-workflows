# CONTEXT.md

## Purpose

This file routes repository tasks.

It determines:

- the task route;
- whether the task is code-capable;
- the applicable task contract.

Routing does not grant authority.

The selected task contract defines the authorized task envelope.

Do not load unrelated context.

## Entry

Before substantive work:

1. Read `AGENTS.md`.
2. Classify the task.
3. Select one task contract.
4. Read the inputs specified by that contract.

If the task cannot be classified deterministically, return `BLOCKED`.

## Routes

| Route | Use | Task Contract | Code-Capable |
| --- | --- | --- | --- |
| `READ_ONLY` | Inspection, diagnosis, evidence review, or review without mutation | `.harness/contracts/read-only.md` | No |
| `GOVERNANCE_BOOTSTRAP` | Establish or repair governance before baseline acceptance | `.harness/contracts/governance-bootstrap.md` | Conditional |
| `GOVERNANCE_ARCHITECTURE` | Change accepted governance structure or control boundaries | `.harness/contracts/governance-architecture.md` | Conditional |
| `MUTATION` | Authorized mutation without a more specific route | `.harness/contracts/mutation.md` | Conditional |
| `BUG_FIX` | Repair a verified behavioral defect | `.harness/contracts/bug-fix.md` | Yes |
| `REVIEW_REPAIR` | Address an accepted review finding | `.harness/contracts/review-repair.md` | Conditional |
| `DETERMINISTIC_CI_CD` | Change CI, CD, build, test, deployment, or deterministic gate logic | `.harness/contracts/deterministic-ci-cd.md` | Yes |
| `AGENTIC_WORKFLOW` | Change agent workflows, harnesses, hooks, middleware, or execution policy | `.harness/contracts/agentic-workflow.md` | Yes |
| `RELEASE_CONSUMER` | Create a release or change consumer adoption | `.harness/contracts/release-consumer.md` | Conditional |
| `COMPLETE_FAILURE` | Process a complete failure established by the active authority | `.harness/contracts/complete-failure.md` | Conditional |

Use the most specific applicable route.

## Code-Capable Tasks

A task is code-capable if it can create or change:

- code;
- tests;
- schemas;
- migrations;
- build logic;
- CI/CD logic;
- harness logic.

For a code-capable task, use the Engineering Rules route specified by the active task contract.

Do not mutate code until that route permits construction.

## Routing Invariants

- Routing does not grant authority.
- Select exactly one active task contract.
- Use the most specific applicable route.
- Load only context specified by the active contract.
- `CONTEXT.md` cannot enlarge the active contract.
- If required routing information is unavailable, return `BLOCKED`.
