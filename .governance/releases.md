# Releases

## Purpose

Define how the central workflow catalog publishes versions and how consumers update them.

## Version Policy

Publish stable workflow packages with semantic release tags.

Use an exact release tag or commit SHA for a production consumer. Do not use `main` as a production consumer pin.

A moving major ref may be used only when the consumer update process still requires an explicit reviewed update.

## Release Gate

Before a release:

1. verify all required deterministic catalog checks;
2. verify changed agentic workflow acceptance cases;
3. compile every changed workflow when compilation is required;
4. review changed generated lock files;
5. record the exact release candidate identity;
6. confirm no required gate is `FAIL` or `BLOCKED`;
7. confirm explicit release authority.

Do not publish from an unverified working tree or unaccepted commit.

## Compatibility

Use a major version change for an incompatible consumer contract change, a minor version for a backward-compatible capability addition, and a patch version for a backward-compatible correction.

Do not silently change an immutable release tag.

## Consumer Updates

A consuming repository must review a workflow update before adoption and run its own deterministic gates.

Central catalog acceptance does not replace the consuming repository's local acceptance contract.

## Rollback

Rollback selects a previously accepted immutable version. Do not repair a bad release tag in place; publish a new corrected version.
