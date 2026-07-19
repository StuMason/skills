---
name: brag-nudge
description: The brag nudge. Use when something real has just shipped, a PR train merged, a deploy gone live, a project delivered. Writes a brag brief and nags the human to go post about it.
---

# Brag Nudge

The human just shipped something real. They will never tell anyone, because people who ship do not stop to market. So the agent does the thinking and the human does the human bit. **Never post on their behalf. The nudge is the product.**

## When it fires

Something real shipped: a merged PR train, a production deploy, a delivered project. One brief per shipped thing. The test for brag-worthy: would someone who might *hire* this person find it impressive? Devs being impressed is nice. Buyers being impressed is the point.

## The brief

Write to `brags/YYYY-MM-DD-<slug>.md` in the project or workspace:

```markdown
# Go brag: <headline of what shipped>

<Two or three sentences of nudge. Direct, cheeky, "go brag about this, mate"
energy. Say why it is impressive TO A BUYER, not to a dev.>

## Receipts
- <Verified facts only. Pull real PR counts, real dates, real features live.
  Never invent a number. No metric available means a qualitative receipt.>

## Angles
- **LinkedIn (buyer frame):** <the business implication: speed, cost, risk,
  delivery capacity>
- **X (peer frame):** <the technical war story or gotcha>
- **Video:** <yes or no, and the beat if yes>

## Rough draft, REWORD ME, do not post as-is
<One rough post draft in the human's voice. Deliberately rough. Editing a
wrong draft beats staring at a blank box.>
```

## The nudge

Deliver it however this environment reaches the human: a notification hook, a messaging tool, or simply ending the session with the headline and the file path in your final message. Loud beats polite.

## Rules

- Receipts must be verifiable. Check the numbers before writing them down.
- Posts are public. No client names, no internal hostnames, no secrets, nothing the human has not already published.
- Never post, schedule, or auto-publish anything. The human rewords and posts by hand. Showing up is the one part of marketing that cannot be automated, so automate the nagging instead.
