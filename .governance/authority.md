# Authority

## Purpose

Define who or what may authorize work, acceptance, and repository state transitions.

## Human Authority

An explicit human instruction defines permitted task scope.

A model may request authority. A model cannot grant authority to itself.

Silence, tool access, memory, prior work, repository visibility, or verifier output does not create new human authority.

## Task Contract Admission

`CONTEXT.md` selects the active task contract. Routing does not grant authority.

A contract is admissible only when its required identity, scope, inputs, predicates, verifier, and stop conditions are complete and valid.

An invalid or unresolved required contract field returns `BLOCKED`.

A task contract may narrow repository governance. It cannot weaken it or enlarge explicit human scope.

## Engineering Rules Authority

For code-capable work, the canonical engineering-rules authority is the content-addressed `engineering-rules` artifact approved for this repository.

Expected canonical document identity:

- logical location: `engineering-rules/SKILL.md`
- SHA-256: `deb95b212e0d3fae948e6cd0b9b932ede58cbaeef0170ccc8257b7a80a117793`

Expected deterministic gate identity:

- logical location: `engineering-rules/scripts/check.py`
- SHA-256: `0c8ba9a02dd5dfc99660ce12f2503727df595fd89a97ec73d91a8d6afe3b7822`

Before code-capable mutation, the active task contract must resolve the canonical document, verify the required identity when available, read it, and satisfy its Pre-Code Readiness Gate.

If the canonical authority is missing, mismatched, or unreadable, return `BLOCKED`. Do not substitute a reconstructed or unverified rules document.

## Acceptance Authority

A deterministic verifier is the default acceptance authority for an automated gate.

An authorized human may accept a candidate when the active contract permits human acceptance.

The proposer, executor, coding agent, or agentic workflow cannot accept its own output.

A test result is evidence. It becomes acceptance evidence only through the verifier selected by the active contract.

## Remote Mutation Authority

Any remote repository mutation requires explicit task authority for that operation. A verifier result never grants remote-write authority.

Examples include closing or reopening a pull request, creating or pushing a branch, opening a pull request, changing pull-request metadata, requesting reviews, or posting a state-changing safe output.

## Protected State Transitions

These transitions require explicit human authority for the transition itself:

- merge a pull request;
- push directly to a protected branch;
- create or rotate a credential;
- change branch protection or a ruleset;
- publish a release;
- promote a deployment to production;
- change organization-wide agentic workflow policy.

Verification success does not supply this authority.

## Delegation

Delegation may narrow authority. Delegation cannot expand authority.

Give a called workflow, sub-agent, or tool only the authority required for its declared operation.

## Evidence Classes

- `VERIFIED`: an authoritative deterministic verifier or authorized human confirmed the fact within its jurisdiction.
- `OBSERVED`: a repository or tool read returned the fact but acceptance authority has not confirmed it.
- `INFERRED`: reasoning derived the fact from other information.

Only `VERIFIED` evidence may satisfy an acceptance gate. `OBSERVED` and `INFERRED` material may select the next read, test, or proposal but cannot cause an acceptance state transition.
