---
name: engineering-rules
description: Apply the canonical 53-rule engineering standard as an ordered lifecycle. For code-producing work, capture and SHA-bind the exact authoritative task bytes, then establish and content-bind a candidate Construction Contract before construction and run deterministic code gates. For read-only audits, report evidence without mutation. Use this skill for code changes, repairs, refactoring, tests, architecture boundaries, agent harnesses, and code review.
---

# Engineering Rules

The 53 rules below are the standard. This skill has two modes: Authoring and Audit. Authoring uses an ordered lifecycle before code production. Audit is read-only unless the task gives authority to repair. Authoring binds the Construction Contract to immutable authoritative task bytes. A `FROZEN` Construction Contract is a content-bound candidate for construction. It is not accepted work. If a blocking item remains unresolved, return the `DRAFT` contract and no code.

## Routing contract

This skill cannot guarantee its own loading. The repository-level coding governance (AGENTS.md, CLAUDE.md, or equivalent) must contain this routing obligation:

> Before any action that can generate or modify code, tests, schemas,
> migrations, build logic, or harness logic, read the canonical
> engineering-rules document from its authoritative location.
>
> Do not generate or mutate code until the engineering-rules
> Pre-Code Readiness Gate is satisfied.

Without that upstream route, an agent can begin coding before it knows this skill exists.

## Two modes

**Authoring** — you are writing or changing code. Authoring starts with engineering preparation, not code generation. You must establish the problem, goal, requirements, Definition of Done, and design before producing code. The workflow below enforces this order.

**Audit** — you are handed existing code, a diff, or a pull request for review. Inspect and report evidence without mutation. If the task authorizes repair, use the Authoring workflow before the first code change.

## Authoring workflow

Authoring is an ordered lifecycle. Do not skip stages or begin code generation before the Pre-Code Readiness Gate is satisfied.

### 1. Capture authority and inspect current state

Before you draft a problem statement or requirement, capture the authoritative task verbatim as an immutable working artifact. If the task is already an accessible immutable artifact, use its exact bytes. Otherwise, copy the exact task content exposed by the environment into a permitted artifact as UTF-8 without rewriting, trimming, normalizing, summarizing, or changing quotation or Markdown syntax. Record the artifact path, its original source locator, and the SHA-256 of its exact bytes.

Do not edit, replace, rename, or repin the captured source artifact. A new or amended task requires a new source artifact and a successor contract. Do not present reconstructed or normalized task text as the authoritative prompt. A quotation in a contract or final report is not a substitute for the captured source artifact. If the environment cannot expose the exact task content or no permitted location can hold an immutable capture, return `BLOCKED` and produce no contract candidate for freezing and no code.

Then read the actual artifacts. Governing instructions, current implementation, the tests that cover it, the interfaces it crosses. Never reason from a snippet or from memory of how the codebase probably looks (AE-001). Re-read each applicable governing source from its authoritative location before the first mutation (AE-010).

### 2. Determine scope

Which language overlays apply. Whether TDD or XP profiles are active. Whether agentic artifacts are in play. `[CONDITIONAL]` rules only fire when their condition actually exists — do not manufacture applicability.

### 3. Establish the Construction Contract

Before code generation, produce a **Construction Contract** as an inspectable Layer 4 working artifact. Use the exact artifact path set by the governing task or stage contract. If no path is set, use a permitted session workspace outside the repository. Do not add a repository file unless the task or repository governance permits it. If no permitted artifact location exists, return `BLOCKED`, include the `DRAFT` contract content, and produce no code.

The file must contain a header block and eight numbered sections:

**Header block:**
```
contract-id: <task-slug or ticket identifier>
status: DRAFT | READY | FROZEN
authority-source-path: <immutable artifact or externally captured source>
authority-source-sha256: <64 lowercase hexadecimal characters>
predecessor-contract-sha256: NONE | <lowercase SHA-256 of the frozen predecessor>
```

| Status | Meaning | Code permitted |
| --- | --- | --- |
| `DRAFT` | One or more readiness items are unresolved. | No |
| `READY` | The proposer found no unresolved readiness item. Required approvals can still be pending. | No |
| `FROZEN` | Applicable approvals exist and the exact candidate bytes have a recorded SHA-256. | Yes, after an identity match |

**Sections:**

