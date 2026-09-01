# Architecture

## Decision

Use one central repository as the source of truth for reusable deterministic and agentic GitHub workflows.

Separate coding-agent governance, task/context routing, agent runtime policy, and deterministic enforcement.

Keep deterministic acceptance separate from agentic reasoning.

## Problem context

The repository portfolio contains different languages, test systems, deployment targets, and governance rules. One identical CI/CD file cannot verify all repositories correctly.

The control plane must provide common policy without replacing repository-specific verification.

Coding-agent instructions also serve a different purpose from workflow runtime instructions. Repository governance must not be confused with task routing or executable enforcement.

## Control surfaces

### Coding-agent governance

Root `AGENTS.md` is the repository-wide governance surface for coding agents.

Codex reads `AGENTS.md` directly.

Root `CLAUDE.md` contains only `@AGENTS.md` so Claude Code receives the same governance rather than a second policy copy.

`AGENTS.md` defines universal repository rules. It does not classify tasks or select working context.

A nested `AGENTS.md`, if later required, may specialize compatible rules for its subtree without expanding human authority.

### Task and context routing

Root `CONTEXT.md` is the workspace task router.

It classifies the explicit task and selects the smallest sufficient context route.

When an accepted stage or subsystem later requires a nested `CONTEXT.md`, the root router must select that scope before the nested context is loaded.

Use this context model:

```text
CODING AGENT ENTRY
        |
        v
    AGENTS.md
 universal governance
        |
        v
    CONTEXT.md
 workspace task router
        |
        v
active task or stage contract
        |
        v
routed governance / architecture / references
        |
        v
working evidence and candidate artifacts
```

Routing selects information and process. Routing does not grant authority or decide acceptance.

### Agent runtime policy

Repository coding-agent governance is not the runtime policy for installed agentic workflows.

Agentic workflow runtime behavior is defined by its workflow source, capability frontmatter, imported shared policy, compiled execution contract, and platform-enforced permission boundaries.

Do not assume a runtime agent obeys `AGENTS.md` merely because the workflow source lives in this repository.

### Deterministic enforcement

Use tools, middleware, hooks, GitHub permissions, safe outputs, CI gates, branch or environment protection, and deterministic verifiers for constraints that require mechanical enforcement.

Do not rely on prompt prose alone when a recurring failure requires an execution-time interlock.

When evidence shows that a rule is enforced at the wrong component level, redesign at the smallest stronger component that directly controls the failure surface.

Keep verifier, acceptance oracle, and protected-state authority outside the model's self-modifiable surface.

## Harness engineering principle

Treat the coding-agent or workflow harness as a set of separable components rather than one large prompt.

A recurring failure should be mapped to the component that can directly observe or control it, such as:

- repository governance;
- task/context routing;
- workflow instructions;
- tool description;
- tool implementation;
- middleware or hook;
- reusable skill;
- bounded memory;
- platform permission or safe output;
- deterministic verifier.

Every harness change must remain attributable to exact evidence and exact candidate identity.

Do not keep adding prose when a tool, middleware, hook, or deterministic gate is the correct enforcement surface.

## Considered alternatives

### One identical workflow for every repository

Reject this option.

It would hide repository-specific contracts and would create false confidence when a generic check passes.

### Agent-controlled CI/CD

Reject this option.

A model can analyze evidence, but it cannot be the authority that accepts its own work or deploys production state.

### AGENTS.md as task router

Reject this option.

`AGENTS.md` governs coding-agent behavior. Root `CONTEXT.md` owns workspace task and context routing.

### Duplicate Claude and Codex governance

Reject this option.

`CLAUDE.md` points to the same root `AGENTS.md` used by Codex so governance does not drift across coding agents.

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

## Decision and evidence flow

Use this state-transition model:

```text
human task and authority
        |
        v
AGENTS.md governance
        |
        v
CONTEXT.md route
        |
        v
bounded observation and reasoning
        |
        v
candidate or proposed action
        |
        v
deterministic verification / policy enforcement
        |
   PASS | FAIL | BLOCKED
        |
        v
authorized state transition, if separately permitted
```

`OBSERVED` and `INFERRED` information may guide the next read, test, or proposal.

Only the required `VERIFIED` evidence may satisfy an acceptance gate.

A protected state transition still requires its own authority even after verification passes.

## Target repository shape

The repository will grow to this shape as each capability is implemented:

```text
agentic-workflows/
├── AGENTS.md                      # coding-agent governance
├── CLAUDE.md                      # @AGENTS.md only
├── CONTEXT.md                     # workspace task/context router
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

Do not add stage directories, nested `CONTEXT.md` files, tools, middleware, hooks, or other harness components until verified evidence and an accepted increment require them.

## Distribution boundaries

Use top-level `workflows/` for installable agentic workflow sources.

Use `shared/` for reusable agentic runtime components that consumers import by a pinned ref.

Use `payload/actions/` for inert deterministic workflow source files that the package manifest installs into a consuming repository.

Use `.github/workflows/` only for deterministic workflows that validate this central repository itself.

This separation prevents catalog payload workflows from executing in the catalog repository.

## Quality attributes

The design prioritizes these attributes:

- Reproducibility: consumers pin approved versions and compiled actions use immutable references.
- Auditability: acceptance evidence identifies the exact commit, source, lock file, and verifier result.
- Least privilege: agent jobs are read-only and external writes use safe outputs.
- Bounded autonomy: agentic workflows can propose actions but cannot merge or deploy production state.
- Context economy: routing loads only the context required for the active task.
- Component observability: governance, routing, runtime policy, enforcement, and verification remain distinct surfaces.
- Decision observability: consequential changes remain tied to evidence, predicted purpose, exact candidate identity, and verifier outcomes.
- Evolvability: repository profiles can change without forcing one global implementation on every repository.

## Consequences

The control plane adds release management and compatibility work.

A source workflow and its generated lock file must stay synchronized.

Consumers do not receive a workflow change until they update to an approved version.

Repository-specific gates remain necessary when a shared profile cannot express the local contract.

A governance statement may still require a stronger executable control when observed failures show that prose is insufficient.
