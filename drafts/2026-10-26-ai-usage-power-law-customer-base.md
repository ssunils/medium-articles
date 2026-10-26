# Design

**Subtitle:** An economist's note on AI returns contains a distribution number that should change how you plan your 2027 roadmap.

**Target reader:** A B2B SaaS PM at a 50–500 person company who has already shipped an AI feature to the entire customer base and is heading into 2027 planning with a renewal conversation coming.

**Key takeaway:** AI consumption inside your customer base is almost certainly a power law rather than an average, so the top decile and the long tail need to be planned, priced and measured as two different products.

**Section outline:**
1. Hook: the 0.5% number, not the margin number
2. What the Apollo note actually says, and what it doesn't
3. Why the concentration figure travels down to your product
4. Your adoption metric measures breadth; only depth varies
5. The buyer's frame changed: token spend as a cost line
6. The decision: two products, not one
7. What the data genuinely does not establish
8. Practical takeaway

**Headline options:**

1. **Nine of Ten Customers Barely Touch Your AI Feature** — *RECOMMENDED*. Hook type: specific surprising number. It is concrete, it names the reader's own product rather than the macro debate, and the article pays it off directly with the 99.5%/0.5% split and the Ramp concentration data.
2. **Your AI Adoption Rate Is Hiding a Power Law** — Hook type: contrarian claim challenging a common PM belief (that percentage-of-accounts-activated is a real adoption signal).
3. **Before You Defend AI ROI, Can You Even See It?** — Hook type: sharp question the reader cannot answer confidently, given how few organisations measure AI returns against a benchmark.

---

# Draft

## Nine of Ten Customers Barely Touch Your AI Feature

Last Saturday an economist at Apollo published a note arguing that AI has delivered "zero" financial payoff to corporate America outside the technology sector. The line that got quoted everywhere was about profit margins.

