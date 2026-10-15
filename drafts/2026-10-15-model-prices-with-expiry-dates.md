# Design

**Subtitle:** Gemini 4 Argon launched at $2 per million input tokens and doubles on December 1. The number in your margin model may be an offer, not a price.

**Target reader:** A B2B SaaS PM at a 50–200 person company who owns the gross margin on a shipped or about-to-ship AI feature, and who picked a model in the last quarter.

**Key takeaway:** Model list prices increasingly ship with expiry dates, so "what does this cost" is now two questions — what it costs today and what it costs after the promotional window — and the second one is the one your margin model needs.

**Section outline:**
1. Open on the two numbers in one launch post
2. The expiry date was announced at launch, not later
3. Why the 95% cache discount doesn't protect you
4. Why you can't engineer around it the usual way (implicit caching only)
5. Not every vendor ships a clock — the contrast case
6. What this changes for a PM: four decisions
7. Practical takeaway
8. The honest limits of this

**Headline options:**

1. **Google's $2 Model Becomes a $4 Model on December 1** — *(hook: specific number and date)* — **RECOMMENDED** — it names the exact change and date, which is the whole reason to read today, and the article pays it off with the vendor's own pricing table rather than a prediction.

2. **The Model Price in Your Margin Model Isn't a Price** — *(hook: contrarian claim challenging a common PM belief)* — good for readers who don't use Gemini, but less urgent.

