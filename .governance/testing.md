# Testing

## Purpose

Define which deterministic checks must run for an active task. Testing produces results; it does not decide acceptance.

## Test Selection

The active task contract must name the required checks for the authorized increment.

Select checks from the observable requirements and affected boundaries. Do not invent a proxy check when the required behavior has no valid test path.

If a normative requirement has no objective test or other verification path, return `BLOCKED` before completion.

## Required Properties

A deterministic check used as gate evidence must:

- be repeatable for the same declared software, toolchain, and controlled inputs;
- contain a meaningful oracle that can fail when the target contract is violated;
- exercise the affected observable contract rather than incidental implementation details;
- avoid uncontrolled time, randomness, network state, execution order, or leaked mutable state;
- preserve valid predecessor or frozen acceptance cases.

Do not use assertion-free, tautological, skipped, weakened, or unrelated checks as acceptance evidence.

Coverage percentage may identify unexercised code. It is not proof of correctness.

## Defect and Review Repair

For a reproducible defect, require regression evidence that distinguishes the faulty baseline from the repaired behavior when the active contract requires a behavior change.

For review repair, run the exact check or contract predicate associated with the accepted finding plus any required regression checks named by the active contract.

Do not alter valid verification merely to make a candidate pass.

## Boundary Changes

When changed behavior crosses an independently owned module, process, service, persistence, serialization, consumer, or tool boundary, test the actual boundary contract when the active contract requires it.

## Engineering Rules Gate

When the active code-capable contract requires the canonical engineering-rules gate, resolve it through `.governance/authority.md` and execute it only after confirming verifier safety under the active contract.

A green engineering-rules mechanical gate is evidence about the properties it checks. It is not repository acceptance.

## Test Results

Record the command or check identity, controlled inputs, exact candidate identity, and result in `.governance/evidence.md` form.

Pass test results to the verifier selected by the active contract. Do not convert test success directly into completion `PASS`.
