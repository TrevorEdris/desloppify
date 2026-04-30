---
description: Run a 24-point post-generation audit checklist against text. Each item marked pass / fail / needs-review. No rewriting. Use when the user has already drafted prose and wants a structured pre-publish review focused on AI-isms, voice, and rhythm.
---

# desloppify:audit

Run a 24-point checklist against the user's text. Mark each item pass / fail / needs-review. Do not rewrite.

## Inputs

The text to audit is whatever the user passes after the slash command.

## Process

Read `references/rubric.md` for the full 24-point checklist. Walk through each item, evaluate the text against it, and mark:

- **PASS** — item satisfied
- **FAIL** — item violated; quote the offending span
- **REVIEW** — borderline; flag for human judgment

Group findings by checklist section: vocabulary (5), structure (8), sentence variety (4), voice (7).

## Output format

```
# desloppify:audit

**Result**: 17/24 pass, 5 fail, 2 review

## Vocabulary (5)

1. ✓ Search/replace every tier-1 word
2. ✗ Remove constructions like "serves as", "stands as", "is a testament to"
   - L:5 `the platform serves as a comprehensive analytics layer`
3. ✗ Eliminate vague attributions or name specific sources
   - L:12 `Studies show...`
4. ? Delete fake authenticity signals — REVIEW: "Honestly, I think" reads natural; verify intent.
5. ✓ Remove chatbot artifacts

## Structure (8)

6. ✗ Break any sequence of 3+ sentences with similar length
   - All sentences in para 2 are 14-17 words
...

## Sentence variety (4)

...

## Voice (7)

...

## Summary

Top 3 fixes to prioritize:
- Replace tier-1 vocab cluster in para 1 (items 1-2)
- Add a knowledge gap or hedge to para 3 (item 22)
- Vary sentence length in para 2 (item 6, 16)
```

Always show the result count first, then the section-by-section walkthrough, then a 3-item prioritized fix list.

## What NOT to do

- Do not rewrite. Only audit.
- Do not score 0-100. The audit checklist is binary per item; use `/desloppify:detect` for a composite score.
- Do not mark items as PASS without checking. If you're not sure, mark REVIEW.
- Do not pad PASS items with congratulatory commentary. One symbol + checklist text is enough.
- Do not invent items not in the 24-point checklist. The list is fixed.

## References

- [`references/rubric.md`](../../references/rubric.md) — full 24-point checklist
- [`references/vocabulary.md`](../../references/vocabulary.md) — tier 1/2/3 word lists (for item 1)
- [`references/phrases.md`](../../references/phrases.md) — banned phrases (for items 2, 3, 4, 5, 8, 13)
- [`references/null-hypothesis.md`](../../references/null-hypothesis.md) — voice consistency (for items 18-22)
