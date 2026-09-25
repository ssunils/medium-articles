# Design

**Subtitle:** New survey data says shoppers trust AI pricing answers more than they trust retailers. That changes who your pricing page is written for.

**Target reader:** A product manager at a consumer or DTC commerce company (roughly 50–500 people) who owns pricing, the pricing page, or the product catalog — and who has been asked at least once this quarter whether the company needs an "AI strategy" for discovery.

**Key takeaway:** Your price is increasingly read by a machine your customer trusts more than they trust you, so the practical question has shifted from "is our price competitive?" to "can our price be found, parsed, and repeated correctly?"

**Format:** data-brief

## Headline options

1. **56% Trust AI On Pricing. Only 32% Trust Retailers.** — *RECOMMENDED*. Two real numbers from the same survey, side by side, and the article's entire argument falls out of the gap between them. It promises a specific finding and then spends the piece on what to do about it.
   *(Hook type: specific surprising number)*

2. **Hiding Your Prices Stopped Protecting Your Margin**
   *(Hook type: contrarian claim — challenges the common belief that opacity is a pricing defense)*

3. **Who Is Actually Reading Your Pricing Page Now?**
   *(Hook type: sharp question the reader cannot answer confidently)*

## Section outline

- Open on the two numbers, from a survey released Wednesday
- Why a vendor-commissioned survey still deserves attention (and how to discount it)
- The decision it forces: publish vs. gate
- What comparability actually costs you
- What being unreadable costs you — the measured data, not the survey data
- Where the line actually sits (machine-readable ≠ publish everything)
- Practical takeaway
- What is still genuinely unclear

---

# Draft

*Word count: 1,198 (target 1,000–1,400).*

# 56% Trust AI On Pricing. Only 32% Trust Retailers.

Two numbers landed on Wednesday, and they belong next to each other.

Fifty-six percent of US shoppers say they trust AI tools to give them accurate pricing information when comparing products across retailers. Thirty-two percent say they completely or mostly trust retailers to offer a fair or competitive price.

