# Pattern taxonomy

36 patterns across 5 categories.

Severity: P0 = credibility killer; P1 = obvious AI smell; P2 = stylistic polish.

## Content (8)

### `C01` Significance inflation (P0)

Replaces concrete details with grandiose language.

- Bad: `marking a pivotal moment in the company's trajectory`
- Good: `was founded in 2019`
- Fix: Replace the framing with a concrete fact (date, number, name, place).

### `C02` Notability name-dropping (P0)

Vague publication or authority credits without specifics.

- Bad: `cited in NYT, BBC, and Wired`
- Good: `In a 2024 NYT interview, she argued...`
- Fix: Cite the specific source with date or quote, or remove.

### `C03` Superficial -ing analyses (P2)

Present participles tacked on for false depth.

- Bad: `highlighting, underscoring, symbolizing the importance of...`
- Good: `Replace with a concrete fact or analysis`
- Fix: Remove or expand into a real claim with evidence.

### `C04` Promotional language (P0)

Tourism-brochure adjectives inflating mundane subjects.

- Bad: `nestled within the breathtaking region`
- Good: `is a town in the Gonder region`
- Fix: Drop the adjectives, state the bare fact.

### `C05` Vague attributions (P0)

Unsourced claims without named sources.

- Bad: `Experts believe... / Studies show...`
- Good: `According to a 2019 Gartner survey...`
- Fix: Name the source or remove the claim.

### `C06` Formulaic challenges (P1)

Generic obstacle-then-triumph narrative structure.

- Bad: `Despite challenges... continues to thrive`
- Good: `Cut staff 30% in 2023 but kept revenue flat`
- Fix: Name the specific issue and concrete response.

### `C07` Novelty inflation (P2)

Treats established concepts as fresh discoveries.

- Bad: `He introduced a term I hadn't heard before`
- Good: `He explained how the term works`
- Fix: Drop the implied novelty; state the substance.

### `C08` Generic conclusions (P2)

Hollow ending statements with no commitments.

- Bad: `The future looks bright. Only time will tell.`
- Good: `Q3 launch is the next milestone.`
- Fix: Replace with a specific plan or fact.

## Language (8)

### `L01` AI vocabulary (tier 1) (P1)

Always-replace words from tier 1 vocabulary list.

- Bad: `We delve into the robust, comprehensive landscape`
- Good: `We look at the system`
- Fix: Replace with plain alternatives. See references/vocabulary.md.

### `L02` AI vocabulary (tier 2 cluster) (P2)

Tier 2 words flagged when 2+ appear in same paragraph.

- Bad: `The platform navigates a paramount, multifaceted ecosystem`
- Good: `The platform handles three teams`
- Fix: Restructure paragraph; replace at least one tier-2 word with plain alternative.

### `L03` AI vocabulary (tier 3 density) (P2)

Tier 3 words flagged when density exceeds 3% of total words.

- Bad: `significant, important, vital, critical, essential, key results`
- Good: `Cut latency 40%`
- Fix: Reduce density; pick the strongest single word.

### `L04` Copula avoidance (P2)

Replaces simple is/has with awkward constructions.

- Bad: `serves as / boasts / features / functions as`
- Good: `is / has`
- Fix: Use plain copulas.

### `L05` Synonym cycling (P1)

Repeats the same concept with different words to avoid repetition.

- Bad: `developers... engineers... practitioners... builders`
- Good: `developers (consistent)`
- Fix: Pick one term and use it consistently.

### `L06` Template phrases (P1)

Formulaic constructions with interchangeable slots.

- Bad: `[adjective] step towards [adjective] infrastructure`
- Good: `Reduced cold-start latency from 800ms to 120ms`
- Fix: Describe the actual outcome with specifics.

### `L07` Filler phrases (P1)

Verbal padding with no information.

- Bad: `In order to / Due to the fact that`
- Good: `To / Because`
- Fix: Cut the filler. See references/phrases.md.

### `L08` Excessive hedging (P2)

Stacked qualifiers that defer commitment.

- Bad: `could potentially possibly arguably`
- Good: `may`
- Fix: Pick one hedge or commit to the claim.

## Structure (10)

### `S01` Em dash overuse (P1)

Em dashes are the #1 surface signal of AI text.

**Threshold**: Target zero. Flag at >1 per 1000 words.

- Bad: `institutions—not the people—yet this continues—`
- Good: `institutions, not the people. This continues.`
- Fix: Replace each em dash with comma, period, parens, or colon.

### `S02` Boldface overuse (P1)

3+ bolded phrases in short text signals scanned/listicle output.

