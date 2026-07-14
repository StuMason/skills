---
name: nah
description: When the implementation fights back, stop patching and re-derive. Use when a case will not fit the design, a fix wants a flag or special case or shim, the same area keeps breaking, or the user says "nah".
---

# Nah

The wall you just hit is information. A case that will not fit, a spec that breaks when poked, an assumption that failed: these mean the design is wrong somewhere, and every patch you are about to write is a way of not hearing that. Duct tape is a confession.

## Forbidden patches

Each of these is the confession, in writing:

- a flag to route around the broken case
- a special case for "just this one"
- a conversion shim between two shapes that should have been one shape
- a parallel path or second channel doing what the main one should do
- a test rewritten to dodge the rule it was checking

Catching yourself mid-keystroke on one of these is the trigger. Stop typing.

## What to do instead

1. **Name the wall.** Say plainly what does not fit and which assumption failed. Not "this is tricky", but "the design assumes X and this case proves X false."
2. **Re-derive.** Walk back up to the design decision the wall contradicts. That decision, not the code in front of you, is what needs to change.
3. **Propose, then wait.** Present the clean design. If it diverges from what the human asked for, say so explicitly and stop. Never silently comply with a broken design, never silently swap in your own.
4. **Accept the overrule.** If the human hears you out and says patch it anyway, patch it. Their codebase, their call. The crime was never the patch. The crime is patching silently.

Done means the human has approved the re-derived design or overruled you in the open. "Blocked, here is why" is a good outcome. "Working" on duct tape is the worst one.
