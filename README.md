# Agentic Workflows

This repository is the central control plane for reusable GitHub CI/CD and agentic workflow definitions.

The repository has one primary rule:

> Deterministic verification controls acceptance and deployment. Agentic workflows can analyze evidence and propose actions. They cannot make an acceptance decision.

## Pipeline

```text
pull request or push
        |
        v
DETERMINISTIC CI
build | test | lint | security | repository-specific gates
        |
        v
ACCEPTANCE GATE
        |
        v
MERGE GATE
        |
        v
DETERMINISTIC CD
        |
        v
STAGING DEPLOYMENT
        |
        v
PRODUCTION AUTHORIZATION
        |
        v
PRODUCTION DEPLOYMENT
        |
        v
POST-DEPLOY VERIFICATION
```

Agentic workflows run beside this pipeline. They do not replace it.

Initial agentic roles are:

- CI Doctor: analyze a deterministic CI failure and produce a report.
- PR Evidence Reviewer: identify missing evidence, scope violations, or unsupported claims.
- Documentation Drift: identify documentation that a merged change made incorrect.
- Repository Health: produce a scheduled repository health report.
- Bounded Repair: produce one repair candidate only after a later authorization phase.

## Distribution model

This repository will publish versioned workflow definitions for other repositories.

Agentic workflow source files will use GitHub Agentic Workflows Markdown. Consuming repositories will install a released workflow with `gh aw add` and will pin an approved version.

Shared agentic components will use `imports:`. Production consumers must use an exact release tag or commit SHA. They must not consume an unreviewed branch.

Compiled `.lock.yml` files and `.github/aw/actions-lock.json` are verification artifacts. Do not edit generated lock files by hand.

## Governance

Read `AGENTS.md` before you change this repository.

The governing documents are in `.governance/`:

- `authority.md`: authority and protected state transitions.
- `execution.md`: pipeline stages, agentic roles, bounds, and stop conditions.
- `verification.md`: deterministic acceptance rules.
- `security.md`: least privilege, safe outputs, secrets, and network rules.
- `evidence.md`: required provenance and run evidence.
- `releases.md`: package versioning and consumer update rules.
- `completion.md`: PASS, FAIL, BLOCKED, and completion conditions.

`ARCHITECTURE.md` defines the target repository shape and the control-plane decision.

## Current phase

This baseline contains governance only. It does not contain an installable workflow package yet.

Do not add `aw.yml` until at least one installable workflow exists and package validation can pass.
