<!-- markdownlint-disable -->

# Hardening Report: octoguide--bot/0.22.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **octoguide--bot/0.22.0** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `codecov/codecov-action@v3`, which is pinned to a mutable version tag rather than an immutable 40-character commit SHA. This exposes the workflow to supply-chain attacks if the tag is moved to a malicious commit.

Locations:

- `.github/workflows/ci.yml:62`

### missing-permissions (severity: medium)

The workflow file `ci.yml` has no top-level `permissions:` key and none of its 11 jobs (build, build_release, build_site, lint, lint_knip, lint_markdown, lint_packages, lint_spelling, prettier, test, type_check) define a job-level `permissions:` block. Without explicit permissions, the workflow inherits the repository default (which may be `write-all` for older repositories), granting unnecessarily broad token access.

Locations:

- `.github/workflows/ci.yml:1`

### missing-permissions (severity: medium)

The workflow file `contributors.yml` has no top-level `permissions:` key and its single job (`contributors`) has no job-level `permissions:` block. Without explicit permissions, the workflow inherits the repository default, which may grant unnecessarily broad token access.

Locations:

- `.github/workflows/contributors.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed three findings across two workflow files: (1) Pinned codecov/codecov-action from mutable tag @v3 to full SHA @ab904c41d6ece82784817410c45d8b8c02684457 in ci.yml. (2) Added `permissions: {}` at the top level of ci.yml since none of the 11 jobs require GITHUB_TOKEN write access. (3) Added `permissions: contents: read` at the top level of contributors.yml — the job uses a GitHub App token for write operations, so the default GITHUB_TOKEN only needs read access for checkout.