Both come from the same [Akeneo PX Pulse survey](https://www.morningstar.com/news/pr-newswire/20260923ne54106/akeneo-survey-finds-shoppers-no-longer-take-prices-at-face-value), released September 23. A 24-point trust gap, in favour of the machine.

If you own a pricing page, that gap is your problem now.

## Read the survey skeptically. Then read it again.

The survey was commissioned by Akeneo, a company that sells product data infrastructure. A finding that says "your product data needs to be better for AI" is exactly the finding that vendor is in business to produce. Discount it accordingly.

But discount it, don't dismiss it. The methodology is disclosed — [conducted by Dynata in August 2026 among 1,000 US consumers aged 18 and over](https://retailtimes.co.uk/akeneo-survey-finds-shoppers-no-longer-take-prices-at-face-value/) — and the surrounding numbers are mundane enough to be believable. Seventy-seven percent say they have noticed the same product at different prices across retailers in the past year. Fifty-nine percent say price matters more to them than it did six months ago.

The one I would treat most cautiously is the headline adoption figure: [24% say they already use tools like ChatGPT or Gemini to compare prices or deals](https://agilebrandguide.com/akeneo-addressing-consumer-price-skepticism-strategic-imperatives-for-enterprise-cx-and-marketing/). Self-reported tool use in surveys tends to run high. Treat it as a direction, not a forecast.

The trust asymmetry is what survives the skepticism. People are outsourcing the "is this fair?" judgment, and they are not outsourcing it to you.

## The decision this actually forces

Most of the commentary around agentic commerce is about whether to let shopping agents transact on your site. That is a real question, but for most product teams it is not this quarter's question.

This quarter's question is narrower and more boring: **do you make your prices and product attributes easy for a machine to read, or do you keep them behind interaction?**

Gating is a genuine strategy. "Request a quote," price-on-login, member pricing, regional pricing that only resolves at checkout — these exist for reasons, usually margin protection and channel conflict. The argument for them has always been that friction slows comparison.

That argument is weakening, and it is worth being precise about why.

## Comparison pressure already exists

AI did not create price comparison. The survey says [77% of shoppers already notice the same product priced differently across retailers](https://www.morningstar.com/news/pr-newswire/20260923ne54106/akeneo-survey-finds-shoppers-no-longer-take-prices-at-face-value), and 79% have delayed a purchase waiting for a price to fall. Those behaviours predate assistants.

What changes is the cost of doing the comparison. It drops from "open eight tabs" to "ask once." When a behaviour that 77% of people already engage in gets ten times cheaper, you should expect more of it, not a new kind of it.

So the margin protection that opacity buys you was already eroding. AI assistants are accelerant, not ignition.

## What being unreadable costs

Here is the part I find more persuasive than the survey, because it is measured rather than self-reported.

Adobe Analytics, drawing on [more than a trillion visits to US retail sites](https://www.digitalcommerce360.com/2026/08/19/adobe-ai-referral-traffic-data-july-2026/), reported that AI-referral traffic to US retail sites in July 2026 was up 62% year over year. That traffic converts at a rate 60% higher than non-AI traffic and generates 53% more revenue per visit.

The volume is still small in absolute terms. But the quality is not small, and Adobe's own read is that [retail sites are lagging on machine readability](https://business.adobe.com/blog/ai-traffic-surge-retail-sites-not-machine-readable) — the pages are built for human scanning, not for parsing.

That is the asymmetric risk. If an assistant cannot parse your price, it does one of two things: it omits you from the comparison, or it infers something. And per the survey, [56% of people will believe what it says](https://www.morningstar.com/news/pr-newswire/20260923ne54106/akeneo-survey-finds-shoppers-no-longer-take-prices-at-face-value).

> The question is no longer whether your price is competitive. It is whether a machine can find it, read it, and repeat it correctly.

An assistant confidently quoting a stale or wrong price for your product is worse than an assistant quoting a high one. You can defend a high price. You cannot defend a price you did not set.

## Machine-readable does not mean publish everything

This is where I think the vendor framing overreaches, so let me draw the line where I would actually draw it.

Three things are worth making unambiguous and machine-parseable: **list price, availability, and spec accuracy.** These are the facts an assistant needs to include you in a comparison at all, and they are facts you are not really protecting by hiding.

Three things do not belong in that bucket: **negotiated and contract pricing, volume discounts, and anything that varies by customer.** Exposing those is a different decision with different consequences, and nothing in this week's data argues for it.

The platforms are drifting the same way. Amazon's [new plugin puts Seller Central data — listings, inventory, sales analytics — directly inside outside assistants like Claude](https://www.geekwire.com/2026/amazon-opens-its-seller-tools-to-outside-ai-agents-starting-with-anthropics-claude/), announced the same day as the Akeneo survey. Structured data is moving to where the assistants are. The interaction layer you built is not the layer it travels through.

## Practical takeaway

Concrete things to do in the next two weeks, cheapest first:

1. **Run the query yourself.** Ask ChatGPT, Gemini, and Claude to compare your three best-selling products against your two closest competitors. Screenshot the answers. This takes twenty minutes and is usually the moment the argument stops being theoretical.

2. **Log the errors, not the vibes.** Wrong price, wrong availability, wrong spec, omitted entirely. Count them. That list is your actual backlog; everything else is speculation.

3. **Fix structured data on your top 20 SKUs first.** Product markup with price, currency, and availability. Not a replatform — a scoped data hygiene task that a single engineer can usually do in a sprint.

4. **Decide the gating question explicitly, and write it down.** For each category: published list price, or gated? If gated, name what you are protecting and how you would know if it stopped working. An undocumented default is not a strategy.

5. **Instrument AI referral traffic separately** if you have not already. You cannot argue for investment in a channel you are not measuring, and by the time it is obvious in aggregate traffic the decision has been made for you.

None of this is a bet on agentic commerce arriving on any particular timeline. It is the same thing you would do if a large, unusually well-converting referral source started sending traffic and occasionally got your facts wrong.

## What is still unclear

Whether the trust gap holds. Trust in a new tool tends to be high before the first bad experience is widely shared, and a wave of confidently wrong AI pricing answers could reverse the 56% quickly.

Whether transparency compresses margin as much as the fear suggests. I have not seen good published evidence either way, and anyone telling you confidently is guessing.

And whether B2B follows. The survey is entirely consumer. The read-across to B2B SaaS pricing pages is plausible — buyers use the same assistants — but it is an extrapolation, and I would not present it to a leadership team as a finding.

---

# Hero image

**I could not verify a specific image, and I am flagging that plainly rather than giving you a link I have not confirmed.**

Outbound web fetching from this environment was blocked for every external domain during this run, including `unsplash.com`, `www.pexels.com`, and `openverse.org`. I could reach search listings but could not open any individual photo page, so I cannot confirm that a particular image exists, who shot it, or what licence it carries. Inventing a plausible-looking direct image URL would be worse than saying this.

**Where to look (verified as real search pages, licence terms not independently confirmed this run):**

- Unsplash — [Pricing](https://unsplash.com/s/photos/pricing) and [Price Tag](https://unsplash.com/s/photos/price-tag) collections. The [Unsplash Licence](https://unsplash.com/license) allows free commercial use with no attribution required, though crediting the photographer is encouraged.
- Pexels — [Pricing](https://www.pexels.com/search/pricing/) and [Online Shopping](https://www.pexels.com/search/online%20shopping/) collections, under the Pexels Licence (free for commercial use, no attribution required).

Both sites display the photographer name and licence on each photo page — check them at the point of download rather than trusting this file.

**Attribution line, if you choose an Unsplash image:** *Photo by [Photographer Name] on Unsplash* — optional under the Unsplash Licence, but good practice.

**Fallback description of the ideal cover image:** A tight, slightly abstract overhead shot of a single physical price tag or paper price label resting on a plain surface, shot shallow so the number itself is soft or partially out of focus. Cool neutral tones, lots of negative space on one side for the Medium title overlay. The feeling to aim for is "a number whose authority is uncertain" — the price is present but not quite legible, which is the article's whole argument. Avoid robots, humanoid AI, glowing brains, and blue circuit-board overlays. A clean alternative: an empty retail shelf edge with the price rail in focus and the products blurred behind it.

---

# Metadata

**Medium tags:** Product Management, Artificial Intelligence, Pricing Strategy, Ecommerce, Product Strategy

---

## Unverified claims

Outbound web fetching was blocked for all external domains during this run (the environment's network policy denied every host I tried, including news sites, `unsplash.com`, `openverse.org`, and `prnewswire.com`). Web search worked. That means **I could not open a single source page to confirm its publication date or wording directly** — every figure below comes from search results that quote or summarise the source, cross-checked across multiple independent outlets where possible. Treat this section as unusually important today.

- **All Akeneo PX Pulse figures (56%, 32%, 77%, 79%, 59%, 24%) and the methodology (Dynata, August 2026, 1,000 US consumers 18+).** Consistently reported across at least four independent outlets, and the Morningstar URL carries a `20260923` date stamp, which is how I placed it inside the 48-hour window. I could not open the Akeneo press release itself. One specific caution: the 24% AI-price-comparison figure and the 56% AI-trust figure appeared in coverage of both the August survey and an earlier May 2026 Akeneo survey in my searches. I have attributed them to the August wave, consistent with the majority of coverage, but I could not confirm this against the release.
- **Adobe Analytics figures (62% year-over-year AI-referral traffic growth in July 2026; 60% higher conversion; 53% more revenue per visit; trillion-plus visits sample).** Reported by Digital Commerce 360 at a URL dated 2026/08/19. Source page not opened. Note this is August data being used to support a September argument — it is recent, but it is not 48-hour-fresh, and it is cited here as context rather than as the news.
- **Adobe's assessment that retail sites lag on machine readability.** Based on the title and summary of an Adobe business blog post; I could not read the post, so I have characterised it broadly rather than quoting a specific statistic.
- **Amazon Seller Assistant plugin details (Seller Central data inside Claude and Amazon Quick, announced September 23, 2026).** Corroborated across GeekWire, Unite.AI, and several other outlets. Amazon's own newsroom page was blocked. Used as a one-sentence directional aside, not load-bearing.
- **Unsplash and Pexels licence terms.** Stated from search summaries of the licence pages, which I could not open. Verify on the licence page before publishing.
- **No image has been verified.** No direct image URL, photographer, or licence is asserted in the Hero image section for this reason.
- **Interpretive claims that are mine, not sourced:** that self-reported AI tool use in surveys runs high; that opacity's margin protection was already eroding before AI; that a confidently wrong price is worse than a high one; and that the consumer findings may not transfer to B2B. These are judgments, flagged as such in the text.
