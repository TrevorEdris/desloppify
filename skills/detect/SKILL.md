---
description: Score a piece of text for AI-isms (em dashes, "not X but Y" parallelism, tier 1/2/3 vocabulary, chatbot artifacts, burstiness, etc.). Returns a 0-100 composite score with issues grouped by P0/P1/P2 severity. No rewriting. Use when the user wants to know how AI a piece of writing reads, audit a draft before publishing, or scan prose without altering it.
---

# desloppify:detect

Detect AI-isms in prose. Output a composite score and a list of flagged issues. Do not rewrite.

## Inputs

The text to scan is whatever the user passes after the slash command. If they paste multi-paragraph prose, score the whole thing as one document.

## Process

Run three layers of detection in order, then combine.

### Layer 1 — Lexical (40% of composite)

Pattern-match the text against the lexical catalog:

- Tier 1 vocabulary (`references/vocabulary.md`): every occurrence is a P1 issue.
- Tier 2 vocabulary: flag when 2+ words appear in the same paragraph. P2 issue per cluster.
- Tier 3 vocabulary: estimate density across the whole text. If density > 3%, flag as a single P2 issue.
- Banned phrases (`references/phrases.md`): every match is a P0 or P1 depending on category (chatbot artifacts and opening crutches are P0; throat-clearing, filler, meta-commentary, fake authenticity, formulaic constructions, business jargon are P1; vague declaratives and adverbs are P2).
- Char signals: count em dashes, en dashes, curly quotes, ellipsis Unicode. Flag each char-normalization issue as P1.

For each lexical issue, record:
- Pattern id (e.g. `L01`, or phrase category)
- Severity (P0/P1/P2)
- Location (line:col estimate, or character offset)
- The matched substring
- A suggested fix from the catalog

### Layer 2 — Structural (35% of composite)

Estimate (you cannot compute these deterministically, but produce reasoned estimates):

- Em dash frequency per 1000 words. Compare against thresholds in `references/rubric.md`.
- Sentence-length burstiness — coefficient of variation (stddev / mean of sentence-word-counts). CV < 0.15 is highly suspicious; CV ≥ 0.30 is natural.
- Paragraph-length CV — < 0.20 is suspicious uniformity.
- Trigram repetition — % of 3-word phrases that appear 2+ times. ≥ 5% is suspicious.
- Passive voice density — % of sentences. 8-12% high risk; 2-4% typical human.
- Rule-of-three frequency — count of 3-item lists per 500 words; flag if ≥ 3.

Each structural finding is P1 or P2 depending on severity.

### Layer 3 — Semantic + null-hypothesis (25% of composite)

Read `references/patterns.md` for the 36-pattern taxonomy. Look for patterns that escape pure regex matching:

- Negative parallelism ("not X but Y") — R01, P0
- Mirror structures and dramatic fragmentation — R03, P1
- Rhetorical Q+A — R04, P1
- Significance inflation — C01, P0
- Promotional language — C04, P0
- Vague attribution — C05, P0
- Formulaic challenges — C06, P1
- Synonym cycling — L05, P1
- Template phrases — L06, P1

Then read `references/null-hypothesis.md` and assess the text against the 12 consistency categories. Pay special attention to **diagnostic absences** — missing uncertainty hedging, missing attribution, missing knowledge gaps, missing tangents, omniscience without bounded expertise. A text can pass surface patterns and still fail consistency.

## Composite scoring

Combine layer outputs with weights from `references/rubric.md`:
- 40% lexical
- 35% structural
- 25% semantic

Apply confidence penalties:
- < 80 words: -40
- < 4 sentences: -30
- ≤ 1 pattern category hit: -15

Clamp 0-100.

Map to a band:
- 0-25 clean (green)
- 26-50 lightly AI-touched (yellow)
- 51-75 moderately AI-influenced (orange)
- 76-100 heavily AI-generated (red)

## Output format

```
# desloppify:detect

**Score**: 67/100 — moderately AI-influenced (orange)

**Layer breakdown**:
- Lexical: 28/40 (12 tier-1 hits, 1 tier-2 cluster, 5 banned phrases, 4 em dashes)
- Structural: 22/35 (CV=0.18, paragraph CV=0.15, 7% passives, 4 em dashes/1k)
- Semantic: 17/25 (3 negative parallelisms, 1 rule-of-three, omniscience flag)
- Confidence: full sample, no penalty

## Issues

### P0 (4)
- L:12 `In today's fast-paced landscape` — opening crutch — drop entirely
- L:18 `It's not just a tool, it's a movement` — R01 negative parallelism — state the point directly
- L:22 `Studies show` — C05 vague attribution — name the source
- L:30 `As of my last update` — M03 cutoff disclaimer — strip

### P1 (9)
- L:5 `delve` — L01 tier-1 vocab — replace
- L:7 — em dash — replace with comma/period/colon
- ...

### P2 (3)
- L:14 `actually, simply, just` — adverb cluster — drop
- ...
```

Always show the score first, then layer breakdown, then issues grouped by severity. Always sort issues by severity (P0 → P1 → P2) then by location.

## What NOT to do

- Do not rewrite the text. Use `/desloppify:rewrite` for that.
- Do not invent statistics — say "estimated" if you cannot compute exactly.
- Do not flag patterns that aren't present. False positives erode trust.
- Do not mention this is an AI-detection skill in the output. The user knows.

## References

- [`references/patterns.md`](../../references/patterns.md) — 36-pattern taxonomy
- [`references/vocabulary.md`](../../references/vocabulary.md) — tier 1/2/3 word lists
- [`references/phrases.md`](../../references/phrases.md) — banned phrase enumerations
- [`references/rubric.md`](../../references/rubric.md) — scoring formula + thresholds
- [`references/null-hypothesis.md`](../../references/null-hypothesis.md) — consistency framework
- [`references/examples.md`](../../references/examples.md) — before/after pairs
