<!-- markdownlint-disable -->

# Hardening Report: octoguide--bot/0.21.8

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **octoguide--bot/0.21.8** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The step `uses: codecov/codecov-action@v3` in ci.yml references a mutable tag (`@v3`) instead of a full 40-character commit SHA. This means the action could be silently updated to a different (potentially malicious) version without any change to the workflow file. It should be pinned to a specific commit SHA, e.g. `codecov/codecov-action@<sha> # v3`.

Locations:

- `.github/workflows/ci.yml:79`

### missing-permissions (severity: medium)

The workflow file ci.yml has no top-level `permissions:` key and none of its jobs define job-level `permissions:` blocks. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (write access to all scopes). A minimal `permissions:` block should be added at the top level or on each job.

Locations:

- `.github/workflows/ci.yml:1`

### missing-permissions (severity: medium)

The workflow file contributors.yml has no top-level `permissions:` key and its only job (`contributors`) has no job-level `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad. A minimal `permissions:` block should be added.

Locations:

- `.github/workflows/contributors.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned `codecov/codecov-action@v3` to full SHA `ab904c41d6ece82784817410c45d8b8c02684457` in ci.yml (line 79). 2. Added `permissions: contents: read` top-level block to ci.yml — all jobs only need to read repository contents for checkout. 3. Added `permissions: contents: read` top-level block to contributors.yml — the job uses a GitHub App token for write operations, so the default GITHUB_TOKEN only needs read access.

