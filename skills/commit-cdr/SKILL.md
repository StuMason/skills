---
name: commit-cdr
description: Commit with a Conversation Decision Record. Use for every commit in repos that keep CDRs, or whenever a commit may land with no PR, no review, and no human reading the diff. Writes the decision record, stages it with the code, and adds machine-parseable provenance trailers.
---

# Commit with a CDR

A Conversation Decision Record is likely the ONLY record of what happened and why. There may be no PR, no code review, no human reading the diff before or after this lands. Write accordingly: capture everything, because nothing else will.

## Step 1: Gather git context

Run these in parallel:

- `git status` (never `-uall`)
- `git diff` and `git diff --staged`
- `git log --oneline -10` for the repo's commit style

If there is nothing to commit, say so and stop.

## Step 2: Write the CDR

Reflect on the conversation that led to these changes. Write the CDR at `docs/context/YYYY-MM-DD-short-slug.md` (today's date, slug derived from the changes; if the repo keeps CDRs elsewhere, follow the repo). If a CDR already exists for today, append a number to the slug.

Use this template as a guide. Adapt it, skip sections that don't apply, and err on the side of capturing too much rather than too little.

```markdown
# [Short Title Derived From Changes]

**Date:** YYYY-MM-DD

## Provenance

| Field | Value |
|---|---|
| **Model** | Full model identifier, e.g. `claude-opus-4-20250514` |
| **Harness** | Tool that orchestrated the generation, e.g. `claude-code 2.1`, `cursor 0.43` |
| **Harness config** | Relevant settings: system prompt version, tools enabled, MCP servers connected |
| **Session ID** | Unique identifier for the session that produced this code (generate a UUID if unavailable) |
| **Generation timestamp** | When the code was generated (not when it was committed) |
| **Review status** | `none` · `human-approved` · `agent-reviewed` · `auto-merged` — be honest, this is the first thing checked during an incident |
| **Confidence** | `high` · `medium` · `low` — the model's self-assessed certainty |
| **Triggered by** | What initiated this work: `human-request`, an agent id, a ticket, a cron schedule, an alert |
| **Touched areas** | e.g. `auth`, `crypto`, `input-validation`, `database`, `api-surface`, `config`, `infra` |
| **Test status** | `tests-added` · `tests-modified` · `tests-none` — absence of tests is itself a risk signal |
| **Dependencies introduced** | New packages, APIs, or services this code now relies on |
| **Dependencies reimplemented** | Functionality implemented inline that could have been a library — see limitation below |

> **Deps-Reimplemented limitation:** self-reported by the same model that wrote the code, which often doesn't know what it doesn't know. Best-effort only; supplement with static analysis. `none` does NOT mean no reimplementation occurred.

## What was asked
The human's request as faithfully as possible — the actual intent, phrasing, and context, not a sanitised summary. Include constraints and preferences given, and what was explicitly NOT asked for, if relevant.

## What changed
A narrative for someone who may never read the diff: files created/modified/deleted, new endpoints/functions/modules, behavioral changes, data model changes, config or infrastructure changes, dependency changes.

## Why
The problem being solved, why this solution and not another, and what triggered the change.

## Decisions made
- **Decision 1**: chose X because Y.
- Flag decisions that were uncertain or coin-flips between near-equal options — future reviewers need to know which choices were deliberate.

## Rejected alternatives
Things considered but not done, and why.

## Agent lineage
If this work was part of a delegation chain, document it: originator (human, agent, schedule, alert), the chain (e.g. `alert-agent → triage-agent → this session`), and upstream context (incident ID, parent task). Skip for direct human-to-agent work.

## Risk surface
Anything a future scanner or remediation tool should pay attention to:
- **Crypto/auth patterns used**: e.g. "HMAC-SHA256 for token validation", "hand-rolled JWT parsing"
- **Input boundaries**: where external input enters and how it is handled
- **Data flow**: does this touch PII, secrets, or credentials?
- **Assumptions**: what this code assumes about its environment that could be wrong
- **Known gaps**: things not asked about or explicitly punted on — be honest, this is the most valuable field
- **Uncertain choices**: specific decisions the model was unsure of, individually — not the same as overall confidence

## Context
Relevant conversation notes: links discussed, constraints mentioned, things to revisit.
```

Rules for CDR content:

- Write it like a black box recording, not a casual note — for a machine matching this commit against a future vulnerability advisory, and for a human investigating an incident at 2am with no prior context.
- Capture the original request faithfully; paraphrasing loses signal.
- Be specific about crypto, auth, and input handling — vague descriptions are useless for remediation.
- `Review: none` and `Tests: tests-none` are not shameful, they are honest. Lying about review status defeats the entire record. `Confidence: low` is a gift to whoever triages later.
- If the change is trivial, write a minimal CDR: Provenance, "What changed", "Why".
- **Do not put a commit SHA in the CDR.** The commit message's `CDR: <path>` trailer is the canonical link; a reverse pointer can't be added in the same commit it references (every amend changes the SHA). Reverse lookup when needed: `git log --oneline -- docs/context/<file>.md`.

## Step 3: Stage and commit

1. Stage the code changes (specific files, never `git add -A`) and the CDR file.
2. Draft a commit message following the repo's style, then add machine-parseable provenance trailers:

```
feat: add JWT validation endpoint

Descriptive commit message body as normal.

Model: claude-opus-4-20250514
Harness: claude-code 2.1
Generated: 2026-07-23T10:30:00Z
Session-ID: a1b2c3d4e5f6
Review: none
Confidence: medium
Triggered-By: human-request
Tests: tests-added
Touched-Areas: auth, crypto
Deps-Reimplemented: jwt-validation
Risk-Flags: hand-rolled-crypto, external-input-parsing
CDR: docs/context/2026-07-23-jwt-validation.md
```

The trailers exist so scanners can query thousands of repos with `git log` without parsing markdown; the CDR is the full narrative. Both matter. The highest-value trailers: **Review** (during an incident, the first question is "did anyone look at this?"), **Model** + **Generated** (scope "everything model X produced in window Y" when an advisory drops), **Session-ID** (find every commit from a session later found corrupted), **Risk-Flags** (be generous — false positives are fine, false negatives are not).

3. Commit, verify with `git status`, and push. If the push fails (branch protection, network), surface the error and stop — do NOT retry blindly.

No amend dance, no SHA chase.
