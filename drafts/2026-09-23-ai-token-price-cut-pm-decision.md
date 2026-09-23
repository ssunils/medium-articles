# Design

**Subtitle:** OpenAI halved its API prices on Tuesday. That's a budget landing on your desk, not a result — and the default way teams spend it is the wrong one.

**Target reader:** A B2B SaaS PM at a 50–500 person company who already has an AI feature in production, owns or is accountable for its inference cost line, and has to defend gross margin to a finance partner.

**Key takeaway:** A 50% token price cut is not free margin — it is an unallocated budget, and unless you deliberately choose whether to bank it, spend it on quality, or widen access, rising tokens-per-task will absorb it before you notice.

**Section outline:**
1. Hook — the price moved on Tuesday and nobody on the team noticed
2. What actually shipped (specific prices, old vs new)
3. The trap — cheaper tokens historically produce bigger bills, not smaller
4. The second signal — this was an efficiency release, not a capability release
5. Four doors — bank it / spend on quality / widen access / cut price
6. The prerequisite — you need cost per task before any of this is actionable
7. Practical takeaway — six concrete actions

**Headline options:**

1. **A 50% Token Price Cut Is Not Free Margin** — *RECOMMENDED*. Contrarian hook that challenges the obvious reading of Tuesday's news, and the article pays it off directly with the Jevons/tokens-per-task argument. Specific, 9 words, promises nothing it doesn't deliver.
2. **Your AI Feature Got 50% Cheaper Tuesday. Now What?** — hook type: specific number plus stakes framing.
3. **Can You Say What Your AI Feature Costs Per User?** — hook type: sharp question most PMs cannot confidently answer.

---

# Draft

On Tuesday the model underneath your AI feature got about 50% cheaper. Most product teams will find out from a finance dashboard three weeks from now.

