# COMPLETE_FAILURE Task Contract

## Purpose

Process a complete failure without fix-forward and convert frozen failure evidence into successor acceptance criteria.

## Inputs

### Governing

- `.governance/authority.md`
- `.governance/execution.md`
- `.governance/security.md`
- `.governance/testing.md`
- `.governance/verification.md`
- `.governance/evidence.md`
- `.governance/completion.md`

### Reference

- `ARCHITECTURE.md`
- failed task contract
- accepted predecessor architecture

### Working

- complete-failure determination;
- failed base and head identity;
- failed gates and findings;
- accepted base identity.

## Engineering Rules

- **Applicability:** No for failure-processing steps.
- Before any code-capable successor construction, end `COMPLETE_FAILURE` and route the successor through `CONTEXT.md` to exactly one new active task contract.
- The successor task contract owns Engineering Rules authority resolution, identity verification, and the Pre-Code Readiness Gate.

## Process

1. Confirm complete failure was declared by the active acceptance authority or explicit human decision.
2. Stop mutation of the failed candidate.
3. Freeze failure evidence before successor construction.
4. Require explicit human authority before any remote close, branch, push, or pull-request transition.
5. Redesign from the last accepted base and frozen evidence.
6. Before any successor mutation, code-capable construction, or verification, end `COMPLETE_FAILURE` and route the successor through `CONTEXT.md` to exactly one new active task contract.
7. Pass the frozen failure corpus and successor acceptance criteria as admitted working inputs. The successor task contract owns Engineering Rules readiness, construction, testing, verification, evidence, completion, and any separately authorized publication.

## Outputs

- immutable failure corpus;
- successor acceptance criteria;
- successor handoff for `CONTEXT.md` routing.

## Verifier

A deterministic verifier designated by this contract or its authorized task instance verifies the frozen failure corpus and successor handoff before `COMPLETE_FAILURE` completes.

After `CONTEXT.md` activates the successor task contract, that active contract selects the verifier for successor construction and acceptance.

The failed predecessor remains `FAIL` and cannot be retroactively accepted.

## Stop Conditions

- required authority or admitted input is missing;
- scope expansion is required but not authorized;
- the required verifier is unavailable;
- unexpected repository drift occurs;
- a required governance or contract condition returns `BLOCKED`.

The contract may narrow repository governance. It cannot weaken governance or enlarge explicit human authority.
