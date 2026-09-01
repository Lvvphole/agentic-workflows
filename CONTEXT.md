# CONTEXT.md

## Purpose

Use this file as the workspace task and context router.

Classify the current task before loading deeper repository context.

Load only the smallest sufficient context for the selected route.

This file does not grant authority. `AGENTS.md` governs coding-agent behavior, and the routed authoritative sources govern their own jurisdictions.

## Context model

- Layer 0: coding-agent entry instructions load repository governance.
- Layer 1: this root `CONTEXT.md` selects the workspace task route.
- Layer 2: an active task, workflow, or stage `CONTEXT.md` defines stage-specific inputs, process, outputs, and bounds when one exists.
- Layer 3: routed governance, architecture, contracts, and references provide persistent authoritative context.
- Layer 4: diffs, findings, run logs, candidate artifacts, and other per-run material provide working evidence.

Treat Layer 3 according to its declared authority.

Treat Layer 4 as working input unless an applicable verifier promotes it to `VERIFIED` evidence.

## Routing procedure

1. Read the explicit human task.
2. Inspect only enough current repository state to classify the task.
3. Select exactly one primary route below.
4. Add another route only when the task necessarily crosses jurisdictions.
5. Read only the sources named by the selected route and any nested `CONTEXT.md` that route explicitly admits.
6. Do not preload unrelated governance, references, histories, or working artifacts.
7. Return `BLOCKED` when the route, authority, or required context cannot be resolved without guessing.

## Routes

| Route | Use when | Load |
| --- | --- | --- |
| `READ_ONLY` | Inspect, diagnose, scout, explain, or gather evidence without repository mutation. | `.governance/authority.md`, `.governance/evidence.md`, and only the repository artifacts needed to answer the task. |
| `MUTATION` | Change any repository artifact when no more specific route applies. | `.governance/authority.md`, `.governance/execution.md`, `.governance/security.md`, `.governance/verification.md`, `.governance/evidence.md`, `.governance/completion.md`, the active task contract, and affected artifacts. |
| `BUG_FIX` | Correct a verified defect in existing behavior. | `MUTATION`, the exact defect evidence, the affected behavioral contract, the required regression oracle, and predecessor evidence. |
| `REVIEW_REPAIR` | Repair one accepted review finding. | `MUTATION`, the exact accepted finding, predecessor candidate evidence, and the active repair envelope. |
| `DETERMINISTIC_CI_CD` | Change deterministic CI, CD, deployment, build, test, security, or verification behavior. | `MUTATION`, `ARCHITECTURE.md`, the active deterministic pipeline contract, and affected deterministic tests. |
| `AGENTIC_WORKFLOW` | Change an agentic workflow, runtime policy, compiled workflow contract, or agentic acceptance case. | `MUTATION`, `ARCHITECTURE.md`, `.governance/releases.md`, the active workflow contract, and its acceptance cases. |
| `RELEASE_CONSUMER` | Publish a catalog version or update a consuming repository to a catalog version. | `.governance/authority.md`, `.governance/releases.md`, `.governance/security.md`, `.governance/verification.md`, `.governance/evidence.md`, and the consumer acceptance contract. |
| `GOVERNANCE_ARCHITECTURE` | Change coding-agent governance, context routing, authority, architecture, or protected contracts. | `.governance/authority.md`, the affected governing source, `.governance/verification.md`, `.governance/evidence.md`, and applicable architecture. |
| `COMPLETE_FAILURE` | An authoritative verifier or explicit human decision declares a mutation a complete failure. | `MUTATION`, `ARCHITECTURE.md`, the failed candidate identity, frozen failure evidence, predecessor acceptance evidence, and the redesign contract. |

## Nested context

When a routed stage or subsystem contains its own `CONTEXT.md`, read it only after the root route selects that stage or subsystem.

A nested `CONTEXT.md` may narrow inputs, process, outputs, and bounds for its scope.

A nested `CONTEXT.md` cannot expand human authority or weaken repository governance.

Do not create stage directories or nested context files until an accepted increment requires them.

## Route boundaries

Routing selects context. It does not decide acceptance.

A route cannot expand explicit human scope.

A route cannot turn `OBSERVED` or `INFERRED` material into `VERIFIED` evidence.

A route cannot authorize merge, release, production deployment, credential changes, branch-protection changes, or other protected state transitions.

Use `PASS`, `FAIL`, and `BLOCKED` only under the applicable acceptance and completion rules.