OpenAI [released GPT-6 Sol and GPT-6 Luna on September 22](https://venturebeat.com/technology/openai-releases-gpt-6-sol-and-luna-models-slashing-api-costs-50-or-more) and cut API prices at the same time. Sol is now [$2 per million input tokens and $10 per million output](https://pulse2.com/openai-launches-gpt-6-sol-and-luna/), down from $4 and $20. Luna went from $0.20/$1.20 to [$0.10/$0.50](https://thenewstack.io/openai-gpt-6-sol-luna-release/). These are [reported as permanent rates, not introductory promotional pricing](https://thenewstack.io/openai-gpt-6-sol-luna-release/).

If your AI feature has a real inference bill, a meaningful cost line just halved without anyone on your team writing code.

That sounds like good news, and mostly it is. But "we just doubled our gross margin on AI" is the conclusion I'd be most careful about. It's usually wrong, and it's wrong in a way that only shows up two quarters later.

## The money doesn't stay saved

Here's the pattern that keeps repeating. Token prices fall, and total AI spend goes up anyway.

Inference costs have dropped [more than 98% in roughly two years](https://liveinthefuture.org/stories/ai-coding-cost-jevons-paradox), while demand grew by orders of magnitude over the same period. Cheaper units didn't shrink anyone's bill. They removed the reason to say no to new usage.

Gartner's version is sharper. Token prices are expected to keep falling — [roughly 95% by 2030 — while the inference cost of a single agentic workflow rises more than fivefold through 2028](https://getnadir.com/blog/gartner-inference-paradox-agentic-cost-tiering-2028/).

The mechanism is mechanical, not mysterious. An agent that plans, calls tools, checks its own work and retries burns [5 to 30 times the tokens of a single chatbot exchange](https://getnadir.com/blog/gartner-inference-paradox-agentic-cost-tiering-2028/). Meanwhile [enterprise AI costs keep climbing even as per-token prices fall](https://www.themoderndatacompany.com/blog/why-cheaper-ai-tokens-are-increasing-enterprise-ai-costs).

So price per token is falling and tokens per task are climbing. Your bill is the product of those two numbers, not the first one.

> A price cut isn't a result. It's a budget you haven't allocated yet.

If you don't decide where the saving goes, your roadmap will decide for you — usually by quietly spending it on longer context, more retries, and a more agentic version of the same feature.

## Cost and capability just came apart

There's a second signal in Tuesday's launch that matters more than the price itself.

At least one analysis argues the new models [cut prices in half but barely moved the needle on performance](https://the-decoder.com/openais-gpt-6-sol-and-luna-cut-prices-in-half-but-barely-move-the-needle-on-performance/). Read that alongside the launch framing: OpenAI pointed to [improvements in inference efficiency and prompt caching](https://pulse2.com/openai-launches-gpt-6-sol-and-luna/) as what let it charge less.

That's a different kind of release than we got used to. It's an efficiency release, not a capability release.

For a PM, that distinction is the entire planning question. If cost is falling faster than capability, then the features you shelved for being too expensive are worth reopening this week. The features you shelved because the model wasn't good enough are still shelved.

Those are two different backlogs. They don't move at the same rate, and treating them as one list is how teams end up re-attempting something that still doesn't work, just more cheaply.

Commentary also frames the cut as competitive — [pressure from rivals and from cheap open-weight models](https://www.cryptopolitan.com/openai-cuts-gpt-6-sol-luna-prices-by-50/). If that read is right, more cuts are coming. Which has a direct implication: don't spend a sprint re-architecting around today's price.

## Four doors, and picking by default is the failure mode

A price drop hands you a budget. There are four honest things to do with it.

**Bank it.** Take the margin. Legitimate if your AI feature is currently underwater, or if you owe someone a gross-margin number this quarter. Just say out loud that you're doing it, so it's a decision and not an accident.

**Spend it on quality.** Same cost, better output. A stronger model on the hard 10% of requests, more retrieval, a verification pass, a self-check before you show the user anything. For a feature that already has users and a known failure mode, this is usually the highest-value door.

**Widen access.** Turn the feature on for the tier that couldn't justify it before. Raise the rate limit you set for cost reasons rather than product reasons. Most AI features have at least one limit that exists only because of a price that no longer applies.

**Cut your own price.** Rarely the right first move, and much the hardest to reverse.

That fourth door connects to a shift already underway: pricing moving from seats toward usage and outcomes. [Intercom charges per resolved conversation and HubSpot's agent moved to a per-resolution price](https://thepricingconundrum.substack.com/p/outcome-based-pricing-in-practice). If you're on outcome pricing, a token price cut flows more or less straight to margin. If you're still on seats, it doesn't — and this is a reasonable moment to revisit that.

## The uncomfortable prerequisite

None of this is actionable if you can't answer one question: what does your AI feature cost per active user, per month?

A lot of teams can't. Bain's argument is that [AI pricing has to be grounded in actual effort and usage rather than intuition](https://www.bain.com/insights/ai-pricing-a-reality-check-on-effort-usage-and-outcomes/). And Gartner has projected that [more than 40% of agentic AI projects will be scrapped by 2027](https://www.metisstrategy.com/product-management-ai-value-measurement/), driven substantially by unclear value and weak cost control.

A 50% price cut is a genuine gift to teams who already instrument cost per task. For everyone else it's noise. They won't see the decrease, and they won't see the increase either.

## Practical takeaway

Concrete things to do this week:

1. **Pull the last 30 days of token spend and divide by active users of the AI feature.** One number. If you can't produce it within an hour, that difficulty is itself the finding.
2. **Re-run your unit economics at the new prices before deciding anything.** Check whether the cut applies to the specific tiers you actually call, including cached input, rather than assuming it's uniform.
3. **Write down which of the four doors you're choosing, and why.** One paragraph in the feature's doc. This is the step that gets skipped, and skipping it is how the saving evaporates.
4. **Audit the limits you set for cost reasons.** Rate caps, truncated context, a cheap model on a path that deserved a better one. Some of those constraints are now obsolete.
5. **Instrument tokens per task, not just tokens per month.** That's the number that rises as your feature gets more agentic, and it's the one that will absorb this cut.
6. **Don't re-platform around today's price.** If the cuts are competitive, another is coming. Spend the effort on model portability instead of on squeezing a number that's moving on its own.

The teams that get real value out of Tuesday won't be the ones who move fastest. They'll be the ones who already knew what the feature cost on Monday.

**Word count (Draft section): 1,114** — within the 1,000–1,400 target. Counted on the Draft section only, with markdown link URLs stripped and link text retained.

---

# Hero image

**I could not verify a real image.** This session's network policy blocked direct access to unsplash.com, pexels.com and openverse.org, so I was unable to open any image page to confirm that it exists, capture the direct image URL, or read the license and photographer credit. Rather than present links I can't stand behind, I'm flagging this plainly.

**Unverified candidate surfaced by search (do not publish without checking):** a search result pointed to an Unsplash photo page titled "A person using a calculator on a desk" at `https://unsplash.com/photos/a-person-using-a-calculator-on-a-desk-i1Ov6Irqego`. I could not open this page. Photographer unknown, direct image URL unknown, existence unconfirmed. Treat it as a lead only.

**Fallback — ideal cover image description:**

A wide, quiet editorial shot of a single desk surface viewed from directly above, lit with soft natural light: a laptop showing an indistinct spreadsheet or line chart, a notebook with a pen resting on it, and a plain calculator slightly off-centre. Muted palette — warm greys, off-white paper, one small accent of colour. No faces, no robots, no glowing brains, no circuit-board motifs. The feeling should be ordinary operational work: someone quietly re-checking their numbers, not a technology spectacle. A near-equivalent alternative is a tight abstract macro of a descending bar or line chart printed on paper, shallow depth of field, with the declining trend legible but not literal.

**To source it manually:** search Unsplash for "calculator desk overhead" or "spreadsheet laptop desk", or Pexels for "budget planning desk". Both the [Unsplash License](https://unsplash.com/license) and the [Pexels License](https://www.pexels.com/license/) permit commercial use without attribution, though crediting the photographer is good practice. Confirm the license on the actual photo page before publishing — some Unsplash results are Unsplash+ (paid) rather than free.

---

# Metadata

**Medium tags:** Product Management, Artificial Intelligence, SaaS, Pricing Strategy, Unit Economics

---

## Unverified claims

Being direct about this: **this session's network policy blocked WebFetch and curl access to every news and image domain I tried** — venturebeat.com, thenewstack.io, pulse2.com, the-decoder.com, openai.com, news.ycombinator.com, blog.google, thenextweb.com, unsplash.com, pexels.com, openverse.org and others all returned egress-blocked errors. Only github.com was reachable. Every factual claim below therefore rests on web-search result summaries, corroborated across multiple independent outlets, but **not** confirmed by reading the source page directly. The linked URLs are the sources the search surfaced; each should be opened and checked before publishing.

- **GPT-6 Sol and Luna launched September 22, 2026, with prices cut ~50%** — consistently reported across at least six independent outlets (VentureBeat, The New Stack, Pulse2, TheNextWeb, Cryptopolitan, Benzinga) with matching figures: Sol $2/$10 per million tokens (from $4/$20), Luna $0.10/$0.50 (from $0.20/$1.20). Corroboration is strong, but I could not confirm against OpenAI's own pricing page, which was blocked. **Verify against openai.com/api/pricing before publishing** — this is the article's central factual claim.
- **That these are permanent rather than promotional prices** — reported in search summaries; not confirmed on a primary source. Note that one outlet (TradingKey) framed the comparison as against a GPT-5.6 *promotional* price, which would change the size of the cut. This discrepancy is unresolved.
- **"Barely moved the needle on performance"** — attributed in the draft to a single outlet (the-decoder) and deliberately framed as one analysis rather than established fact. No benchmark figures were obtained.
- **OpenAI attributing the cut to inference efficiency and prompt caching** — from search summary only; no direct quote verified.
- **Gartner: token prices down ~95% by 2030; agentic workflow inference cost up >5x through 2028; agentic tasks use 5–30x the tokens of a chatbot turn** — these come from secondary write-ups of Gartner research (getnadir.com, neuralwired.com), not from Gartner directly. The underlying report is paywalled and was not accessed.
- **Gartner: >40% of agentic AI projects scrapped by 2027** — widely cited figure, sourced here via a secondary write-up (Metis Strategy), not from Gartner directly.
- **Inference costs down 98%+ in two years / demand up ~10,000x** — from a single secondary analysis (liveinthefuture.org). The 98% figure is widely repeated elsewhere; the 10,000x demand figure is not independently corroborated and is the weakest number in the piece. Consider cutting it or softening further.
- **Intercom per-resolved-conversation and HubSpot per-resolution pricing** — from a Substack summary (The Pricing Conundrum); specific figures ($0.99 and $0.50) appeared in search results but are **not** stated in the draft precisely because I could not verify them. The directional claim is safe; the numbers are not.
- **Competitive framing of the price cut (rivals, open-weight pressure)** — commentary/interpretation from secondary sources, presented in the draft as framing rather than fact.
- **Hero image** — no image verified. License, photographer and existence all unconfirmed for the one candidate URL surfaced by search. See the Hero image section.
