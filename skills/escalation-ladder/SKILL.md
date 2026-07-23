---
name: escalation-ladder
description: Cheapest technique first, LLM last. Use before designing any feature that classifies, matches, routes, dedups, ranks, scores, or extracts — anything where the first instinct is "call the LLM per item". Forces enumeration of deterministic and classical-stats options, with costs and a measurement plan, before a model is allowed in.
---

# Escalation Ladder

The user is not ML-trained and does not need to be. The gate is a question, not knowledge: the model knows the techniques; this skill forces it to put them on the table before reaching for per-item LLM calls. An LLM call per item is the most expensive, least auditable, least debuggable tool in the box — it must be earned, not defaulted to.

## The ladder

Before proposing a design, walk every rung and say explicitly why each is or isn't enough. Name real techniques, explain each in one plain-English sentence (no unexplained jargon), and give per-item cost:

1. **Lookup.** Is the answer already keyed in the data? (IDs, thread keys, foreign keys, container membership.) O(1), free, exact.
2. **Rule.** Does structural metadata decide it? (Headers, flags, sender type, counts, date arithmetic.) Deterministic, explainable in one sentence.
3. **String.** Exact match, normalized match, fuzzy similarity (Jaro-Winkler, trigrams — Postgres pg_trgm counts), regex on bounded vocabularies.
4. **Statistics.** Counting with thresholds: set overlap, IDF weighting, decay formulas, quantile cutoffs, calibration against observed outcomes. Decades-old, tiny code, no training.
5. **Embedding.** Rented vectors + cosine similarity. Cheap per item, fuzzy, needs an index. (Signal already has pgvector.)
6. **Small LLM.** Haiku-class, forced JSON, only on the residual the rungs above couldn't decide — near-ties, genuinely ambiguous cases.
7. **Big LLM.** Last, on the residual of the residual.

The output shape to aim for is a cascade: most traffic dies on rungs 1–4, a minority reaches 5, a sliver reaches 6–7. If the proposal sends 100% of items to rung 6+, that needs a stated justification, not a shrug.

## The three questions that do the work

- **"What is the dumbest thing that gets 80%?"** Design that first, measure it, then decide if the remaining 20% is worth a model.
- **"Where are the free labels?"** Find ground truth already lying in the domain (items whose answer is structurally known) — that's the eval set and the threshold calibrator, at zero labelling cost. Mask the known answer, run the pipeline, grade it.
- **"What does each rung cost at 10x volume?"** Per-item cost and latency, stated per rung, before choosing.

## Rules

1. **Enumerate before designing.** The ladder table (rung → applicable technique → plain-English explanation → cost → expected coverage) comes before any code or schema.
2. **Every technique gets one plain sentence.** "Platt scaling — fitting an S-curve to past right/wrong answers so a raw score becomes an honest probability." If it can't be explained in a sentence, it can't be maintained here.
3. **A measurement plan is part of the design.** How will we know the cheap rung is good enough — what's the free-label source, what number decides escalation? No number, no next rung.
4. **Thresholds are derived, not invented.** Prefer quantiles of observed data over hand-picked magic constants; if a constant is hand-picked, mark it as provisional in a comment.
5. **LLM output on the hot path is constrained.** Forced JSON, choices limited to an offered candidate set, out-of-set answers treated as "no decision" — never free text parsed hopefully.

## When to break it

- Genuinely generative work (writing prose, summarising a document) starts at the LLM rung; the ladder is for *decisions* about items, not for producing content.
- A throwaway spike for a demo can skip the enumeration — but say so, and don't let the spike become the design.
- When the volume is tiny and fixed (tens of items, ever), rung 6 first is fine; the ladder pays off at pipeline scale.
