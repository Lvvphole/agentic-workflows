# Authority

## Purpose

Define who can authorize a state change and what evidence can support acceptance.

## Human authority

An explicit human instruction defines the permitted task scope.

A model can request authority.

A model cannot grant authority to itself.

Silence, tool access, memory, or a prior task does not grant new authority.

## Contract admission

A contract gives no authority until the complete contract passes its authoritative schema.

Validate all required fields, values, budgets, paths, predicates, identifiers, and task types.

Partial, malformed, unknown, or invalid contract state gives zero authority.

Return `BLOCKED` when complete contract validation fails.

Mandatory predicates are admission requirements, not optional enforcement switches.

A required predicate must equal `true` when the active task class requires that predicate.

A missing, false, null, malformed, or unknown required predicate invalidates the contract.

Do not interpret a false mandatory predicate as permission to skip an invariant.

## Acceptance authority

A deterministic verifier is the default acceptance authority for an automated gate.

An authorized human can accept a candidate when the active contract permits human acceptance.

An agentic workflow cannot accept its own output.

## State-transition authority

The following actions are protected state transitions:

- Merge a pull request.
- Push directly to a protected branch.
- Create or rotate a credential.
- Change branch protection or a ruleset.
- Publish a release.
- Promote a deployment to production.
- Change an organization-wide agentic workflow policy.

Do not perform a protected state transition without explicit human authority for that transition.

## Delegation

Delegation can narrow authority.

Delegation cannot expand authority.

Give a called workflow, sub-agent, or tool only the authority required for its declared operation.

## Evidence classes

Use these evidence classes:

- `VERIFIED`: An authoritative deterministic check or authorized human confirmed the fact.
- `OBSERVED`: A tool or repository read returned the fact, but no acceptance authority confirmed it.
- `INFERRED`: Reasoning derived the fact from other information.

Only `VERIFIED` evidence can satisfy an acceptance gate.

`OBSERVED` and `INFERRED` information can select the next read or test.

They cannot cause an acceptance state transition by themselves.
