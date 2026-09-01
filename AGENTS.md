# AGENTS.md

## Scope & Role

- **Project Purpose:** Central control plane for reusable deterministic GitHub CI/CD and agentic workflow definitions.
- **Architecture:** Shared workflow catalog with deterministic acceptance separated from agentic reasoning and repository-specific verification.

## Environment & Tooling

- **Workflow Platform:** GitHub Actions and GitHub Agentic Workflows.
- **Agentic Workflow Tooling:** `gh aw` for supported workflow compilation, installation, and validation when an active contract requires it.
- **Primary Formats:** Markdown and YAML.
- **Package Manager:** None established for the current governance-only phase.
- **Testing / Verification:** Use only the deterministic checks and verifier selected by the active task contract.

## Development Tasks

- **Task Routing:** Read `CONTEXT.md` and select exactly one active task contract before substantive work.
- **Task Authority:** Follow the active task contract selected through `CONTEXT.md`.
- **Architecture Changes:** Read `ARCHITECTURE.md` when the active contract requires architecture context.
- **Validate Changes:** Run only the deterministic checks designated by the active task contract and `.governance/testing.md`.

Do not invent development commands, validators, package-manager operations, or implementation details that are not established by repository evidence or the active contract.

## Engineering Rules

Before any action that can generate or modify code, tests, schemas,
migrations, build logic, or harness logic, read the canonical
engineering-rules document from its authoritative location.

Do not generate or mutate code until the engineering-rules
Pre-Code Readiness Gate is satisfied.

- **Engineering Rules Authority:** Refer to `.governance/authority.md`.
- **Task Routing:** Refer to `CONTEXT.md`.

## Architecture & Guidelines

Do not guess implementation details. Read only the references admitted by the active task contract.

- Refer to `CONTEXT.md` for task routing.
- Refer to `.harness/contracts/` for task-specific execution envelopes.
- Refer to `ARCHITECTURE.md` for repository topology and control-plane boundaries.
- Refer to `.governance/authority.md` for authority and protected state transitions.
- Refer to `.governance/execution.md` for execution lifecycle, repair bounds, and stop conditions.
- Refer to `.governance/security.md` for least privilege, path authorization, secrets, and safe-output rules.
- Refer to `.governance/testing.md` for required deterministic checks.
- Refer to `.governance/verification.md` for proof, oracle, verifier, and exact-candidate requirements.
- Refer to `.governance/evidence.md` for evidence classification and provenance.
- Refer to `.governance/releases.md` for release and consumer-adoption rules.
- Refer to `.governance/completion.md` for terminal states and the Definition of Done.

## Completion

- Follow the active contract selected through `CONTEXT.md`.
- Verify the exact final candidate before completion.
- Any mutation after verification invalidates that verification.
- Report `PASS`, `FAIL`, or `BLOCKED`.
