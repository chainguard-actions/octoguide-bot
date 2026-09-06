<!-- markdownlint-disable -->

# Hardening Report: octoguide--bot/0.23.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **octoguide--bot/0.23.0** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `codecov/codecov-action@v3` which is pinned to a mutable version tag rather than an immutable 40-character commit SHA. This exposes the workflow to supply-chain attacks if the tag is moved to a different commit.

Locations:

- `.github/workflows/ci.yml:56`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and none of its jobs define a `permissions:` block. Without explicit permissions, the workflow inherits the default repository token permissions, which may be broader than necessary.

Locations:

- `.github/workflows/ci.yml:1`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the single `contributors` job has no `permissions:` block. Without explicit permissions, the workflow inherits the default repository token permissions, which may be broader than necessary.

Locations:

- `.github/workflows/contributors.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed three findings across two workflow files:
1. ci.yml: Pinned `codecov/codecov-action@v3` to full SHA `ab904c41d6ece82784817410c45d8b8c02684457` with `# v3` comment. Added top-level `permissions: {}` to restrict GITHUB_TOKEN to no permissions.
2. contributors.yml: Added top-level `permissions: {}` to restrict GITHUB_TOKEN to no permissions (the job uses a GitHub App token for its actual write operations, so the default GITHUB_TOKEN needs no permissions).

