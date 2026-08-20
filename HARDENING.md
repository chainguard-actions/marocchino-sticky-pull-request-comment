<!-- markdownlint-disable -->

# Hardening Report: marocchino--sticky-pull-request-comment/v3.0.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **marocchino--sticky-pull-request-comment/v3.0.2** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `actions/checkout@v6`, which is pinned to a mutable tag rather than a full 40-character commit SHA. This means the action could be silently updated to a different (potentially malicious) version without any change to the workflow file. It should be pinned to a specific commit SHA, e.g. `actions/checkout@<40-char-sha> # v6`.

Locations:

- `.github/workflows/test.yml:15`

### github-env-injection (severity: high)

The `run:` block at line 21 pipes the raw, unsanitized output of `npm run all` directly into `$GITHUB_ENV` (`npm run all >> "$GITHUB_ENV" 2>&1 || true`). This workflow is triggered on `pull_request` events, meaning attacker-controlled code in a PR can produce output that injects arbitrary key=value pairs into the GitHub environment file — allowing environment variable injection for subsequent steps. The output is not passed through the required sanitization step (`printf '%s' ... | tr -d '\n\r'`) before being written to `$GITHUB_ENV`. Additionally, lines 20 and 22–23 write the heredoc delimiter and terminator around this unsanitized content, compounding the risk.

Locations:

- `.github/workflows/test.yml:21`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, github-env-injection

**Notes:**

1. Pinned actions/checkout@v6 to full SHA d23441a48e516b6c34aea4fa41551a30e30af803 (keeping # v6 comment). 2. Fixed github-env-injection by capturing 'npm run all' output to /tmp/npm_all_output.txt first, then writing the heredoc delimiter to $GITHUB_ENV before cat-ing the captured output. This prevents npm output from appearing before the EOF delimiter and injecting arbitrary environment variables.

