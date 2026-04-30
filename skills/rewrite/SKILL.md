---
description: Rewrite a piece of text to remove AI-isms — em dashes, "not X but Y" parallelism, tier 1/2/3 vocabulary, chatbot artifacts, uniform sentence rhythm, vague attribution. Three-pass system (vocab → structure → texture) with audit recursion. Use when the user wants to publish AI-drafted prose and needs it to sound human, or when prose got flagged by a detector and needs cleanup.
---

# desloppify:rewrite

Rewrite text to remove AI-isms. Output the cleaned version plus a brief summary of changes.

## Inputs

The text to rewrite is whatever the user passes after the slash command.

## Process

### Step 0 — Detect first

Silently run the same detection logic as `/desloppify:detect` (see `../detect/SKILL.md` for the full procedure) to identify what needs fixing. Do not output the detection result; use it to inform the rewrite.

### Step 1 — Decide: patch or full rewrite

Apply the heuristic from `references/rubric.md`:

> If 5+ vocab issues AND 3+ pattern categories are detected, do a full rewrite from scratch. Otherwise, patch.

A full rewrite means: extract the underlying claims and facts, throw out the original prose, write fresh.

A patch means: edit in place, fixing flagged issues while preserving structure.

### Step 2 — Three-pass rewrite

For both patch and full-rewrite paths, apply three passes:

**Pass 1 — Vocabulary**
- Replace every tier-1 word with a plain alternative. See `references/vocabulary.md`.
- Restructure paragraphs containing 2+ tier-2 words.
- Reduce tier-3 word density below 3%.
- Replace banned phrases (chatbot artifacts, opening crutches, throat-clearing, filler) — strip outright if no replacement makes sense.
- Apply char normalization: em dash → period/comma/colon (pick contextually), curly quotes → straight, ellipsis Unicode → three dots.

**Pass 2 — Structure**
- Vary sentence length. Mix 3-5 word sentences with 25+ word sentences. No three consecutive sentences in similar length range.
- Reduce em dashes to zero (target).
- Drop rule-of-three patterns. Use 1, 2, or 4 items instead.
- Vary paragraph weights. Avoid 3-4-sentence-per-paragraph monotony.
- Break trigram repetitions.
- Convert passive voice to active where possible (target ≤ 4% passive).

**Pass 3 — Texture**
- Add contractions in non-academic prose ("don't", "it's", "we're").
- Insert discourse markers where natural ("Look,", "Honestly,", "I think", "Well,").
- Add register shifts — one or two casual asides in formal prose, or a technical term in conversational prose.
- Replace generic claims with specifics (names, dates, numbers, places).
- Add a sentence fragment for emphasis if none exist.
- Show genuine emotional texture; avoid uniform distance from all topics.

### Step 3 — Audit recursion

Re-run detection on the rewritten text. If the new score is still > 25:
1. Identify which patterns survived.
2. Run pass 2 + pass 3 once more, focused on the surviving patterns.
3. Re-detect.

If the second pass still scores > 25, output the best version and note in the summary that further manual editing is recommended. Do not loop indefinitely.

### Step 4 — Null-hypothesis sanity check

Read `references/null-hypothesis.md`. Check the rewritten text for diagnostic absences:
- Are there knowledge gaps where they should be?
- Is uncertainty marked?
- Is knowledge mediated through realistic channels (sources, attribution)?
- Are there tangents, recursion, "wait, I should mention" moments?
- Is the speaker bounded — not omniscient?

If the rewrite still reads as omniscient or perfectly linear, soften specifics into ranges, add an "I think" or "I don't recall exactly", or introduce a bounded source ("the dashboard showed roughly...").

## Output format

```
# desloppify:rewrite

[Rewritten text — clean, no headers, no commentary]

---

## Changes

- Pass 1 (vocab): replaced 12 tier-1 words; stripped 4 chatbot artifacts; normalized 7 em dashes
- Pass 2 (structure): broke sentence-length uniformity (CV 0.16 → 0.34); dropped 2 rule-of-three lists; converted 5 passives to active
- Pass 3 (texture): added 4 contractions, 2 discourse markers, 3 register shifts, 1 sentence fragment for emphasis
- Audit: rescored from 67 to 18 (clean band)

## Strategy

Patch — issues were concentrated in pass 1 and structural rhythm; underlying claims were sound.
```

Always output the rewritten text first (the user's primary need), then change summary.

## What NOT to do

- Do not preserve AI-isms even if the original prose is clear. The user wants them gone.
- Do not change facts, claims, or arguments. Only style.
- Do not add new content unless filling in vague attribution with a placeholder (mark `[source needed]`).
- Do not add sycophancy, chatbot artifacts, or sign-offs in the output. Just deliver the text.
- Do not over-correct into stilted "anti-AI" prose (no em dashes ever; perfectly varied burstiness; mandatory contractions). Natural is the goal.
- Do not mention this is an anti-slop rewrite in the output text itself.

## References

- [`references/patterns.md`](../../references/patterns.md) — 36-pattern taxonomy
- [`references/vocabulary.md`](../../references/vocabulary.md) — tier 1/2/3 word lists
- [`references/phrases.md`](../../references/phrases.md) — banned phrases + char map
- [`references/rubric.md`](../../references/rubric.md) — scoring formula + rewrite-vs-patch heuristic
- [`references/null-hypothesis.md`](../../references/null-hypothesis.md) — consistency framework
- [`references/examples.md`](../../references/examples.md) — before/after pairs