1. **Authority and source binding.** Identify the authorized task, the original source locator, the content-bound task artifact from the header, separately applicable governing sources, repository state, and applicable interfaces. Do not reproduce a modified task and label it as the source.
2. **Problem definition.** State the observed current condition, required condition, gap, affected behavior, and supporting evidence. Do not put the proposed solution in the problem statement.
3. **Goal.** State the observable outcome the change must achieve. Keep the goal implementation-neutral unless the authority constrains implementation.
4. **Scope and non-goals.** Identify what may change and what must remain unchanged.
5. **System requirements.** Derive each obligation from either the content-bound task source or a separately identified governing source (REQ-001). Give each requirement an identifier, exact source reference, observable behavior, failure behavior when applicable, and acceptance path (REQ-003, REQ-004). Do not complete an omission in the task by inference. The requirement set must be internally consistent and sufficiently complete (REQ-006).
6. **Definition of Done.** Define the evidence that an independent completion authority will use. Do this before implementation.
7. **Design.** Define the smallest sufficient structure and logic (SC-002). Cover ownership, module boundaries, interfaces, data flow, control flow, state transitions, invariants, failure semantics, and affected boundaries. Compare alternatives when the choice is consequential (AD-001).
8. **Implementation plan.** Map requirements to bounded implementation increments, affected files, and verification.

### 4. Pre-Code Readiness Gate

Do not generate code while any of the following remains true:
- The authoritative task artifact or its recorded SHA-256 is missing.
- The authoritative task bytes do not match the identity recorded in the contract header.
- An authoritative requirement is unresolved (REQ-006).
- An acceptance criterion has no objective verification path (REQ-004).
- A consequential design decision has not been made (AD-001).
- A blocking fact needed for correct implementation is unknown.

If any item above remains true, set the contract status to `DRAFT`. Mark each unresolved item with `[UNRESOLVED: <what is missing>]` in the applicable section. Stop and produce no code.

When all items are resolved, set the contract status to `READY`. `READY` is the proposer's readiness claim. It is not acceptance or permission that overrides governing authority.

### 5. Freeze the Construction Contract

Apply all required upstream approvals before the transition to `FROZEN`. If an approval is required but unavailable, return `BLOCKED` and produce no code.

When the contract is `READY`, bind the source and freeze the exact contract candidate bytes:

1. Recompute the SHA-256 of the authoritative task artifact.
2. Continue only when it matches `authority-source-sha256` in the contract header.
3. Set the status to `FROZEN` and finish all contract edits.
4. Compute the SHA-256 of the exact contract file bytes.
5. Record the authority-source path and SHA-256 and the contract path and SHA-256 for the report.
6. Immediately before the first code mutation, recompute both SHA-256 values.
7. Continue only when both recomputed values match the recorded values.

`FROZEN` identifies the candidate used for construction. It does not mean that the proposer accepted its own requirements, design, code, or completion claim (AE-002). Do not edit, replace, rename, or repin a `FROZEN` contract during construction.

Freeze the problem contract, not an unproven diagnosis. For a bug, the failure and required behavior can be frozen. A suspected root cause must remain falsifiable until evidence establishes it.

If the authoritative task identity changes before freezing or construction, stop. Do not repin the source identity or rewrite the task capture to match the contract. Preserve any frozen predecessor unchanged. Create a successor `DRAFT` only in an authorized artifact location and derive it from the newly authorized source identity.

If implementation evidence invalidates the contract or design, stop construction. Preserve the frozen contract and its recorded SHA-256 unchanged. Create a successor `DRAFT` only in an authorized artifact location. The successor must identify the predecessor SHA-256 and the invalidating evidence. Return to the applicable planning or authority stage. Do not overwrite or repin the predecessor.

### 6. Generate code

Apply the in-scope rules as you write. The frozen Construction Contract governs what the code must do, must not do, and must preserve. Stop if the authoritative task identity or the contract identity no longer matches.

### 7. Run the gate script

Run the deterministic gate on the code candidate:
```bash
python scripts/check.py <paths...>                  # scan files or directories
python scripts/check.py --changed                   # scan files changed vs git HEAD
python scripts/check.py <paths...> --intent fix     # feature | fix | refactor
python scripts/check.py <paths...> --checklist full # auto (default) | full | off
python scripts/check.py <paths...> --exclude '*/vendor/*'  # repeatable glob
python scripts/check.py <paths...> --profile tdd,xp --json
```
The script decides mechanically what can be decided mechanically (AE-005). Take its output as authority for those rules — do not re-argue a gate result from reading the code.

