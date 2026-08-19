<!-- markdownlint-disable -->

# Hardening Report: chkfung--android-version-actions/v1.2.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **chkfung--android-version-actions/v1.2.3** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses actions/checkout@v2, which is a mutable tag reference rather than a pinned full 40-character commit SHA. This means the action could be silently updated or replaced with a different (potentially malicious) version without any change to the workflow file, creating a supply-chain risk.

Locations:

- `.github/workflows/automate_ncc.yml:11`

### missing-permissions (severity: medium)

The workflow file .github/workflows/automate_ncc.yml has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (e.g., write access to contents). Minimal explicit permissions should be declared.

Locations:

- `.github/workflows/automate_ncc.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both findings in .github/workflows/automate_ncc.yml: (1) Pinned actions/checkout@v2 to its full commit SHA (0717577d45739eb3c851188b29f50ed6c0b2194e) with a # v2 comment for readability. (2) Added a top-level `permissions:` block with `contents: write` — the minimum required since the workflow creates a new branch and pushes commits to the repository. All other permissions default to none.

