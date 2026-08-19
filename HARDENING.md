<!-- markdownlint-disable -->

# Hardening Report: marocchino--sticky-pull-request-comment/v3.0.4

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **marocchino--sticky-pull-request-comment/v3.0.4** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow references `actions/checkout@v6`, which uses a mutable tag (`@v6`) instead of a pinned 40-character commit SHA. This means the action could be silently updated to a different (potentially malicious) version without any change to the workflow file, creating a supply-chain risk.

Locations:

- `.github/workflows/test.yml:14`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced `actions/checkout@v6` (mutable tag) with `actions/checkout@d23441a48e516b6c34aea4fa41551a30e30af803 # v6` (pinned full commit SHA) in `.github/workflows/test.yml` line 14. The SHA was resolved via lookup_action_sha. The human-readable `# v6` comment is preserved for maintainability.

