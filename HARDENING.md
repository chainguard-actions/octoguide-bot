<!-- markdownlint-disable -->

# Hardening Report: octoguide--bot/0.21.6

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **octoguide--bot/0.21.6** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `codecov/codecov-action@v3`, which is pinned to a mutable tag (`v3`) rather than an immutable 40-character commit SHA. This exposes the workflow to supply-chain attacks if the tag is moved to a malicious commit. It should be replaced with a full SHA pin, e.g. `codecov/codecov-action@<40-hex-sha> # v3`.

Locations:

- `.github/workflows/ci.yml:57`

### missing-permissions (severity: medium)

The workflow file `ci.yml` has no top-level `permissions:` block and none of its 12 jobs define job-level `permissions:`. Without explicit permissions, the workflow inherits the repository default (typically `write-all` for private repos or `read-all` for public repos), granting more access than necessary. A minimal `permissions:` block should be added.

Locations:

- `.github/workflows/ci.yml:1`

### missing-permissions (severity: medium)

The workflow file `contributors.yml` has no top-level `permissions:` block and its only job (`contributors`) has no job-level `permissions:`. Without explicit permissions, the workflow inherits the repository default, granting more access than necessary. A minimal `permissions:` block (e.g. `contents: read` plus whatever the all-contributors action needs) should be added.

Locations:

- `.github/workflows/contributors.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned `codecov/codecov-action@v3` to full SHA `ab904c41d6ece82784817410c45d8b8c02684457` with `# v3` comment in ci.yml. 2. Added `permissions: contents: read` top-level block to ci.yml (CI jobs only need to read code). 3. Added `permissions: contents: read` top-level block to contributors.yml (write operations are performed via a GitHub App token, not the default GITHUB_TOKEN, so the workflow-level token only needs read access).