The number that should actually worry you is in the table underneath. The bottom 90% of firms account for [0.5% of all spending on model serving and inference](https://cryptobriefing.com/apollo-ai-spending-concentration-risk/). The top 10% account for 99.5%.

Not five percent. Half of one percent.

If you have shipped an AI feature to your whole customer base, that distribution is probably sitting inside your own product right now. And most roadmaps, pricing models and adoption dashboards quietly assume it isn't.

## What the note says, and what it doesn't

Torsten Slok's argument is economy-wide. Revenue per worker is rising for the Magnificent 7 and flat for the other 493 companies in the S&P 500, whose [margins have stayed near 10%](https://ppc.land/apollo-finds-zero-ai-payoff-outside-tech-as-s-p-493-margins-stay-near-10/). He also sees [no clear acceleration in total factor productivity](https://www.implicator.ai/ai-payoff-skips-corporate-america-apollo-slok/) despite the investment, and argues the gap may be structural rather than a lag — that firms will struggle to convert cheap intelligence into revenue growth.

That macro claim is contested and you don't need to settle it. The concentration data is a different kind of fact, and a more useful one.

It comes from [Ramp's AI Index](https://cryptobriefing.com/apollo-ai-spending-concentration-risk/), card and bill payment data across tens of thousands of US companies. Direct payments to OpenAI and Anthropic are 95.6% concentrated in the top decile. Ramp's own cut of the same data finds [1% of firms driving roughly 80% of spend](https://beincrypto.com/ai-spending-concentration-ramp-data/) on those two vendors. Anthropic's top 1% of tracked customers reportedly drove [46% of its August spending](https://www.tokenpost.com/news/business/38148).

Three independent cuts, same shape. This is the most consistent finding in the whole AI-returns argument, and almost nobody is building product plans around it.

## The distribution travels downward

Here is why it lands on your desk.

Those payment records are companies buying AI. Your customers are companies buying software that contains AI. Same buyers, one layer up. If nine in ten of them spend almost nothing on tokens directly, there is no reason to expect them to suddenly become heavy consumers of the AI you embedded in your product.

So when you model "average queries per seat per month" and multiply, you are averaging across a curve where the mean sits nowhere near the median. Your capacity forecast, your margin forecast and your roadmap bets are all built on a number that describes almost none of your accounts.

> A power-law distribution with an average-shaped plan is how you end up over-serving the ninety and under-serving the ten.

## Your adoption metric measures the wrong axis

"AI features active in 42% of accounts" can be true while the median active account runs three prompts a month and then forgets the feature exists.

Breadth metrics — accounts touched, seats activated, percentage enabled — are the ones that look good in a board deck and the ones that move first. Depth metrics are where the variance actually lives, and depth is what determines whether the feature survives a renewal.

This is harder to fix than it sounds, because most organisations are not measuring returns at all. One widely-cited survey puts the share of organisations that [measure AI returns against a benchmark at 6.5%](https://www.beri.net/article/cfos-coming-ai-budgets-what-survives-2026). If your customers can't see their own payoff, they cannot defend your line item for you.

## The buyer's frame changed under you

The sharpest thing in Slok's note isn't a chart. It's his read on behaviour: mainstream corporate America is starting to view token spending ["not as a source of growth but as a cost center that weighs on margins"](https://fourweekmba.com/ai-tokens-are-a-cost-center-outside-tech-apollos-slok-says/).

That is a positioning problem, not an economics problem. A growth line gets a sponsor and a budget increase. A cost line gets a review and a target.

The budget signals point the same way. Deloitte finds [CFOs bracing for higher AI costs through fiscal 2027](https://www.cfodive.com/news/cfos-brace-higher-ai-costs-fiscal-2027-deloitte/830379/). Forrester is cited as predicting enterprises will defer about [25% of planned AI spend into 2027, with McKinsey finding only 37% of organisations attributing any EBIT impact to AI](https://www.innoverdigital.com/ai-roi-for-2027-budgets-what-cfos-need-cios-to-prove-before-funding-enterprise-ai/) — both figures secondhand, so treat them as directional.

Your AI feature is about to be defended by a champion to a finance team that reads it as variable cost with unproven return.

## The decision: two products, not one

The tempting response is to prove ROI harder — build a value calculator, commission a study. That's slow and it fights the measurement gap rather than routing around it.

The more honest move is to stop treating the AI surface as one product.

For the top decile, the ones already consuming: depth is the roadmap. They have the volume to justify usage-based pricing, they will absorb latency and cost tradeoffs for capability, and they are where your evals and your hardest edge cases should come from.

For the long tail: the goal is not to raise their consumption. It is to make the AI invisible and bundled, priced inside the thing they already bought, so nobody in their finance function ever sees a variable line item to question. That means capping it, defaulting it on, and not metering it.

This cuts against where the industry is heading — credits, allowances, metered pools. Metering is right for the decile that consumes. Applied to the ninety percent that doesn't, it manufactures a budget conversation you will lose.

## What this data does not establish

Honesty about the limits, because they matter for how hard you lean on this.

The 99.5% figure is a share *within Ramp's tracked customer base*, not of the whole economy. The denominator is a payments sample, and it skews toward the kinds of companies that use Ramp.

Adoption itself is rising, not falling. A Census working paper found [18% of firms using AI in a business function between November 2025 and January 2026](https://www2.census.gov/library/working-papers/2026/adrm/ces/CES-WP-26-25.pdf), up from low single digits in 2023. The 2025 "AI adoption is declining" headlines applied [only to large firms over a few months](https://www.tomshardware.com/tech-industry/artificial-intelligence/ai-adoption-rate-is-declining-among-large-companies-us-census-bureau-claims-fewer-businesses-are-using-ai-tools), and part of the later jump came from [a broadened survey question](https://econlab.substack.com/p/the-census-bureau-was-undercounting) rather than real change.

And flat margins are not proof of no payoff. Competitive industries pass savings to customers; the gain shows up as lower prices, not wider margins. Absence of a margin signal is weak evidence either way.

What survives all that is the shape of the curve. Concentration is the robust finding.

## Practical takeaway

Four things worth doing before your 2027 plan is locked:

1. **Plot the curve this week.** Per-account AI calls over the last 90 days, sorted descending. Not the average — the actual distribution. Find where your own 90/10 break sits. This is a one-afternoon query and it will reframe the rest of your planning.
2. **Split your adoption metric in two.** Report breadth and depth separately, and stop letting breadth stand in for health. Add a median-active-account number next to the percentage.
3. **Check the top decile's concentration risk.** If a handful of accounts drive most of your inference cost, they also drive most of your AI-attributable revenue. Know who they are by name before renewal season.
4. **Ask your champions one question:** "If your CFO asked you to justify this line next quarter, what number would you use?" If they can't answer, that is your real roadmap input — and it is a positioning fix, not a model upgrade.

The macro argument about whether AI pays off will run for years. The distribution question you can answer about your own product by Friday.

---

# Hero image

**Status: no verified image. I could not complete this step.**

I was unable to search or verify any image. This session's network policy denied outbound connections to every image source I tried — `unsplash.com`, `images.unsplash.com`, `api.unsplash.com`, `www.pexels.com`, `images.pexels.com`, `openverse.org`, `api.openverse.engineering`, `www.flickr.com`, `live.staticflickr.com`, and `commons.wikimedia.org` — each returning a 403 policy denial at the egress gateway.

Rather than present a URL I could not confirm exists or guess at a license, I am reporting the step as blocked. No primary image, no backup image.

**To unblock this for future runs:** add the image hosts above under Allowed domains in the environment's network settings (cloud environment menu in the session title bar → Edit), keeping "Allow package managers" ticked. Instructions: https://code.claude.com/docs/en/cloud-environments#network-access

**Fallback cover image description (for manual sourcing):**

A wide, editorial photograph of a long-exposure or abstract scene expressing extreme imbalance — for example, a single brightly lit office window in a dark high-rise facade, a steep histogram-like skyline at dusk, or a row of identical empty desks with exactly one occupied and lit. Muted palette: slate blues, charcoal, one warm accent light. Shot wide with generous negative space on the left for title overlay, 2:1 crop or wider to suit Medium's header. Avoid robots, androids, humanoid hands touching screens, glowing blue brains, and literal dollar signs. An abstract alternative that works well: a sparse scatter of points where almost all cluster at one edge of the frame, shot as bokeh or light trails, reading as a distribution rather than a diagram.

---

# Metadata

**Tags:** Product Management, Artificial Intelligence, AI Strategy, SaaS, Product Strategy

**Format:** segmentation-brief

**Word count (Draft section, excluding the headline):** 1,240 words.

---

## Unverified claims

This session's network policy blocked outbound HTTPS to nearly every host except github.com, raw.githubusercontent.com, anthropic.com and claude.com (403 policy denials at the egress gateway). **I could not open a single source page directly.** Every claim below therefore rests on web-search result summaries across multiple outlets rather than on my own read of the primary page. Where outlets agreed I have treated the claim as well-supported, but none of it is primary-source verified by me.

- **Publication date of the Apollo note (October 24, 2026).** Reported consistently across Bloomberg, Yahoo Finance, PYMNTS, implicator.ai and ppc.land, with Bloomberg's story dated October 25. One secondary item attributed the same 99.5% figure to a September 24 note, which conflicts. I could not open Apollo's Daily Spark page (`apollo.com` and `apolloacademy.com` both denied), so the date is cross-outlet corroborated but not primary-verified.
- **The 99.5% / 0.5% inference-spend split and the 95.6% OpenAI-plus-Anthropic concentration.** Taken from secondary coverage of Slok's table. I did not see Apollo's chart or Ramp's methodology page, so the exact sample definition is unconfirmed. The caveat in the article — that it is a share within Ramp's tracked base — is my inference from how the data is described, not a stated limitation I read in the source.
- **Direct quotes attributed to Slok** ("zero" payoff, "not as a source of growth but as a cost center that weighs on margins", "revenue per worker is rising for the Mag 7 but is flat for the S&P 493"). Consistent across outlets, but quoted from search summaries, not from the note.
- **S&P 493 margins "near 10%".** From a ppc.land headline. One other source described a different series (operating margins rising from ~16% to ~18% of sales, 2019–2025), which may or may not be the same measure. I could not reconcile them; the two figures are probably different margin definitions.
- **The 6.5% of organisations measuring AI returns against a benchmark.** Attributed to a "Basis survey" in secondary coverage. I could not find or open the primary survey, and the sample size and methodology are unknown. This is the weakest number in the article.
- **Forrester's 25% deferred-spend prediction and McKinsey's 37% EBIT figure.** Both appear only as secondhand citations on consultancy and vendor blogs. Flagged as directional in the article text. Not primary-verified.
- **Ramp's 1%-of-firms/80%-of-spend figure and Anthropic's top-1%/46%-of-August-spending figure.** Both from secondary coverage (beincrypto, tokenpost). The Anthropic figure describes spending within a tracked sample, not company revenue, and I could not verify its origin.
- **Census figures (18% of firms, Nov 2025–Jan 2026; the 2025 large-firm decline; the broadened survey question).** The working paper URL is a census.gov PDF surfaced in search, but I could not fetch it to confirm the 18% figure or the survey-break detail appears there as described.
- **Hero image: no image sourced or license confirmed.** Reported as blocked above. No image URL, photographer or license is asserted anywhere in this draft.