With `--changed`, findings are scoped to the changed lines (±2) — a two-line diff does not resurface pre-existing issues, and the header reports how many were suppressed.

The checklist is scoped, not fixed. In the default `auto` mode a rule appears only when a signal for it is present in the code — boundary rules when serialization or I/O is in scope, test rules when test artifacts are, agentic rules when harness or orchestration artifacts are. With `--changed`, scope is judged from the added lines only, so a two-line diff does not arrive with the whole inventory attached. Use `--checklist full` when you want the complete set regardless, and `off` when you only want the gates. Declare `--intent` when you know it: the refactoring and defect-fix rules cannot be scoped from code alone.

### 8. Fix and re-verify

Correct each blocking gate failure. Inspect each `review` finding in context and correct it only when evidence establishes a violation. Use the repair bound from the governing task. If no bound exists, perform one repair pass and one re-verification. Then stop and report each remaining finding.

### 9. Report

Report in the format below.

## Audit workflow

1. **Read the actual artifacts.** Same as Authoring step 1.
2. **Determine scope.** Same as Authoring step 2.
3. **Confirm verifier safety.** Inspect the transitive execution path before running a verifier (AE-009).
4. **Run the gate script** on the files in question.
5. **Review judgment rules.** Attach evidence to each finding.
6. **Report without mutation.** If repair is authorized, enter the Authoring workflow before changing code.

## Output format

The deliverable depends on the mode and readiness result:

- **Authoring with matching authoritative-task and `FROZEN` contract identities:** Return the source and contract paths and SHA-256 values, the contract artifact, the code candidate, and the report.
- **Authoring with `DRAFT` or `BLOCKED`:** Return the contract artifact or content with `[UNRESOLVED]` markers. Return no code.
- **Read-only Audit:** Return findings, evidence, and the mechanical gate result. Do not return corrected code unless repair was authorized and completed through Authoring.

Report lines (at most four):

```
Bindings: authority-path=<path> authority-sha256=<64 lowercase hexadecimal characters> contract-status=FROZEN contract-path=<path> contract-sha256=<64 lowercase hexadecimal characters>
Rules applied: SC-002, SC-008, RT-011
Gates: 3 blocking → 0
Needs your call: REQ-001 — the retry cap is not in any authorized task. Cannot proceed until specified
```

Constraints on the report:
- Use one line for each category, not for each rule. Use rule IDs only. Do not repeat rule text.
- Include the `Bindings` line only for Authoring. Cite the same authority-source path and SHA-256 recorded in the contract header. Use `DRAFT` without a contract SHA-256 when the readiness gate fails.
- `Needs your call` is for genuine unresolved information: a missing authorization, an ambiguous contract, a trade-off that is the user's to make. Mark it unresolved rather than guessing (REQ-006). Omit the line when there is nothing unresolved.
- No preamble, no summary of what you changed line by line, no praise for the existing code.

## What the gates are and are not

Measured against four production repositories (requests, flask, axios, zod — 764 files): the gates flag roughly 2 findings per file, most of them `review` rather than `blocking`. Two things follow.

Severity is calibrated, not decorative. `blocking` means the pattern is always a violation. Examples include an empty catch, `as any`, or randomness in a test. `review` means that the context determines whether the pattern is a violation. Read the code before you correct a `review` finding. The gate cannot identify intent.

A high count on an unfamiliar codebase usually means scope, not rot. Type-gymnastics libraries produce hundreds of `TS-001`/`TS-003` hits because their internals genuinely use `any` deliberately. Run against a diff, not a repository, unless you actually want the backlog.

The pre-code SHA-256 comparisons verify authoritative-task and contract identity only. They do not verify the contract's correctness or acceptance. The gate script validates code structure. It cannot decide whether the problem, goal, or requirements have legitimate authority. Those are Construction Contract obligations and candidate claims.

## Do not self-certify

You are the proposer. The proposer does not accept its own work (AE-002). This has concrete consequences for how you write the report:

