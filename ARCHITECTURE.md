# Architecture

## Decision

Use one central repository as the source of truth for reusable deterministic and agentic GitHub workflows.

Keep deterministic acceptance separate from agentic reasoning.

## Problem context

The repository portfolio contains different languages, test systems, deployment targets, and governance rules. One identical CI/CD file cannot verify all repositories correctly.

The control plane must provide common policy without replacing repository-specific verification.

## Considered alternatives

### One identical workflow for every repository

Reject this option.

It would hide repository-specific contracts and would create false confidence when a generic check passes.

### Agent-controlled CI/CD

Reject this option.

A model can analyze evidence, but it cannot be the authority that accepts its own work or deploys production state.

### Shared control plane with repository profiles

Accept this option.

It centralizes reusable workflow definitions and policy. It preserves local deterministic gates where a repository needs them.

## Control-plane pipeline

```text
EVENT
  |
  v
DETERMINISTIC CI
  |
  +-- FAIL --> AGENTIC CI DOCTOR --> report or later bounded repair candidate
  |
  v
DETERMINISTIC ACCEPTANCE
  |
  v
MERGE GATE
  |
  v
DETERMINISTIC CD
  |
  v
STAGING
  |
  v
PRODUCTION AUTHORIZATION
  |
  v
PRODUCTION
  |
  v
POST-DEPLOY VERIFICATION
```

Parallel agentic workflows can review pull requests, detect documentation drift, and report repository health.

They cannot produce the acceptance decision.

## Target repository shape

The repository will grow to this shape as each capability is implemented:

```text
agentic-workflows/
├── AGENTS.md
├── ARCHITECTURE.md
├── README.md
├── aw.yml                         # add with the first valid installable package
├── .governance/
│   ├── authority.md
│   ├── execution.md
│   ├── verification.md
│   ├── security.md
│   ├── evidence.md
│   ├── releases.md
│   └── completion.md
├── .github/
│   ├── CODEOWNERS
│   ├── pull_request_template.md
│   ├── aw/
│   │   └── actions-lock.json      # compiler-managed after first agentic compile
│   └── workflows/
│       └── catalog-ci.yml         # deterministic validation of this catalog
├── workflows/
│   ├── ci-doctor.md
│   ├── pr-evidence-review.md
│   ├── documentation-drift.md
│   ├── repository-health.md
│   └── bounded-repair.md          # later autonomy phase
├── shared/
│   ├── agent-policy.md
│   ├── security-policy.md
│   └── evidence-policy.md
├── payload/
│   └── actions/
│       ├── ci-python.yml
│       ├── ci-node.yml
│       └── deploy-profile.yml
└── tests/
    ├── contracts/
    └── fixtures/
```

Do not create placeholder files only to make this tree exist. Add a path when an accepted increment needs that path.

## Distribution boundaries

Use top-level `workflows/` for installable agentic workflow sources.

Use `shared/` for reusable agentic components that consumers import by a pinned ref.

Use `payload/actions/` for inert deterministic workflow source files that the package manifest installs into a consuming repository.

Use `.github/workflows/` only for deterministic workflows that validate this central repository itself.

This separation prevents catalog payload workflows from executing in the catalog repository.

## Quality attributes

The design prioritizes these attributes:

- Reproducibility: consumers pin approved versions and compiled actions use immutable references.
- Auditability: acceptance evidence identifies the exact commit, source, lock file, and verifier result.
- Least privilege: agent jobs are read-only and external writes use safe outputs.
- Bounded autonomy: agentic workflows can propose actions but cannot merge or deploy production state.
- Evolvability: repository profiles can change without forcing one global implementation on every repository.

## Consequences

The control plane adds release management and compatibility work.

A source workflow and its generated lock file must stay synchronized.

Consumers do not receive a workflow change until they update to an approved version.

Repository-specific gates remain necessary when a shared profile cannot express the local contract.
