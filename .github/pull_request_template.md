## Scope

Describe the authorized change and list the changed paths.

## Contract

State the observable behavior or governance requirement that this pull request changes.

## Candidate identity

- Head commit SHA:
- Workflow source SHA-256, when applicable:
- Lock-file SHA-256, when applicable:
- `gh aw` version, when applicable:

## Deterministic verification

List each required gate and its result.

- [ ] Required tests pass.
- [ ] Required workflow compilation passes.
- [ ] Generated lock-file changes were reviewed.
- [ ] Required security checks pass.

## Agentic behavior

If this pull request changes an agentic workflow, state:

- Trigger.
- Read permissions.
- Safe outputs.
- Output limits.
- Network allowlist.
- Acceptance cases.

## Protected state transitions

- [ ] This pull request does not merge itself.
- [ ] This pull request does not authorize production deployment.
- [ ] Any protected state transition has separate explicit human authority.

## Evidence

Link or attach the deterministic verification evidence for this exact candidate.