- Bad: `**OKRs**, **KPIs**, **BMC**`
- Good: `OKRs, KPIs, BMC`
- Fix: Drop bold; let strong content carry weight.

### `S03` Inline-header lists (P1)

**Header:** definition repeated in prose context.

- Bad: `**Performance:** Performance improved by...`
- Good: `Performance improved...`
- Fix: Convert to flowing prose.

### `S04` Title case headings (P2)

Every Main Word Capitalized.

- Bad: `Strategic Negotiations And Partnerships`
- Good: `Strategic negotiations and partnerships`
- Fix: Use sentence case for headings.

### `S05` Emoji decoration (P1)

Emojis in headers or professional prose.

- Bad: `🚀 Launch Phase: 💡 Key Insight:`
- Good: `Launch Phase: Key Insight:`
- Fix: Remove emojis.

### `S06` Curly quotes / Unicode chars (P1)

Smart quotes, en/em dashes, ellipsis Unicode.

- Bad: `“quoted” — word …`
- Good: `"quoted" - word ...`
- Fix: Normalize to ASCII via char map (see references/phrases.md).

### `S07` Structural uniformity (P2)

Same-length paragraphs throughout, predictable openings.

- Bad: `Six paragraphs, all 3-4 sentences, all opening with thesis sentence`
- Good: `Mixed: 1-sentence, 6-sentence, mid-thought-opener, etc.`
- Fix: Vary paragraph weight and opener strategy.

### `S08` Sentence-length uniformity (low burstiness) (P1)

AI clusters sentences in 15-25 word range. Humans swing 3-40.

- Bad: `All sentences 18-22 words`
- Good: `Mix 4-word punches with 30-word flowing sentences`
- Fix: Break monotony with very-short and very-long sentences.

### `S09` Trigram repetition (P2)

Same 3-word phrase recurring.

- Bad: `the platform provides... the platform provides...`
- Good: `Vary phrasing`
- Fix: Detect repeated trigrams; rewrite at least one.

### `S10` Transition phrase clustering (P2)

Furthermore / Moreover / Additionally bunched together.

- Bad: `Furthermore... Moreover... Additionally...`
- Good: `Drop most; use one if necessary`
- Fix: Limit one transition word per 500 words.

## Communication (6)

### `M01` Chatbot artifacts (P0)

AI assistant filler that leaks into output.

- Bad: `I hope this helps! Let me know if...`
- Good: `Remove entirely.`
- Fix: Strip; never include in shipped prose.

### `M02` Sycophantic tone (P1)

Excessive validation.

- Bad: `Great question! You're absolutely right!`
- Good: `(remove)`
- Fix: Drop. Respond directly.

### `M03` Cutoff disclaimers (P0)

Knowledge-cutoff statements visible to reader.

- Bad: `As of my last update / While details are limited in available sources`
- Good: `(remove)`
- Fix: Strip entirely; or find the source.

### `M04` "Let's" openers (P1)

Indirect framing via collective voice.

- Bad: `Let's dive in / Let's break this down / Let's explore`
- Good: `Start with the content`
- Fix: Drop the meta-narration; deliver the content directly.

### `M05` Signposting announcements (P1)

Telling reader what's coming instead of saying it.

- Bad: `Here's what you need to know...`
- Good: `(deliver the content)`
- Fix: Cut announcement; state the content.

### `M06` Acknowledgment loops (P2)

Restating user's question before answering.

- Bad: `To answer your question about...`
- Good: `(answer directly)`
- Fix: Skip the acknowledgment; answer.

## Rhetoric (4)

### `R01` Negative parallelism (P0)

"It's not X, it's Y" framing — the canonical AI tell.

- Bad: `It's not just a tool, it's a movement`
- Good: `It's a movement`
- Fix: State the point directly. Drop the negation setup.

### `R02` Rule of three (P1)

Forced triads when 1, 2, or 4 items would be natural.

- Bad: `innovation, inspiration, and insights`
- Good: `innovation and inspiration`
- Fix: Use the natural number of items, not always three.

### `R03` Mirror structures / dramatic fragmentation (P1)

Identical syntactic shapes for emphasis; staccato triplets.

- Bad: `[Noun]. That's it. / No X. No Y. Just Z.`
- Good: `Use complete sentences.`
- Fix: Drop fragmentation; write a complete sentence.

### `R04` Rhetorical Q+A openers (P1)

Question posed then immediately answered.

- Bad: `What if there were a better way? Turns out, there is.`
- Good: `There is a better way: ...`
- Fix: Drop the rhetorical question; deliver the claim.
