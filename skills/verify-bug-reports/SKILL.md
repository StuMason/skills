---
name: verify-bug-reports
description: Never take bug reports or QA feedback as gospel. Use before fixing anything QA or a user reported, to verify what correct behaviour actually is.
---

# Verify Bug Reports

QA describes what they see. They do not define what is correct. A "fix" for a misunderstood requirement is a new bug with a paper trail, so before fixing what is reported, verify the report.

## The check

1. **Reproduce what they saw.** If you cannot reproduce it, that is your finding, go back with exactly what you tried.
2. **Find the source of truth for expected behaviour.** The ticket, the spec, an ADR, how the rest of the codebase handles the same pattern. Not the bug report itself, and not vibes.
3. **Deliver a verdict, one of three:**
   - **The report is right.** Behaviour contradicts the source of truth. Fix it.
   - **The report misunderstands the requirement.** The observed behaviour is correct. Explain why, with the source cited. Do not "fix" it. Do not change working code to match a misreading.
   - **Nobody actually knows what correct is.** There is no source of truth to check against. That is not a bug, that is an unwritten requirement: stop and get it decided before touching code (see the ticket-readiness skill).

## Why bother

Because "QA said so" is how correct code gets broken politely. The reporter is describing a symptom through their own model of the system, and their model may be wrong. Asking "hang on, is that actually the intended behaviour?" costs nothing. Being the agent who quietly broke checkout because a tester misread the spec costs rather more.
