# Architecture

## Decision

Use one central repository as the source of truth for reusable deterministic and agentic GitHub workflows.

Separate repository orientation, task routing, task authority, stable governance, engineering readiness, implementation, testing, verification, evidence, and completion.

Keep deterministic acceptance separate from agentic reasoning.

## Canonical Repository Lifecycle

```text
AGENTS
   ↓
CONTEXT
   ↓
TASK CONTRACT
   ↓
GOVERNANCE
   ↓
ENGINEERING-RULES
   ↓
PRE-CODE READINESS
   ↓
BUILD / REPAIR
   ↓
TEST
   ↓
VERIFY
   ↓
EVIDENCE
   ↓
COMPLETE
```

The responsibilities are distinct:

- `AGENTS.md`: repository map and universal coding-agent obligations.
- `CONTEXT.md`: Layer-1 task router only.
- `.harness/contracts/<task>.md`: Layer-2 task envelope, admitted inputs, required process, outputs, and verifier.
- `.governance/*`: stable Layer-3 governing rules.
- canonical engineering rules: construction readiness for code-capable work.
- `.governance/testing.md`: checks that must run.
- `.governance/verification.md`: what counts as proof and which verifier decides.
- `.governance/evidence.md`: provenance and exact-candidate binding.
- `.governance/completion.md`: terminal-state rules.

Routing does not grant authority. A task contract cannot weaken governance. Testing is not verification. Verification is not completion.

## Control Surfaces

### Coding-agent governance

Root `AGENTS.md` is the repository operating map for coding agents. It does not classify tasks or duplicate detailed downstream policy.

Root `CLAUDE.md` contains only `@AGENTS.md`.

### Task routing

Root `CONTEXT.md` selects exactly one most-specific task route and task contract. It does not enumerate the downstream inputs owned by the selected contract.

### Task contracts

Each task contract uses the same Layer-2 shape:

```text
Inputs
  ↓
Process
  ↓
Outputs
```

The contract freezes task-specific scope, prohibitions, required evidence, engineering-rules applicability, deterministic checks, verifier, and stop conditions.

### Engineering readiness

For code-capable work, the active task contract resolves the canonical engineering-rules authority through `.governance/authority.md` and requires its Pre-Code Readiness Gate before mutation.

### Deterministic enforcement

Use tests, parsers, schema checks, hooks, middleware, platform permissions, safe outputs, CI gates, and verifiers when mechanical enforcement is required. Do not rely on prompt prose where an executable interlock controls the failure surface more directly.

Keep verifier, acceptance oracle, and protected-state authority outside the model's self-acceptance surface.

## Target Repository Shape

```text
agentic-workflows/
├── AGENTS.md
├── CLAUDE.md
├── CONTEXT.md
├── ARCHITECTURE.md
├── .harness/
│   └── contracts/
│       ├── read-only.md
│       ├── governance-bootstrap.md
│       ├── governance-architecture.md
│       ├── mutation.md
│       ├── bug-fix.md
│       ├── review-repair.md
│       ├── deterministic-ci-cd.md
│       ├── agentic-workflow.md
│       ├── release-consumer.md
│       └── complete-failure.md
├── .governance/
│   ├── authority.md
│   ├── execution.md
│   ├── security.md
│   ├── testing.md
│   ├── verification.md
│   ├── evidence.md
│   ├── releases.md
│   └── completion.md
└── <runtime and workflow implementation added only by accepted increments>
```

Do not create placeholder runtime files only to make a future tree exist.

## Control-Plane Invariants

- Agentic workflows may analyze evidence and propose actions but cannot accept their own output.
- Deterministic verification controls automated acceptance.
- Protected transitions require human authority even after verification succeeds.
- Candidate identity changes invalidate prior verification.
- Repository-specific consumer gates remain authoritative for consumer acceptance.
- Complete failure stops fix-forward on the failed candidate and preserves the failure as successor evidence.
