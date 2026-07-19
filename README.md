# Skills

Six skills, one per scar. Each exists because its absence cost me something: shipped duct tape, code built on guesses, a "fix" for a bug that was not one, work nobody heard about, prose that read like a model wrote it, and answers buried under three paragraphs of preamble. Rules I beat into my own agents shipping real production systems: 20+ apps, a self-hosted estate, actual clients.

## Install

```bash
npx skills@latest add StuMason/skills
```

Or as a Claude Code plugin:

```
/plugin marketplace add StuMason/skills
/plugin install stumason-skills@stumason
```

## The skills

### [/stop-patching](./skills/stop-patching/SKILL.md)

When the implementation fights back, the wall is information: the design is wrong somewhere. Stops the agent patching around it with flags, special cases and shims, and makes it re-derive the design and propose instead. Duct tape is a confession.

### [/ticket-readiness](./skills/ticket-readiness/SKILL.md)

Vague acceptance criteria are a blocker, not a challenge. If the business rule cannot be said in plain English, the ticket goes back with specific questions, each with a recommended answer so they actually get answered.

### [/verify-bug-reports](./skills/verify-bug-reports/SKILL.md)

QA describes what they see, not what is correct. Before fixing a report, reproduce it, find the source of truth, and deliver a verdict: real bug, misread requirement, or nobody ever decided.

### [/brag-nudge](./skills/brag-nudge/SKILL.md)

You shipped something real and will never tell anyone. Writes the brag brief — receipts, angles, a rough draft to reword — then nags you to post it. Never posts for you.

### [/prose-revision](./skills/prose-revision/SKILL.md)

A language model's default register is pre-assembled prose. When a human will actually read the thing — docs, PR descriptions, site copy — this is the revision pass: concrete, cut, fresh, shown rather than labelled, and guarded against overcorrecting into telegrams.

### [/answer-first](./skills/answer-first/SKILL.md)

Stop burying the answer. Lead with the outcome, number the steps, park tangents visibly, no ceremony. Descended from [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd) with the lossy rules fixed: tangents are parked instead of dropped, lists are ranked instead of capped, and made-up minute estimates are gone.

## Why so few

Edited, not collected. One skill per scar; when I earn a new scar, there will be a new skill. The two writing skills were used on this repo — the README you are reading went through /prose-revision.

## Who is this

[stumason.dev](https://stumason.dev).

## License

MIT. Steal them, fork them, sand the swearing off, make them yours.
