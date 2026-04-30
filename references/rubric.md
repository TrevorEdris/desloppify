# Scoring rubric

Composite 0-100 score with confidence penalties.

## Composite score

- Lexical layer: 40%
- Structural layer: 35%
- Semantic + null-hypothesis layer: 25%

## Confidence penalties (subtractive)

- Sample < 80 words: -40 pts
- Sample < 4 sentences: -30 pts
- ≤ 1 pattern category hit: -15 pts

Final score clamped 0-100.

## Bands

| Band | Score | Color |
|---|---|---|
| clean | 0-25 | green |
| lightly AI-touched | 26-50 | yellow |
| moderately AI-influenced | 51-75 | orange |
| heavily AI-generated | 76-100 | red |

## Quantified structural thresholds

### Em dashes (per 1000 words)

- High risk: 5+
- Medium risk: 2-4
- Human target: 0

### Passive voice (% of sentences)

- High risk: ≥ 8.0%
- Medium risk: 4.0-8.0%
- Human typical: ≤ 4.0%

### Burstiness (sentence-length CV = stddev / mean)

- Highly suspicious: CV < 0.15
- Moderate: CV 0.15-0.25
- Natural human: CV ≥ 0.3

### Paragraph uniformity

- High risk: paragraph word-count CV < 0.2

### Trigram repetition

- High risk: ≥ 5.0% of trigrams repeat

### Rule of three

- Flag if ≥ 3 3-item lists per 500 words

## Rewrite-vs-patch heuristic

When **5+ vocab issues** AND **3+ pattern categories** are detected, do a full rewrite from scratch instead of patching individual issues.

## 24-point post-generation audit checklist

Source: paraphrased from adenaufal/anti-slop-writing.

### Vocabulary (5)

1. Search/replace every tier-1 word.
2. Remove constructions like "serves as", "stands as", "is a testament to", "highlights the importance of".
3. Eliminate vague attributions or name specific sources.
4. Delete fake authenticity signals.
5. Remove chatbot artifacts.

### Structure (8)

6. Break any sequence of 3+ sentences with similar length.
7. Add or remove items from any list with exactly three items.
8. Rewrite openings that begin with temporal framing ("In today's world").
9. Delete redundant restatements at paragraph ends.
10. Convert -ing participial phrases tacked to sentences into separate sentences or remove.
11. Count em/en dashes — target zero. Replace with commas, parens, colons, periods.
12. Replace semicolons in non-academic prose with periods or conjunctions.
13. Eliminate staccato triplets ("No X. No Y. Just Z.").

### Sentence variety (4)

14. Add at least one question or fragment if text is all declarative.
15. Rewrite paragraph openings that all start with thesis statements; begin some mid-thought.
16. Mix very short (3-5 words) and very long (25+ words) sentences.
17. Rewrite if more than two consecutive passive constructions appear.

### Voice (7)

18. Add 2-3 register shifts (casual aside in formal prose, technical term in conversational text).
19. Read aloud; AI rhythm is audible where invisible on screen.
20. Add contractions naturally in non-academic prose.
21. Insert discourse markers ("Well", "Look", "I think", "Honestly") where contextually appropriate.
22. Show genuine emotional texture; avoid uniform distance from all topics.
23. Add at least one sentence fragment for emphasis if none exist.
24. Replace generic claims with specifics (names, dates, numbers, places).
