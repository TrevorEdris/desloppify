# Before / after examples

Each example pairs AI-flavored input with a humanized rewrite. Patterns flagged in the bad version are listed.

---

## Example 1 — promotional / corporate announcement

**Bad** (score ~85, heavily AI-generated):

> Certainly! Here's a comprehensive overview of Acme Analytics' Series B. Acme, a vibrant startup nestled in the heart of Boulder's thriving tech ecosystem, has secured $40M in Series B funding — marking a watershed moment in the company's trajectory. The platform, which leverages cutting-edge AI to deliver robust, seamless analytics, serves as a testament to the team's relentless dedication to innovation, inspiration, and insights.

Patterns flagged:
- M01 chatbot artifact ("Certainly!")
- C04 promotional language ("vibrant", "nestled", "thriving")
- C01 significance inflation ("watershed moment", "trajectory")
- L01 tier 1 vocab cluster (leverages, cutting-edge, robust, seamless, testament)
- L04 copula avoidance ("serves as")
- R02 rule of three ("innovation, inspiration, and insights")
- S01 em dash overuse

**Good** (score ~15, clean):

> Acme Analytics raised a $40M Series B led by Sequoia. The Boulder-based startup makes an observability platform that runs queries in under a second and plugs into existing monitoring stacks. Two enterprise customers, Datadog and Snowflake, beta-tested the platform for six months before the round closed.

Changes: removed chatbot artifact, replaced promotional language with concrete facts, named the lead investor, replaced tier-1 vocab cluster with plain description, broke the rule-of-three.

---

## Example 2 — negative parallelism / rhetorical setup

**Bad** (score ~75):

> Here's the thing: building products isn't just about writing code, it's about understanding your users. Let's dive in. What if I told you that the best teams don't optimize for productivity, they optimize for learning? Full stop.

Patterns flagged:
- Throat-clearing opener ("Here's the thing:")
- R01 negative parallelism ("isn't just X, it's Y" — twice)
- M04 "let's" opener ("Let's dive in")
- R04 rhetorical Q+A ("What if I told you...")
- Emphasis crutch ("Full stop")

**Good** (score ~10):

> Building products is hard. Technology is manageable; people aren't. The best teams I've worked with optimized for learning over productivity, and the data backed them up: their cycle time was 30% slower but their feature retention was 2x higher.

Changes: dropped throat-clearing, dropped both negative parallelisms, replaced rhetorical question with direct claim, removed emphasis crutch, added a concrete metric.

---

## Example 3 — hedging / vague attribution

**Bad** (score ~65):

> Studies show that, in today's fast-paced landscape, organizations could potentially possibly benefit from leveraging cutting-edge frameworks to navigate the complexities of digital transformation. Experts believe this is a pivotal moment in the evolution of enterprise software.

Patterns flagged:
- C05 vague attribution ("Studies show", "Experts believe")
- Opening crutch ("In today's fast-paced landscape")
- L08 excessive hedging ("could potentially possibly")
- L01 tier 1 vocab cluster (leveraging, cutting-edge, navigate, pivotal)
- C01 significance inflation ("pivotal moment in the evolution of")

**Good** (score ~20):

> A 2024 Gartner survey of 1,200 CIOs found 41% had migrated production workloads off SAP in the last 18 months. Most cited license cost, not technical capability, as the trigger.

Changes: replaced vague attribution with named source + specific number, dropped opening crutch, dropped hedging cluster, dropped tier-1 vocab, replaced inflation with bare fact.

---

## Example 4 — chatbot artifacts in a casual reply

**Bad** (score ~50):

> Great question! I'd be happy to help you explore this further. As of my last update, the recommended approach is to leverage a robust framework that serves as a comprehensive solution. Let me break this down for you. I hope this helps! Let me know if you have any other questions.

Patterns flagged:
- M02 sycophancy ("Great question!")
- M01 chatbot artifacts ("I'd be happy to", "I hope this helps", "Let me know")
- M03 cutoff disclaimer ("As of my last update")
- M04 "let's" opener equivalent ("Let me break this down")
- L01 tier 1 vocab (leverage, robust, comprehensive)
- L04 copula avoidance ("serves as")

**Good** (score ~5):

> Use Express. It's the most common Node.js framework and you can find a Stack Overflow answer for any pattern in 30 seconds.

Changes: removed all sycophancy and chatbot scaffolding, dropped cutoff disclaimer, replaced tier-1 vocab with direct recommendation, dropped copula avoidance.

---

## Example 5 — uniform burstiness / paragraph rhythm

**Bad** (score ~55, mostly structural):

> Cloud migration is an important decision for most companies today. Many organizations have successfully moved their infrastructure to the cloud. The benefits include scalability, cost reduction, and improved security. However, there are also significant challenges that must be carefully considered. Companies should evaluate their specific requirements before making this decision. Working with experienced consultants can help ensure a smooth transition.

Patterns flagged:
- S08 sentence-length uniformity (every sentence 11-15 words)
- S07 paragraph uniformity (single block, no rhythm variation)
- L01 tier 1 vocab (significant, scalability, robust)
- R02 rule of three ("scalability, cost reduction, and improved security")
- C08 generic conclusions

**Good** (score ~15):

> Most companies migrate to cloud the wrong way. They lift-and-shift VMs, hit the same cost ceiling on AWS as on-prem, and conclude cloud doesn't work. The companies that win re-architect: drop legacy SQL servers, move to managed services, accept some rewrite cost upfront. Two years in, their bill is half the on-prem TCO. The rest are still paying Azure to run a 2014 monolith.

Changes: varied sentence lengths (4-, 18-, 28-word mix), broke uniformity, replaced generic claim with concrete narrative, dropped rule-of-three list, gave the reader a stake.

---

## Example 6 — null-hypothesis failure (passes surface patterns, fails consistency)

**Bad** (score ~40 surface, ~75 with semantic layer):

> When I joined the engineering team in 2022, I noticed that our deploy pipeline was taking 47 minutes on average, with a P95 of 73 minutes and a P99 of 112 minutes. The team had grown from 8 engineers to 34 over 18 months, and the build infrastructure (originally provisioned for 12 engineers maximum) was struggling. We held weekly retros every Thursday at 2pm where engineers would surface friction points, and the deploy pipeline came up in 11 of the 14 retros that quarter.

Patterns flagged (surface): minimal — clean vocab, no em dashes, varied sentence length.

Null-hypothesis flags:
- Omniscience: exact P95/P99 numbers without claimed source (logs? Datadog? memory?)
- Stacked authenticity signals (specific dates, exact counts, exact percentages)
- Missing knowledge gaps (no "I think", no "around 50 minutes", no "most weeks")
- No mediation ("our pipeline was X" rather than "Datadog showed our pipeline was X")
- Linearity: perfect sequential escalation, no tangent

**Good** (passes both):

> I joined that team in 2022 and the deploys were brutal — sometimes 45 minutes, sometimes pushing 90, depending on whether the test cache hit or not. The team had roughly tripled in 18 months, going from a handful of engineers to over 30. Looking at our build infra in retrospect it was provisioned for the old team size, but at the time none of us thought about it that way. Retros (we ran them weekly, I think on Thursdays) flagged the pipeline constantly. I don't have the exact count anymore but it felt like every other week.

Changes: replaced exact figures with realistic ranges + mediated knowledge ("Looking at... in retrospect"), added genuine uncertainty ("I think on Thursdays", "I don't have the exact count anymore"), introduced tangent ("depending on whether the test cache hit or not"), made the speaker bounded.
