---
name: ticket-readiness
description: Vague acceptance criteria are a blocker, not a challenge. Use before building from any ticket, issue, or request that is ambiguous about business logic or expected behaviour.
---

# Ticket Readiness

If you cannot explain the business rule in plain English, refuse to code it. Building from guesses produces confident, plausible, wrong code, and the human carries it into review with their name on it.

## The readiness check

Before writing any code from a ticket, check:

- **Concrete expected behaviour.** For the main path and each edge the ticket touches, can you state what the user sees? "Needs to be fleshed out" anywhere in a ticket is an automatic fail.
- **Every decision named.** No "somehow", no "appropriately", no "as needed" standing in for a business rule.
- **Money gets specifics.** Financial or payment work must name the exact account, the exact flow, the exact mechanism. "The company bank account" is not specific enough. If you cannot say which account and why it is the right one, you do not know enough to write the code.
- **The plain-English test.** Say the business rule out loud in one sentence. If you cannot, you have not understood it, and neither has the ticket.

## When it fails

Do NOT build the parts you understand and guess the rest. Stop and send it back:

1. Tell the human plainly: this ticket is not ready for dev.
2. Produce the not-ready list: one line per gap, each phrased as a specific, answerable question. "What happens when the booking is cancelled after payment?" not "please clarify cancellations."
3. Where you have a recommended answer, include it. Questions with recommendations get answered fast. Bare questions get ignored.
4. Wait. Do not start a "safe subset" while waiting; the answers usually change the design.

Pushing back feels expensive and is not. Asking the obvious question costs a minute. Shipping the wrong thing costs the failed QA round, the review, and the rework. Be the one who asks.
