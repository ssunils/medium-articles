# Design

**Subtitle:** OpenAI's Decisions API returns a typed answer in 150ms. The two inputs that shape it are things a PM writes, not things an engineer configures.

**Target reader:** B2B SaaS PM at a 50–200 person company who is about to put a model into a triage, routing, or prioritization path — support tickets, lead scoring, content review, claim severity.

**Key takeaway:** When a model call returns a typed value instead of prose, it stops getting reviewed as a product decision — but the option list you supply and the rubric levels you define still determine the output, and both belong to you.

## Headline options

1. **Reorder Your Choice List, Move the Answer 13 Points**
   *(hook: specific surprising number)*

2. **Your AI Routing Bug Isn't the Model. It's Your Option Order.** — **RECOMMENDED**
   *(hook: contrarian claim challenging a common PM belief)*
   Reason: PMs reflexively treat bad classification as a model-quality problem to be fixed by swapping models or tuning thresholds; the article shows the defect is usually in inputs the PM owns, which is both surprising and actionable.

3. **Can You Say What a 2.6 Out of 4 Means in Your Product?**
   *(hook: sharp question the reader cannot answer confidently)*

## Section outline

- Open on the 150ms / $0.10 typed-answer pitch and the tension: it looks like plumbing
- What shipped (GA date, endpoint, three question types, pricing, batching, Box result)
- The option list is a product decision (order sensitivity, peer-reviewed + the 13-point test)
- A score that lands between your levels (rubric indices, the 2.6 problem)
- Pull-quote
- Why cheap and fast moves the decision out of review (confidence ≠ correctness, the HN debate)
- Practical takeaway (5 concrete actions)

---

# Draft

