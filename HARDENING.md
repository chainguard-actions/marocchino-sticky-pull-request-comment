<!-- markdownlint-disable -->

# Hardening Report: marocchino--sticky-pull-request-comment/v3.0.5

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **marocchino--sticky-pull-request-comment/v3.0.5** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `actions/checkout@v7` which is pinned to a mutable version tag rather than an immutable 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit, enabling supply-chain attacks. It should be replaced with the full SHA, e.g. `actions/checkout@<40-char-sha> # v7`.

Locations:

- `.github/workflows/test.yml:14`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced `actions/checkout@v7` with `actions/checkout@9c091bb21b7c1c1d1991bb908d89e4e9dddfe3e0 # v7` in `.github/workflows/test.yml` line 14. The full commit SHA was resolved via lookup_action_sha to prevent supply-chain attacks from mutable tag references.

