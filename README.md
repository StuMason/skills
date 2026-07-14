# Skills

Oi. Everyone has a skills repo now. The calm wizards have theirs, beautifully documented, six figures of stars. This is not that.

Four skills, over a decade of getting burned baked into every one. They are the rules I beat into my own agents after shipping real production systems with them: 20+ apps, a self-hosted estate, AI pipelines, actual clients. Every one of these exists because its absence cost me something.

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

### [/nah](./skills/nah/SKILL.md)

When the implementation fights back, those hands are information. A case that will not fit, a spec that breaks, an assumption that fails: the design is wrong somewhere, and a flag, a special case, or a shim is just a way of ignoring it. This skill makes the agent stop, re-derive the design, and tell you, instead of quietly shipping duct tape. Duct tape is a confession, listen carefully.

### [/oi](./skills/oi/SKILL.md)

The brag nudge. You shipped something real and you will never tell anyone, because people who ship do not stop to market. This skill writes the brag brief for you (receipts, angles, a rough draft to reword) and then nags you to go post it. It never posts for you. Showing up is the one part of marketing you cannot automate, so it automates the nagging instead.

### [/not-ready](./skills/not-ready/SKILL.md)

Vague acceptance criteria are a blocker, not a challenge. If the agent cannot explain the business rule in plain English, it refuses to code it and sends the ticket back with the exact questions that need answers, each with a recommended answer so they actually get answered. Building from guesses makes YOU look shit, not the agent.

### [/you-what](./skills/you-what/SKILL.md)

Never take QA feedback as gospel. QA describes what they see, not what is correct. Before fixing what was reported, this skill makes the agent reproduce it, find the actual source of truth, and deliver a verdict: real bug, misread requirement, or nobody ever decided. "QA said so" is how correct code gets broken politely.

## Why only four

Because these are edited, not collected. Most agent failures I have actually been burned by come down to: it patched around a broken design, it built from a vague ticket, it trusted a wrong bug report, or I shipped something great and told nobody. One skill per scar. When I earn a new scar, there will be a new skill.

## Who is this

[stumason.dev](https://stumason.dev).

## License

MIT. Steal them, fork them, sand the swearing off, make them yours.
