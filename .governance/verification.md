# Verification

## Purpose

Define the acceptance contract for deterministic CI/CD and workflow catalog changes.

## Acceptance invariant

The verifier decides PASS or FAIL.

The model does not decide PASS or FAIL.

## Candidate identity

Bind verification to the exact candidate.

Record at least:

- Repository.
- Commit SHA.
- Changed path set.
- Workflow source SHA-256 when an agentic workflow source changed.
- Compiled `.lock.yml` SHA-256 when a lock file exists.
- `.github/aw/actions-lock.json` SHA-256 when that file is applicable.
- Verifier version or command identity.

If candidate identity changes after verification, the prior result does not accept the new candidate.

## Required gate properties

A deterministic gate must be repeatable for the same declared software, toolchain, and controlled inputs.

A deterministic gate must contain a meaningful oracle that can fail when the target contract is violated.

Do not use assertion-free, tautological, or unrelated checks as acceptance evidence.

Do not use coverage percentage as proof of correctness.

Use behavior-specific tests for the required contract.

## Agentic workflow verification

For a new or changed agentic workflow, verify the source contract and the compiled execution contract.

For a frontmatter change:

1. Compile the workflow with the approved `gh aw` version.
2. Require compile success.
3. Review the generated `.lock.yml` diff.
4. Verify that generated action references are immutable.
5. Verify that permissions and safe outputs match the source contract.

For a body-only change:

1. Run compile verification.
2. Verify the instruction change against the workflow acceptance cases.

Do not accept a workflow only because it compiles.

## Independent verification unavailable

When required independent verification is unavailable:

- Return `BLOCKED`.
- Preserve the candidate.
- Report that a candidate exists but is not accepted.
- Use a deterministic local gate only when the governing contract designates that gate as an acceptance authority.
- Request human authorization before substituting a different verifier.
