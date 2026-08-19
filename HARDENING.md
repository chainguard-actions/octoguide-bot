<!-- markdownlint-disable -->

# Hardening Report: octoguide--bot/0.21.7

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **octoguide--bot/0.21.7** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `codecov/codecov-action@v3`, which is pinned to a mutable tag rather than a full 40-character commit SHA. This allows the action to be silently updated to a different (potentially malicious) version without any change to the workflow file.

Locations:

- `.github/workflows/ci.yml:63`

### missing-permissions (severity: medium)

ci.yml has no top-level `permissions:` key and no job-level `permissions:` key on any of its jobs. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be broader than necessary.

Locations:

- `.github/workflows/ci.yml:1`

### missing-permissions (severity: medium)

contributors.yml has no top-level `permissions:` key and no job-level `permissions:` key on its job. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be broader than necessary.

Locations:

- `.github/workflows/contributors.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned codecov/codecov-action from mutable tag @v3 to full SHA @ab904c41d6ece82784817410c45d8b8c02684457 # v3 in ci.yml. 2. Added top-level `permissions: contents: read` to ci.yml — the workflow only builds, lints, and tests code so read-only access is sufficient. 3. Added top-level `permissions: contents: read` to contributors.yml — the actual repository write operations are performed using a GitHub App token (not GITHUB_TOKEN), so GITHUB_TOKEN only needs minimal read access.

