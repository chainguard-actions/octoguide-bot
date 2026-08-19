<!-- markdownlint-disable -->

# Hardening Report: octoguide--bot/0.21.10

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **octoguide--bot/0.21.10** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `codecov/codecov-action@v3`, which is pinned to a mutable version tag rather than an immutable 40-character commit SHA. This exposes the workflow to supply-chain attacks if the tag is moved to a malicious commit.

Locations:

- `.github/workflows/ci.yml:71`

### missing-permissions (severity: medium)

ci.yml has no top-level `permissions:` block and none of its 11 jobs (build, build_release, build_site, lint, lint_knip, lint_markdown, lint_packages, lint_spelling, prettier, test, type_check) define job-level permissions. Without explicit permissions, the workflow inherits the repository default, which may be overly broad (write access to all scopes for private repos or repos with permissive defaults).

Locations:

- `.github/workflows/ci.yml:1`

### missing-permissions (severity: medium)

contributors.yml has no top-level `permissions:` block and its single `contributors` job has no job-level permissions block. The job uses a GitHub App token to run `all-contributors-auto-action`, which likely needs write access to the repository, but no explicit minimal permissions are declared.

Locations:

- `.github/workflows/contributors.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Three fixes applied across two workflow files:
1. ci.yml: Pinned `codecov/codecov-action@v3` to full SHA `ab904c41d6ece82784817410c45d8b8c02684457` (keeping `# v3` comment). Added top-level `permissions: contents: read` block — all 11 jobs are build/test/lint tasks requiring only read access.
2. contributors.yml: Added top-level `permissions: contents: read` block. The job uses a GitHub App token for write operations, so the workflow's own GITHUB_TOKEN only needs read access to the repository.

