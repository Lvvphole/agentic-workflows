# Authority

## Purpose

Define who can authorize a state change and which evidence can support acceptance.

## Human authority

An explicit human instruction defines the permitted task scope.

A model can request authority. A model cannot grant authority to itself.

Silence, tool access, repository access, memory, or a prior task does not grant new authority.

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

Delegation can narrow authority. Delegation cannot expand authority.

A called workflow, sub-agent, or tool receives only the minimum authority required for its declared operation.

## Evidence classes

Use these evidence classes:

- `VERIFIED`: produced by an authoritative deterministic check or confirmed by an authorized human.
- `OBSERVED`: returned by a tool or repository read but not yet accepted as a governing fact.
- `INFERRED`: derived by reasoning from other information.

Only `VERIFIED` evidence can satisfy an acceptance gate.

`OBSERVED` and `INFERRED` information can select the next read or test. They cannot cause an acceptance state transition by themselves.
