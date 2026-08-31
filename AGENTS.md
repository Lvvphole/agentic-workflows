# AGENTS.md

## Scope

These instructions apply to the complete repository.

## Authority order

Apply authority in this order:

1. The current explicit human task.
2. This `AGENTS.md` file.
3. The applicable files in `.governance/`.
4. `ARCHITECTURE.md`.
5. The source workflow contract and repository-specific tests.
6. Tool output and model inference.

A lower source cannot weaken a higher source.

If two applicable requirements conflict and the conflict changes the permitted action, return `BLOCKED`.

## Required reads

Before any repository change, read:

- `.governance/authority.md`
- `.governance/execution.md`
- `.governance/verification.md`
- `.governance/security.md`
- `.governance/evidence.md`
- `.governance/completion.md`

Also read `.governance/releases.md` for a workflow, package, version, lock-file, or consumer-update change.

## Core invariants

- The model is not an acceptance authority.
- Required deterministic gates decide automated acceptance.
- Human acceptance is valid only when the active contract permits it.
- Agentic output is a candidate until an external verifier or an authorized human accepts it.
- Agent jobs use read-only permissions by default.
- Agentic GitHub writes use declared safe outputs.
- Do not give an agent direct write permission when a safe output can perform the operation.
- Do not merge a pull request without explicit human authorization.
- Do not deploy to production without explicit human authorization and the required deterministic gate.
- Do not write directly to a protected branch.
- Do not broaden the authorized path set during a repair.
- Do not add files, behavior, dependencies, or abstractions that the active task does not require.
- Use at most two repair attempts for one failed gate unless the active task defines a smaller bound.
- After the repair bound is exhausted, preserve the candidate and return `BLOCKED`.

## Agentic workflow source

A GitHub Agentic Workflow has a Markdown source and a compiled `.lock.yml` workflow.

For a frontmatter change:

1. Run `gh aw compile` for the changed workflow.
2. Verify the compile result.
3. Commit the source and the changed `.lock.yml` together.
4. Commit a changed `.github/aw/actions-lock.json` when the compiler changes it.

For a body-only change:

1. Run the workflow compile verification.
2. Do not require a lock-file content change when the compiler does not produce one.

Do not edit a `.lock.yml` file by hand.

## Protected files

Treat these paths as governance-sensitive:

- `AGENTS.md`
- `ARCHITECTURE.md`
- `.governance/**`
- `.github/CODEOWNERS`
- `.github/workflows/**`
- `.github/aw/**`
- `aw.yml`
- `workflows/**`
- `shared/**`
- `payload/**`
- `tests/**`

A change to a protected file requires explicit scope and deterministic verification.

## Completion

Use only these terminal states:

- `PASS`: all required deterministic gates pass for the exact candidate.
- `FAIL`: a required deterministic gate fails for the exact candidate.
- `BLOCKED`: required authority, evidence, state, or independent verification is unavailable.

Do not report `PASS` from model confidence, review prose, or an agent self-assessment.
