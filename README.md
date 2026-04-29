# desloppify

Bad AI, no slop.

A Claude Code plugin that detects and removes AI-isms from English prose. Three skills, single ruleset, MIT.

## What it catches

36 patterns across five categories:

- **Content** — significance inflation, vague attribution, promotional language, formulaic challenges, generic conclusions, novelty inflation, notability name-dropping, superficial -ing analyses
- **Language** — tier 1/2/3 AI vocabulary (~110 words), copula avoidance, synonym cycling, template phrases, filler phrases, false ranges, parenthetical hedging, excessive hedging
- **Structure** — em dash overuse, boldface overuse, inline-header lists, title-case headings, emoji decoration, curly quotes, structural uniformity, sentence-length uniformity, trigram repetition, transition phrase clustering
- **Communication** — chatbot artifacts, sycophantic tone, cutoff disclaimers, "let's" openers, signposting, acknowledgment loops
- **Rhetoric** — negative parallelism ("not X but Y"), rule of three, mirror structures, rhetorical Q+A openers

See [references/patterns.md](references/patterns.md) for the full taxonomy with examples.

## Three commands

| Command | Purpose |
|---|---|
| `/desloppify:detect <text>` | Score 0-100, issues grouped P0/P1/P2, no rewriting |
| `/desloppify:rewrite <text>` | 3-pass rewrite (vocab → structure → texture) with audit recursion |
| `/desloppify:audit <text>` | 24-point post-generation checklist, no rewriting |

## Install

### Claude Code (recommended)

```
/plugin marketplace add TrevorEdris/desloppify
/plugin install desloppify@desloppify
```

Then run `/desloppify:detect`, `/desloppify:rewrite`, or `/desloppify:audit` on any text.

## How scoring works

Composite 0-100. Claude estimates three layers:

- **Lexical** (40%) — tier 1/2/3 vocab matches, banned phrases, character signals (em dash, curly quotes, ellipsis Unicode)
- **Structural** (35%) — em dash frequency, paragraph uniformity, rule-of-three count, passive voice density, trigram repetition, sentence-length burstiness
- **Semantic** (25%) — pattern reasoning + null-hypothesis consistency check (lmmx-style: what diagnostic absences should be present?)

Confidence penalties: short samples score lower confidence (`-40` if < 80 words, `-30` if < 4 sentences, `-15` if ≤ 1 pattern category).

Bands:

- **0-25** — clean (green)
- **26-50** — lightly AI-touched (yellow)
- **51-75** — moderately AI-influenced (orange)
- **76-100** — heavily AI-generated (red)

Scores are Claude estimates, not deterministic measurements. A standalone CLI with deterministic stats may follow in a future release.
