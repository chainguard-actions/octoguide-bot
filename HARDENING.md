<!-- markdownlint-disable -->

# Hardening Report: octoguide--bot/0.21.9

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **octoguide--bot/0.21.9** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `codecov/codecov-action@v3`, which is pinned to a mutable version tag rather than a full 40-character commit SHA. This allows the action to be silently updated to a different (potentially malicious) version without any change to the workflow file.

Locations:

- `.github/workflows/ci.yml:77`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and no job-level `permissions:` keys on any of its jobs. Without explicit permissions, the workflow inherits the repository's default token permissions (which may be `write-all` for older repositories), granting broader access than necessary.

Locations:

- `.github/workflows/ci.yml:1`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and no job-level `permissions:` keys on any of its jobs. Without explicit permissions, the workflow inherits the repository's default token permissions, granting broader access than necessary.

Locations:

- `.github/workflows/contributors.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Three fixes applied across two workflow files:
1. ci.yml: Pinned `codecov/codecov-action@v3` to full SHA `ab904c41d6ece82784817410c45d8b8c02684457` (# v3). Added top-level `permissions: contents: read` since the CI workflow only reads code and uploads coverage.
2. contributors.yml: Added top-level `permissions: contents: write` and `pull-requests: write` since the all-contributors-auto-action needs to push commits and open/update pull requests.