- Say what the gates returned. Do not say the code "is compliant," "meets the standard," or "passes all 53 rules."
- The judgment rules — the ones no script can decide — are candidate claims. If you assert one, attach the evidence (`file:line`, the test that fails on the old baseline, the contract you checked). If you cannot attach evidence, say so instead of asserting.
- A green gate report means the mechanical checks found nothing. It is not proof of correctness. Never convert gate results into a percentage or a grade (RT-009).

## Rules that most often get violated in practice

Recurring failure patterns worth checking explicitly, because they survive casual review:

- **Inventing requirements** (REQ-001). Added behavior nobody asked for, defended as obviously useful.
- **Speculative abstraction** (SC-002). An interface with one implementation, a config flag with one value, a plugin system for a single case.
- **Assertion-free tests** (RT-011). A test that calls the function, catches nothing, asserts nothing, and passes on any implementation.
- **Weakening tests to make a change pass** (RT-006). Loosening an assertion, adding `skip`, widening a tolerance. Change verification only when the requirement or the verification is proven wrong.
- **Nondeterminism disguised as a gate** (RT-007). Wall-clock time, randomness, live network, execution-order dependence inside something treated as a deterministic check.
- **Silent failure** (SC-008). Empty catch, bare except, an error mapped to `None` or `false` where the caller cannot tell failure from a valid result.
- **Inferring tool success** (AE-004). Acting on the assumption that the previous command worked because it was issued.
- **Unbounded loops** (AE-006). Retry, repair, or fan-out with no stop condition and no budget.
- **Coding before the problem is defined.** Generating code around unresolved requirements, unstated goals, or missing acceptance criteria — then defending the code as the implicit specification.
- **Reconstructing authority after the fact.** Rewriting, normalizing, or expanding the task in a contract or report, then presenting the reconstruction as the authoritative prompt. Bind the original task bytes before deriving requirements.

---

# Canonical Engineering Rule Inventory

**Base and language engineering rules:** 41 · **Method and agentic overlays:** 12 · **Total admitted rules:** 53

## Activation

- **[MUST]** applies whenever the rule's scope applies.
- **[CONDITIONAL]** applies only when the condition stated in the rule exists.
- Apply the Python and TypeScript overlays only when that language is in scope.
- Apply the TDD and XP overlays only when those development methods are active.
- Apply the Agentic Engineering overlay when an agent plans, changes, reviews, repairs, evaluates, orchestrates, or adapts repository or harness artifacts.
- These rules guide candidate construction. They do not override the authorized task, repository governance, architecture decisions, or authoritative verification.

## Technical Writing (3)

- **TW-001** [MUST] — Use clear, direct, unambiguous language and one stable term for each technical concept. Do not vary terminology for style.
- **TW-002** [MUST] — Structure technical text so each sentence carries one primary claim or action. Give each paragraph one topic, and introduce information in a logical progression.
- **TW-003** [MUST] — Put required actions and conditions in the operative instruction or specification. Do not put them only in notes, asides, comments, or duplicated prose. Keep documentation synchronized with the authoritative artifact it describes.

## Requirements (7)

- **REQ-001** [MUST] — Do not invent requirements. Every requirement or behavior change must derive from an authorized task, stakeholder need, business objective, governing specification, or explicit constraint.
- **REQ-002** [MUST] — Express one independently interpretable obligation per requirement. Use terminology consistently so reasonable readers reach the same meaning.
- **REQ-003** [MUST] — Specify observable behavior precisely enough to identify relevant preconditions or triggers, expected outcomes, side effects, and required failure behavior. Do not leak an implementation unless the implementation itself is constrained.
- **REQ-004** [MUST] — Every normative requirement must have an objective verification or acceptance path. If compliance can only be judged by opinion, the requirement is not ready.
- **REQ-005** [MUST] — A requirement must be necessary, feasible, and within authorized scope. Do not add unnecessary implementation constraints or gold-plated behavior.
- **REQ-006** [MUST] — The requirement set for the current increment must be internally consistent and sufficiently complete to proceed at an acceptable risk. Mark unresolved information as unresolved rather than guessing.
- **REQ-007** [CONDITIONAL] — Where requirement, implementation, and test artifacts exist, preserve traceability from the authoritative source to the requirement, changed implementation, and verification evidence.

## Software Construction (11)

