# Releases

## Purpose

Define how the central workflow catalog publishes versions and how consumers update them.

## Version policy

Publish stable workflow packages with semantic release tags.

Use an exact release tag or commit SHA for a production consumer.

Do not use `main` as a production consumer pin.

A moving major ref can be used only when the consumer update process still requires an explicit reviewed update.

## Release gate

Before a release:

1. Verify all required deterministic catalog checks.
2. Verify all changed agentic workflow acceptance cases.
3. Compile every changed agentic workflow that requires compilation.
4. Review changed `.lock.yml` files.
5. Review changed `.github/aw/actions-lock.json` content.
6. Record the exact release candidate commit SHA.
7. Confirm that no required gate is FAIL or BLOCKED.

Do not publish from an unverified working tree or an unaccepted commit.

## Compatibility

Use a major version change for an incompatible consumer contract change.

Use a minor version change for a backward-compatible capability addition.

Use a patch version change for a backward-compatible correction.

Do not silently change the behavior of an existing immutable release tag.

## Consumer updates

A consuming repository must review a workflow update before adoption.

Run the consuming repository's deterministic gates on the updated workflow version.

The central catalog PASS does not replace the consuming repository's local acceptance contract.

## Rollback

Rollback means selecting a previously accepted immutable version.

Do not repair a bad release tag in place.

Publish a new version for a correction.
