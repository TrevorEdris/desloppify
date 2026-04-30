# Null-hypothesis consistency framework

A semantic-layer detection technique that complements pattern matching. **Diagnostic absences** carry as much signal as **suspicious presences**.

Paraphrased from the lmmx "AI tells rubric" gist. The original framework treats AI text as text optimized for *seeming* authentic rather than text produced by an authentic process.

## Core question

> Is this text consistent with its claimed authorship?

Establish what should be present and what should be absent given the author's claimed context. Then check the text against both.

## Twelve diagnostic categories

### 1. Voice and perspective
- Lacks a situated speaker with stakes
- Exhibits "view from nowhere" — no visible motivation or learning process
- Missing register oscillation (tone stays uniform)
- No indication of personal investment

### 2. Epistemic texture
- Uniform confidence across all domains (humans modulate: certain on fundamentals, hedging on frontiers)
- Zero epistemic humility — never admits knowledge gaps
- Missing genuine uncertainty markers ("I think", "from what I understand", "it's unclear")
- Pseudo-hedges that intensify ("essentially", "literally", "actually") rather than qualify

### 3. Grammatical / sentence-level
- Nominalization heavy
- Free-floating agency (subjects without clear actors)
- Colon-list elisions instead of explained causation
- Heavy "to be" reliance with nested conceptual dependencies
- Minimal participial / ablative constructions

### 4. Structural organization
- Symmetric load-balancing (equal-length sections regardless of importance)
- Throat-clearing openers
- Rigid academic scaffolding
- Artificial Q&A structures
- Restated significance at ending

### 5. Intensification
- Adverb inflation
- Verb upgrading ("discovered" instead of "observed")
- Cliché reaching
- Dramatic fragments for artificial emphasis
- Qualifier stacking

### 6. Pedagogical failures
- Misallocated explanation depth
- Misleading analogies that don't actually map
- Definition-list interruptions
- Pseudo-runnable code (uncanny valley)
- Adversarial framing ("you thought X, but actually Y")

### 7. Social and contextual blindness
- Context-free knowledge presentation
- Dead references (equations without source)
- Authority borrowing without earning
- Absence of communication mediation ("my manager told me", "the wiki says")

### 8. Parenthetical tells
- AI parentheticals: only clarify definitions or evidence
- Human parentheticals: asides, tangents, self-corrections, associative jumps
- Diagnostic: **absence** of associative human-style parentheticals

### 9. Meta-level tells
- Text optimized for production, not consumption
- No positioned stakes about why this matters
- Explanations exist without underlying purpose

### 10. Tense and immediacy
- False present-tense urgency
- Context collapse (present tense even after author claims to have left)
- Rapid recovery to present after unavoidable past-tense passages

### 11. Linearity
- Perfect sequential escalation, no recursion
- Missing "oh and another thing" moments
- No tangents, no flagged narrative reordering ("wait, I should mention")
- Diagnostic: **absence** of non-linear thought

### 12. Omniscience problem (most diagnostic)
- Cross-team knowledge exceeding realistic access
- Exact figures without sources
- Both system internals AND strategic reasoning, with no bounded expertise
- Absence of "I don't know" admissions

## How to apply

Two passes when scoring text:

**Suspicious presences**:
- Omniscience, perfect structure, uniform confidence, stacked authenticity signals, clean prose under impaired states, uniformly intense language

**Suspicious absences**:
- Uncertainty hedging, attributed speech, errors matching claimed state, knowledge gaps, tangential thinking, situated speaker, associative parentheticals

Either pass can flag P0 / P1 / P2 issues independently of vocabulary or punctuation patterns.

## Why this matters

Pattern-matching on em dashes, banned words, and rhythm catches surface tells. The null-hypothesis framework catches text that has been carefully rewritten to *avoid* surface tells but still reads as AI-generated because the deeper structure (omniscience, uniform confidence, missing hedges, no tangents) gives it away.

A text can pass all 36 surface patterns and still fail the null-hypothesis test.