- **SC-001** [MUST] — Satisfy the authorized contract and preserve correctness before optimizing style, abstraction, or elegance.
- **SC-002** [MUST] — Make the smallest sufficient change and design that solves the authorized problem. Do not introduce speculative behavior, abstractions, dependencies, or complexity. Do not move local complexity into hidden global complexity.
- **SC-003** [MUST] — Hide implementation decisions behind the smallest sufficient stable interface. Do not leak a design decision across modules or force callers to understand unnecessary internal complexity.
- **SC-004** [MUST] — Use precise, intention-revealing, domain-appropriate names. Use the same name for the same concept.
- **SC-005** [MUST] — Keep each unit of code conceptually coherent at one useful level of abstraction. Split or combine code to reduce cognitive load and interface complexity, not to satisfy arbitrary size targets.
- **SC-006** [MUST] — Keep one authoritative representation of each piece of knowledge when practical. Do not duplicate logic, constants, type facts, requirements, or design decisions in forms that can drift independently.
- **SC-007** [MUST] — Comments and API documentation must explain non-obvious intent, rationale, invariants, contracts, or consequences. Do not restate obvious code. Update nearby documentation when the code invalidates it.
- **SC-008** [MUST] — Make failure behavior explicit and appropriate to caller needs. Preserve useful failure context. Do not silently swallow, disguise, or ambiguously encode exceptional failure.
- **SC-009** [CONDITIONAL] — Where correctness depends on operation order, state progression, or a required protocol, make that dependency explicit and enforceable through the interface, data flow, or state model. Do not rely on undocumented call ordering or hidden temporal state.
- **SC-010** [MUST] — Validate data and state when they cross an external, trust, ownership, serialization, persistence, process, or service boundary. Use one authoritative contract for allowed shape, values, optionality, and failure semantics so producers and consumers cannot silently disagree.
- **SC-011** [CONDITIONAL] — When correctness depends on an invariant, precondition, or postcondition that the type system or interface cannot guarantee, make that condition executable at the nearest authoritative boundary or verify it directly. Do not substitute proxy conditions for the semantic invariant.

## Refactoring & Testing (11)

- **RT-001** [MUST] — A refactoring must preserve observable behavior. If observable behavior changes, treat the work as a behavior change, not as refactoring.
- **RT-002** [MUST] — Do not mix behavior change and structural cleanup invisibly. Keep the intent of each change explicit so verification can distinguish new behavior from behavior-preserving restructuring.
- **RT-003** [MUST] — Perform refactoring and other high-risk structural changes in small, reviewable increments. Verify after each meaningful increment, and increase scrutiny as risk increases.
- **RT-004** [MUST] — Changed behavior must have verification evidence that tests the observable contract rather than incidental implementation details.
- **RT-005** [CONDITIONAL] — For a reproducible defect fix, add or update regression evidence that fails on the faulty baseline for the targeted behavior and passes after the fix.
- **RT-006** [MUST] — Do not weaken, delete, bypass, or rewrite valid verification merely to make a candidate change pass. Change verification only when an authoritative requirement or the verification itself is proven wrong.
- **RT-007** [MUST] — Verification used as a deterministic automated gate must be self-validating and repeatable for the same software version, declared dependency and toolchain state, and controlled inputs. Tests must not depend on execution order or leaked mutable state. Uncontrolled time, randomness, scheduling, network state, or external-service behavior must not masquerade as deterministic verification evidence.
- **RT-008** [CONDITIONAL] — When the observable contract contains thresholds, ranges, empty or missing cases, state transitions, or defined failure modes, verification must exercise the materially relevant boundaries and failure partitions. Do not test only representative normal-path values.
- **RT-009** [MUST] — Do not treat code-coverage percentage as proof of correctness or verification adequacy. Use coverage to identify unexercised code. Establish adequacy with behavior-specific evidence against the required observable contract.
- **RT-010** [CONDITIONAL] — When changed behavior crosses a module, process, service, persistence, serialization, third-party, or other independently owned boundary, verify the actual boundary contract and both sides' interpretation of it. Unit tests of each side alone are not sufficient evidence for that boundary.
- **RT-011** [MUST] — Verification evidence must contain a meaningful oracle that can fail when the targeted contract is violated. Do not treat assertion-free, tautological, unused-input, or unrelated assertions as evidence of correctness.

## Architecture Decisions (4)