3. **Which of Your Model Prices Expire Before Your Launch?** — *(hook: a sharp question most PMs can't answer confidently)* — strong curiosity, but slightly softer than naming the date.

---

# Draft

Google shipped Gemini 4 Argon to general availability on October 13 at $2 per million input tokens and $10 per million output tokens. On December 1, the same model costs $4 and $20.

Both numbers are in [the launch post](https://cloud.google.com/blog/products/ai-machine-learning/gemini-4-argon-available-on-google-cloud). Not a leak, not a later revision — the price increase was published in the same paragraph as the launch.

That is worth sitting with for a second, because it changes what a model price is.

## The clock shipped with the product

Argon is available now through the API as `gemini-4-argon`, plus AI Studio, Antigravity, and Gemini for business, [per Google's announcement](https://cloud.google.com/blog/products/ai-machine-learning/gemini-4-argon-available-on-google-cloud). The introductory rate of $2 input and $10 output runs through November 30, 2026. After that, standard pricing applies.

Google's [pricing table](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) carries this as two separate rows for the same model: one labelled through November 30, 2026 at $2 input on the global endpoint, and one effective December 1, 2026 at $4. Non-global endpoints run slightly higher in both windows — $2.20 now, $4.40 later.

So if you evaluated Argon in the last two days, benchmarked it, liked the cost-per-task, and put that figure into a margin model, your margin model has six weeks of life left.

This is not a Google problem. It is becoming the default way models launch. Third-party pricing trackers now list [several Gemini Flash tiers on introductory rates through December 31, 2026](https://tokencost.app/blog/llm-api-price-increases-2026), doubling on January 1 — though I could not verify those against Google's own pages, so treat them as a prompt to go look rather than a fact.

## The cache discount doubles too

Here is the part that caught me.

Argon prices cached input tokens at 95% off. That sounds like insurance — if your workload is cache-heavy, surely the discount absorbs the increase?

It doesn't, because 95% off is a percentage of the input price. Google's pricing table lists cached input at $0.10 per million through November 30 and $0.20 from December 1 on the global endpoint. The discount survives. The number it applies to doesn't.

> The 95% stays. What it's 95% of is what changes.

If you built your cost case on a high cache-hit rate, you didn't hedge the price increase. You just scaled it down by a constant and kept the same exposure.

## The usual engineering lever is narrower than you think

The normal response to a model price rise is to engineer around it: cache harder, trim prompts, route cheap work to a cheap model.

With Argon, the caching lever is partly out of your hands. Google's developer documentation says Argon [supports implicit caching only](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-4-argon), with a 6,144-token minimum shared prefix and durable caching on by default. Explicit context caching isn't supported.

Practically: you don't call a cache API and manage entries. You earn the discount by putting static content at the front of the prompt and keeping that prefix long enough and stable enough to hit. That is a prompt-layout decision, which means it lives with whoever owns your prompt templates — and it's the kind of thing that silently stops working when someone personalises a system prompt.

Worth checking before December, not after.

## Not every price has a clock

The useful contrast is that this isn't universal.

[Claude's pricing page](https://claude.com/pricing) lists Sonnet 5.5 at $2 input and $10 output per million tokens with no promotional framing and no expiry date attached. Haiku 5.5 sits at $0.10 and $0.50 for prompts up to 100K tokens. Cache reads on Sonnet 5.5 are $0.10 per million — a rate Anthropic [halved on October 7](https://siliconangle.com/2026/10/07/anthropic-releases-claude-haiku-5-5-small-model-and-halves-sonnet-5-5-cache-read-prices/), moving in the opposite direction in the same month.

I'm not claiming one vendor is cheaper or more honest. A standard price can be raised with notice, and an introductory price can be extended — pricing trackers report that Anthropic [cancelled a scheduled increase on Sonnet 5 back in August](https://tokencost.app/blog/llm-api-price-increases-2026), which I also couldn't verify directly.

The point is narrower and more useful: "does this price have a date attached to it" has become a real question with different answers per model, and most PMs I know aren't asking it.

## Four decisions this actually touches

**Your margin model.** Run it at post-promotional rates for any period after the expiry date. If the feature only works at $2, it doesn't work. Better to know that in October than in December, when the fix is a repricing conversation under time pressure.

**Launch sequencing.** If your AI feature ships in late November, its first full month of real usage is priced at the higher rate. Your early cohort's cost-per-user, the number everyone will quote for a year, gets measured in the expensive window.

**Your own pricing and limits.** If you sell seats with usage caps, those caps were sized against a cost that changes. Credit-based and consumption pricing pass the increase through; flat seats eat it. That's a decision, and it's yours, not finance's.

**Model-choice criteria.** Add price stability to the evaluation. Not as a tiebreaker on cost, but as a question: is this rate dated, what does it revert to, and what's my switching cost if it reverts badly? A model that's 20% more expensive today but not on a clock may be the cheaper choice over a planning year.

## Practical takeaway

Four things you can do this week:

1. **List every model your product calls, and mark which prices carry an expiry date.** Pull it from the vendor's pricing page, not a comparison blog. Most teams have three to five models in production and have never written them down in one place.
2. **Re-run your cost-per-task at post-promotional rates.** For Argon that's doubling input and output and doubling cached input. If the feature's unit economics break, you have six weeks to change the architecture, the price, or the limits.
3. **Check whether you're actually earning the cache discount.** With implicit caching, that means measuring your cached-token share, not assuming it. If your prefix is under 6,144 tokens or unstable, you're paying full rate and don't know it.
4. **Put the expiry date in whatever your team actually reads** — the roadmap, the on-call doc, the renewal calendar. November 30 is not a date anyone will remember unprompted, and it falls right where Q4 launches land.

## The honest limits of this

Six weeks is enough time to react, and a price doubling from a low base is still a low base — $4 and $20 is not exotic. I'm not arguing anyone should avoid Argon.

I'm arguing that a dated price is a different object than a price, and that a PM who treats the two the same will eventually explain a margin miss that was published in advance, in the launch post, on day one.

---

# Hero image

**Honest status first:** I could not verify any image page directly. This environment's network policy blocks DNS resolution for every image host I tried — unsplash.com, images.unsplash.com, pexels.com, openverse.org and commons.wikimedia.org all failed to resolve. The two candidates below came from search results that quoted the photo pages, so the photographer names and license types are second-hand and **must be confirmed on the page before publishing**. I have not fabricated a direct image URL for either, because the direct `images.unsplash.com` URL cannot be derived from the page slug without loading the page.

**Candidate 1 (primary)**
- **Source page:** https://unsplash.com/photos/black-and-white-calendar-on-white-wall-bY9bfWjLtiU
- **Direct image URL:** not obtained — download from the source page (Unsplash's own download button yields the direct URL)
- **Creator:** Waldemar Brandt
- **License (unconfirmed):** Unsplash License — free for commercial use, no attribution required
- **Attribution line (optional under this license, recommended anyway):** `Photo by Waldemar Brandt on Unsplash`
- **Why it fits:** A black-and-white wall calendar is editorial rather than literal, and the article is about a date attached to a price. No robots.

**Candidate 2 (backup)**
- **Source page:** https://unsplash.com/photos/clear-hour-glass-AMzC2RVurO4
- **Direct image URL:** not obtained — download from the source page
- **Creator:** Alexandar Todov
- **License (unconfirmed):** Unsplash License — free for commercial use, no attribution required
- **Attribution line:** `Photo by Alexandar Todov on Unsplash`
- **Why it fits:** Minimal hourglass, reads as a deadline without illustrating AI.

**Rejected:** Two strong-looking hourglass and "December 2026 calendar" images on Unsplash came back under the **Unsplash+ License**, which is paid. Don't use those: the hourglass on a pink background by Andrej Lišakov, and the December 2026 wall calendar by TSD Studio.

**Fallback description, if neither license checks out:** A tight, desaturated shot of a paper wall calendar or desk planner, photographed at a slight angle so the grid of dates recedes out of focus, with one date near the centre still sharp and unmarked. Cool neutral tones, lots of negative space on the left for Medium's title overlay, no screens, no hands, no stock-photo "AI" motifs. The visual idea is a deadline you can see but haven't circled yet. A plain abstract alternative: two flat price-tag shapes in slightly different shades, one noticeably larger than the other, on a muted background.

---

# Metadata

**Tags:** Product Management, AI, Pricing Strategy, SaaS, Unit Economics

---

## Unverified claims

- **Gemini Flash introductory rates through December 31, 2026, doubling January 1, 2027.** Taken from a third-party pricing tracker ([tokencost.app](https://tokencost.app/blog/llm-api-price-increases-2026)); the domain would not resolve in this environment, so I could not read the page or check it against Google's own pricing. Flagged as unverified in the article text too.
- **Anthropic cancelled a scheduled Sonnet 5 increase to $3/$15 in August 2026.** Same third-party source, same problem. Flagged in the article text.
- **Anthropic halved Sonnet 5.5 cache reads to $0.10 on October 7, 2026.** The *current* $0.10 rate is confirmed on [claude.com/pricing](https://claude.com/pricing), which I fetched. The *change* and its date come from [SiliconANGLE](https://siliconangle.com/2026/10/07/anthropic-releases-claude-haiku-5-5-small-model-and-halves-sonnet-5-5-cache-read-prices/), which I could not fetch.
- **Argon's implicit-caching-only behaviour, the 6,144-token minimum prefix, and durable caching by default.** These came from search results quoting Google's own developer documentation at docs.cloud.google.com, but that subdomain would not resolve, so I read the quotes rather than the page.
- **Non-global endpoint rates ($2.20 → $4.40 input).** From search results quoting Google's pricing page. The pricing page itself returned truncated content when fetched, and the search result noted other Argon-labelled rows at different prices ($3.60, $1.00) that it could not account for — so treat the global-endpoint figures as solid and the non-global ones as probable.
- **Both hero image licenses.** Every image host was DNS-blocked, so neither Unsplash License is confirmed. See the Hero image section.

**Confirmed by direct page fetch:** the Gemini 4 Argon launch post and its October 13, 2026 date, the $2/$10 introductory rate, the November 30, 2026 expiry, the $4/$20 standard rate, the 95%-off cached input, Argon's availability surfaces, and all quoted Claude Sonnet 5.5 and Haiku 5.5 prices.