**Word count: 1091** (target 1000–1400, excluding headings' link syntax)

## Your AI Routing Bug Isn't the Model. It's Your Option Order.

On October 22, OpenAI [made its Decisions API generally available](https://techcrunch.com/2026/10/22/openai-makes-its-jev-competitor-widely-available-as-decision-model-competition-heats-up/). The pitch is unusually narrow: ask a question, get back a typed answer — a probability, a choice from a list you supply, or a score against a rubric — in [roughly 150 milliseconds](https://byteiota.com/openai-decisions-api-typed-answers-10x-faster/), at [$0.10 per million input tokens with output free](https://www.unite.ai/openai-makes-decisions-api-generally-available-with-gpt-6-luna/).

No prose. No parsing. No "sometimes it replies with a preamble."

Which makes it look like plumbing. A typed value, a tenth of a cent, back before the page renders. It reviews like a function call, so it gets reviewed like one.

That's the trap. The two inputs that most shape what comes back are things a product manager writes, not things an engineer configures — and right now, on most teams, nobody owns either of them.

## What actually shipped

The API reached general availability on October 22, after a DevDay preview in late September and a [public beta on October 6](https://smartscope.blog/en/blog/openai-decisions-api-use-pricing-public-beta-october-2026/). It runs on GPT-6 Luna through a dedicated `/v1/decisions` endpoint.

There are [three question types](https://developers.openai.com/api/docs/guides/decisions). A *predicate* returns a probability between 0 and 1 that some condition holds. A *choice* returns one of the values you supplied, along with per-option probabilities and a confidence value. A *score* rates an input against ordered levels, and the result is a probability-weighted average of the level indices.

You can [batch up to 400 questions](https://app.dealroom.co/news/note/openai-opens-decisions-api-to-all-developers-adding-image-input-in-challenge-to-typesafe-s-jev) in a call. OpenAI reports that Box saw [about 5x faster route selection across 30 certificate-of-insurance cases](https://www.unite.ai/openai-makes-decisions-api-generally-available-with-gpt-6-luna/) at the same accuracy as the Responses API, sending lower-confidence cases to human reviewers. The list price lands at [roughly 2.4x rival Jev's](https://fourweekmba.com/ai-openai-opens-decisions-api-at-2-4x-the-price-of-rival-jev/).

The intended uses are exactly the ones PMs have been hand-rolling for two years: classifying content, routing requests, prioritizing work.

## The option list is a product decision

Here is the part that gets skipped.

For a choice question, *you* supply the values. Not just which values — what order they come in. And order is not neutral.

A [2024 NAACL Findings paper](https://aclanthology.org/2024.findings-naacl.130.pdf) found that LLMs are highly sensitive to the sequence in which options are presented, and that calibration methods correcting for it gained up to 8 percentage points across models and benchmarks. One [developer test on this API](https://byteiota.com/openai-decisions-api-typed-answers-10x-faster/) reported that reordering the choice list shifted the model's probability for the correct answer by about 13 points — a single test, not a benchmark, but directionally consistent with the research.

So: `["Tier 1", "Tier 2", "Tier 3"]` and `["Tier 3", "Tier 2", "Tier 1"]` may not route your tickets identically.

Go look for where that list lives in your product. In most codebases it's a literal array inside a service file, written once by whoever built the integration, never reviewed, never versioned, with no owner. It is customer-facing routing logic with less governance than a button label.

## A score that lands between your levels

The score type has a sharper edge.

Because the result is a probability-weighted average of level indices, it can land *between* your levels. Wavect's guidance is blunt about the implication: [define what an intermediate value means before you attach a priority rule to it](https://wavect.io/blog/openai-decisions-api-model-routing/).

Make that concrete. Your severity rubric says 1 is cosmetic, 2 is minor, 3 is major, 4 is critical. The API returns 2.6.

Is that a P2 that's trending ugly? Do you round up, and accept that you just moved a chunk of minor bugs into a 4-hour SLA? Do you round down and eat the misses? Does 2.6 mean the model is confident it's between minor and major, or that it's genuinely torn between a 2 and a 3 — because those are different situations with the same number?

Nobody can answer that from the number alone. It is a product definition, and if you don't write it, a rounding convention in someone's PR will decide it for you.

> You are not configuring a model. You are writing the ballot — and the order of the options is part of the result.

## Cheap and fast moves the decision out of review

The pricing shape matters more than the price.

Free output tokens, 400-question batches, and sub-200ms responses mean you can afford to ask on every single request rather than in a nightly job. That's a genuine capability change. It also quietly relocates judgment calls into the synchronous request path, where your org has no review step — because that path was built for lookups, not opinions.

And the thing the endpoint hands back invites more trust than it has earned. A confidence value is [not a validated probability of correctness](https://wavect.io/blog/anyjev-calibration-option-order-bias/). Whether LLM-reported confidence means anything at all is actively contested: an argument that [using LLMs for confidence scoring is a bad idea](https://rumple.github.io/blog/2026/10/20/asking-llm-for-confidence.html) drew 202 points and 99 comments on Hacker News on October 20, days before GA.

This is early, and I'd treat the calibration question as open rather than settled. But "open" is the point. You are being handed a number that looks like a probability, in a response type that looks like infrastructure, at a price that encourages you to call it everywhere.

## Practical takeaway

Five things to do before this lands in a routing path you're accountable for:

**Find your choice lists.** Grep the codebase for the option arrays feeding any classification call. Move them somewhere with an owner and a version history, and treat changes to them the way you treat changes to user-facing copy.

**Run a rotation test before launch.** Evaluate the cyclic rotations of your K options so each value appears in every position once, then compare the answer distributions — [that's the standard check](https://wavect.io/blog/anyjev-calibration-option-order-bias/) for option-order bias. If rotating the list changes your routing mix, you have a specification bug, not a model bug.

**Write down what a between-levels score means.** Put it in the spec, with the rounding rule and the reasoning, before any priority logic reads the value.

**Log the selected option's probability separately from the confidence value**, and handle refusals, missing fields, and malformed distributions [as errors rather than defaulting them to a business action](https://wavect.io/blog/openai-decisions-api-model-routing/). A failed decision call should not silently become a P3.

**Decide whether this counts as an AI feature in your own governance.** If your company has disclosure rules, review gates, or an AI register, a typed endpoint that routes a customer's ticket belongs in them. The response type changed. The decision didn't.

The useful thing about this API is that it strips the judgment call down to its bare shape — a question, some options, a number. What's left is unmistakably yours.

---

# Hero image

**Status: not verified — no image link presented.**

I could not confirm a usable image. Outbound network access in this environment is restricted to GitHub, so `unsplash.com`, `pexels.com`, and `openverse.org` all refused connections (HTTP 403 at the egress proxy). I could not open any image page to confirm that a specific photo exists, that its direct URL is valid, or what license it carries. Per the brief, I am not presenting an unverified link.

What search results did surface, offered only as leads for a human to check manually — **not as confirmed, usable images**:

- A candidate on Pexels titled "Close-up Photo of Checklist on White Paper," credited in search results to **Nataliya Vaitkevich**, at `pexels.com/photo/close-up-photo-of-checklist-on-white-paper-6837794/`. Existence and license unconfirmed.
- A second candidate described in results as bold "YES"/"NO" typography with checkboxes, on the Pexels `checkbox` search page. Specific photo, photographer, and license all unconfirmed.
- One Unsplash illustration of a ballot box that search results flagged as **Unsplash+**, the paid tier — so it is *not* free for commercial use and should not be used.

On licensing generally: the [Unsplash License](https://medium.com/unsplash/the-unsplash-license-f6fb7de5c95a) permits most commercial and editorial use with no attribution required, excluding resale of unmodified photos and compiling a competing service. Pexels' license also generally waives attribution. Neither statement substitutes for checking the individual photo page, which I could not do.

**Fallback cover-image description (use this to source or commission one):** A clean, overhead editorial shot of a paper form with a short vertical list of unmarked checkboxes, shot at a slight angle in natural light against a muted neutral background, with shallow depth of field so the lower options fall softly out of focus. The list should read as ordered and deliberate — first option crisp, last option blurred — which carries the article's argument that position in a list is doing work. Muted palette, no hands, no screens, no robots, no glowing brains. An abstract alternative: a row of identical small blocks in a single line where one near the front is tipped or offset, suggesting that order, not content, is what differs.

---

# Metadata

**Tags:** Product Management, Artificial Intelligence, AI Product Development, OpenAI, Product Strategy

---

# Unverified claims

- **The ~13-point shift from reordering the choice list.** Attributed in search results to a single developer test written up by ByteIota, not a published benchmark. I could not open the post to confirm the figure, the methodology, or the sample size. The underlying phenomenon of option-order sensitivity is well supported by the [NAACL 2024 Findings paper](https://aclanthology.org/2024.findings-naacl.130.pdf), but treat the specific 13-point number as one person's result.
- **All source pages are unverified against the primary source.** This environment's network policy allows outbound HTTPS to GitHub only; every other host returned 403 at the egress proxy. I could not open `techcrunch.com`, `openai.com`, `developers.openai.com`, `unite.ai`, `wavect.io`, `byteiota.com`, or any other cited page. Every fact here comes from search-result snippets, which I cross-checked across multiple independent outlets where possible. The dates, pricing, latency, and API semantics should be confirmed against OpenAI's own docs and changelog before publication.
- **The GA date of October 22, 2026.** Consistently reported by TechCrunch, Unite.AI, and CellCog, but some outlets still describe the API as being in public beta. Not confirmed against OpenAI's changelog.
- **Latency figures (~150ms, "10x faster than the Responses API").** Vendor-sourced claims repeated by secondary coverage, not independently benchmarked.
- **Pricing ($0.10 per million input tokens, free output, 400-question batches) and the 2.4x-Jev comparison.** From secondary coverage and vendor-adjacent blogs; the batch limit of 400 (up from 200 at beta) appears in only one source.
- **The Box customer result (~5x faster route selection, 30 certificate-of-insurance cases).** A vendor-reported customer outcome relayed by Unite.AI, with a very small case count.
- **The Hacker News post's 202 points and 99 comments.** Taken from an auto-generated third-party digest of HN, not from `news.ycombinator.com` directly, which I could not reach. The post itself is dated October 20, which is outside the 48-hour window; it is cited as context for an ongoing debate, not as today's news.
- **Hero image: no image verified.** See the Hero image section — no license could be confirmed for any candidate, and no link is presented as usable.