- **AD-001** [MUST] — For a consequential architecture choice, record the problem context, considered alternatives, decision, justification, consequences, and material trade-offs. Do not present a contextual choice as a universal best practice.
- **AD-002** [MUST] — Treat established architectural boundaries, contracts, ownership, and dependency directions as constraints. Do not bypass them for local convenience unless the authorized task explicitly changes the architecture.
- **AD-003** [MUST] — An architecture change must identify the quality attributes and coupling it materially affects. Justify the chosen trade-off against the authorized requirements.
- **AD-004** [CONDITIONAL] — When changing a public contract, shared data ownership, or cross-boundary interface, preserve compatibility or provide an explicit migration. Account for affected consumers and consequences.

## Python Overlay (2)

- **PY-001** [CONDITIONAL] — When a Python function has an exceptional failure state distinct from valid results, signal it with an exception rather than an ambiguous falsey sentinel such as `None`. Make the caller-facing failure contract explicit.
- **PY-002** [CONDITIONAL] — For Python APIs whose exceptions are part of the contract, document when those exceptions are raised. Do not duplicate type facts in docstrings when annotations already express them.

## TypeScript Overlay (3)

- **TS-001** [MUST] — Treat values of unknown external shape as `unknown` until they are validated or narrowed. Do not use plain `any` to bypass uncertainty.
- **TS-002** [MUST] — Model types so declared states are valid and truthful. Prefer a less precise type over an inaccurate type that claims facts the program has not established.
- **TS-003** [MUST] — Do not use type assertions to silence type errors or manufacture unproven facts. When an unsafe assertion is unavoidable at a boundary, isolate it behind a well-typed interface.

## Test-Driven Development Overlay (1)

- **TDD-001** [MUST WHEN TDD PROFILE IS ACTIVE] — Establish an executable test that fails for the absence or defect of the targeted behavior before the production change. Make the smallest production change that makes the test pass. Refactor only while the applicable verification remains green.

## Extreme Programming Overlay (1)

- **XP-001** [MUST WHEN XP PROFILE IS ACTIVE] — Keep each increment continuously integrable. Integrate small changes frequently and run the applicable automated build and verification after integration. Restore a failed integration before adding unrelated work.

## Agentic Engineering Overlay (10)

- **AE-001** [MUST] — Before changing repository artifacts, inspect the current governing instructions, repository state, relevant implementation, applicable tests, and affected interfaces. Do not substitute model memory, assumptions, or an isolated snippet for repository evidence.
- **AE-002** [MUST] — Treat agent-generated code, tests, diagnoses, harness changes, and completion claims as candidates. Use the authoritative external verifier or an authorized human for acceptance or promotion. The proposer or executor must not self-certify.
- **AE-003** [MUST] — Preserve authorized scope and unrelated repository work. Destructive operations and protected side effects require explicit authority.
- **AE-004** [CONDITIONAL] — When a later action depends on an earlier action, inspect the actual tool or environment result first. Do not infer success from the requested action, prior plan, or model statement.
- **AE-005** [MUST] — When an available deterministic mechanism can decide a property exactly, use it as the authority. Do not replace exact verification or computation with model judgment.
- **AE-006** [MUST] — Give each retry loop, repair loop, recursion path, and subagent fan-out explicit stop conditions and finite resource budgets. If repeated work produces no new evidence or progress, stop, change strategy within budget, or hand off.
- **AE-007** [CONDITIONAL] — When work uses multiple or recursive agents, define each unit's task, allowed scope, output contract, and termination condition. Parallelize only independent work. Otherwise, define synchronization and merge rules.
- **AE-008** [MUST] — Evaluate an agentic system as a versioned configuration of model, instructions, tools, harness policy, budgets, environment, and verifier. Re-evaluate after a material configuration change before transferring a measured result.
- **AE-009** [MUST] — Before executing a verifier (test suite, gate script, check harness, or acceptance runner), confirm that the execution is safe transitively: the verifier entry point and every wrapper, hook, fixture, configuration source, subprocess invocation, and network call it reaches must be within authorized scope and must not produce destructive side effects outside the verified artifact. Do not treat a verifier as safe because its entry point appears safe; inspect or constrain the transitive closure of its execution.
- **AE-010** [MUST] — Before the first mutation in an increment, re-read each applicable governing source — task authorization, repository governance, architecture decisions, interface contracts, and upstream specifications — from its authoritative location. Do not rely on a prior session's cached content, model memory, or a stale copy when the authoritative source is accessible.
