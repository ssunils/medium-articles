# Design

**Format:** case-study (rotated away from yesterday's decision-guide)

**Subtitle:** Amazon blocked Meta's Muse on Sunday. Shopify wired it into every store by Wednesday. The split tells you how to pick your own agent policy.

**Target reader:** A product manager at a 50–500 person B2B SaaS company or marketplace who owns a logged-in surface, and who has just been asked — by a customer, a partner, or their own CTO — whether third-party AI agents should be allowed to drive the product on a user's behalf. Secondary: PMs at consumer products with an account system and an ads or engagement-based revenue line.

**Key takeaway (one sentence):** Whether you block or welcome third-party agents is decided by where your revenue actually comes from — the attention on your pages, or the transaction at the end of them — and you already have a de facto policy that nobody on your team chose.

## Headline options

1. **"$68 Billion Says Block the Agent. A Take Rate Says Otherwise."**
   *Hook type: specific surprising number.* (11 words)

2. **"Your AI Agent Policy Is a Pricing Decision, Not Security"** — **RECOMMENDED**
   *Hook type: contrarian claim challenging a common PM belief.* (10 words)
   Reason: it names the reframe the article actually delivers, and it challenges the assumption most PMs walk in with — that agent access is a trust-and-safety ticket rather than a business-model question.

3. **"Amazon Blocked It. Shopify Billed It. Same Agent, Same Week."**
   *Hook type: concrete before/after stakes framing.* (10 words)

## Section outline

1. Cold open — the 72-hour split, stated as two dated events
2. What actually happened (timeline, both sides' claims)
3. Follow the money, not the security memo ($68.6B ad revenue vs. a GMV take rate)
4. The tell: the double standard as a strategy statement
5. The version of this that lands on your desk (non-retail, B2B)
6. Three doors, priced differently (block / ignore / sanction)
7. Practical takeaway — concrete next actions
8. What I'd watch next (Ninth Circuit, CFAA)

---

# Draft

*Word count: 1174 (target 1000–1400).*

## Your AI Agent Policy Is a Pricing Decision, Not Security

On Sunday night, Amazon started blocking Meta's two-week-old AI agent from its store. On Wednesday, Shopify's CEO announced he was wiring the same agent into every store on his platform.

Same agent. Same week. Opposite answers.

If your product has a login screen, that split is your next roadmap argument. It will arrive earlier than you'd like, and it will arrive disguised as a security ticket.

## What actually happened

Meta launched Muse — a personal agent that browses, books and buys on your behalf — [on September 8](https://finance.yahoo.com/technology/ai/articles/meta-platforms-unveils-muse-ai-030205273.html).

About two weeks later, Amazon began blocking it, [starting Sunday night](https://www.bloomberg.com/news/articles/2026-09-21/amazon-blocks-meta-s-muse-ai-agent-from-its-retail-site). Amazon's stated reasons: Meta never asked permission, the agent doesn't identify itself while browsing, and it "appears to capture and store" customer credentials. Shoppers who point Muse at Amazon now [get pop-ups telling them they're violating the conditions of use](https://www.geekwire.com/2026/amazon-blocks-metas-muse-ai-assistant-in-new-standoff-over-agentic-shopping/).

Meta disputes the credentials claim, saying Muse ["has no visibility into people's passwords or payment methods"](https://www.geekwire.com/2026/amazon-blocks-metas-muse-ai-assistant-in-new-standoff-over-agentic-shopping/) because they sit in separate storage the model can't read. As far as I can tell, [no third party has published an analysis of Muse's actual credential handling](https://thenewstack.io/amazon-meta-muse-block/), so both positions are currently assertions.

Then on Wednesday, Shopify CEO Tobi Lütke announced a partnership ["to enable agentic checkout with Shop Pay on all Shopify stores"](https://www.pymnts.com/commerce/ecommerce/2026/shopify-brings-shop-pay-checkout-solution-to-metas-muse-ai-agent/). PayPal, Expedia and Instacart [landed the same day](https://techcrunch.com/2026/09/23/everything-new-coming-to-metas-ai-agent-muse/).

One platform spent the week building a wall. The other spent it building a door, with a toll booth in the frame.

## Follow the money, not the security memo

Amazon made [more than $68.6 billion in advertising revenue in 2025, up 22% year over year](https://www.forbes.com/sites/the-prompt/2026/09/23/amazons-68-billion-reason-to-block-metas-muse/). That number depends on humans landing on Amazon pages and looking at sponsored placements.

An agent that searches, compares and checks out without a person ever seeing a page doesn't just skip the ads. It makes the surface Amazon rents to advertisers unviewed.

Shopify's economics run the other direction. Shopify gets paid [when a checkout completes, whoever or whatever drove it there](https://www.fool.com/investing/2026/09/23/amazon-blocked-meta-s-ai-shopping-agent-shopify-welcomed-it-and-gets-paid-on-every-checkout/). An agent that closes more carts is distribution, not leakage.

> Amazon and Shopify didn't disagree about agents. They disagreed about where their money comes from.

Amazon's security objections may well be valid. They're just not what's doing the deciding.

## The tell: the double standard

Amazon's updated conditions of use, effective August 14, [require agents to identify themselves in their user-agent string and to stop when asked](https://www.geekwire.com/2026/amazon-blocks-metas-muse-ai-assistant-in-new-standoff-over-agentic-shopping/). That's a reasonable rule, and one worth copying.

Amazon also [builds agents that shop across other people's sites](https://stellagent.ai/insights/amazon-ai-agent-rufus-buy-for-me). Reporting this week argues Amazon is [holding Muse to identification standards its own shopping agents don't clearly meet](https://www.techtimes.com/articles/327940/20260923/amazon-blocks-meta-muse-using-standards-it-ignores-its-own-shopping-agent.htm) — a pattern one analyst summarised as ["your agent can't shop at Amazon; Amazon's agents shop everywhere"](https://liatbenzur.com/2026/09/21/your-agent-cant-shop-at-amazon/).

Read that as a strategy statement rather than hypocrisy. Amazon is clearly betting agentic shopping grows, or it wouldn't be building for it. It just wants to be the agent, not the store the agent shops at.

That's the same bet you're making when you write your own policy, whether you realise it or not.

## The version of this that lands on your desk

You don't run a marketplace. Fine. Here's the B2B shape of the same problem: a customer connects a general-purpose agent to your product using their own credentials, and it starts clicking through your UI at 40 actions a minute — pulling reports, changing settings, filing tickets.

Nothing was breached. A paying user delegated their access. Your seat-based pricing quietly stops describing reality, your support volume changes shape, and your audit log now says a human did things a human didn't do.

The tooling to take a position already exists. Cloudflare's signed-agent work turns allow-versus-block into a configuration choice: [19 verified agents covering an estimated 84% of identified AI browser traffic](https://blog.cloudflare.com/signed-agents/), with a default of letting verified agents through and blocking unverified ones. On the identity side, the emerging guidance for B2B products is that [agents should delegate rather than impersonate](https://www.scalekit.com/blog/b2b-m2m-authready) — scoped, revocable, attributable access instead of a borrowed human session.

Most teams aren't there. Cisco's 2026 security report puts [the share of organisations that say they're prepared to secure agentic deployments at 29%](https://securityboulevard.com/2026/09/ai-agent-identity-and-access-control-a-framework-for-b2b-saas/).

The uncomfortable part: you already have an agent policy. It's whatever your login flow, rate limiter and edge config happen to do today. Nobody chose it.

## Three doors, priced differently

**Block.** Defensible when agent traffic erodes the surface you monetise, or when you genuinely can't attribute actions. Costs you the users who wanted it, and invites the argument Amazon is currently having in court.

**Ignore.** The default. Agents keep using your product badly, through a human interface built for humans, and you learn about it from a support ticket or a bill.

**Sanction.** Build an interface agents are supposed to use, require them to identify themselves, scope what they can do, and price it. This is where the decision stops being abstract: OpenAI [charges merchants 4% per Instant Checkout purchase](https://openai.com/index/buy-it-in-chatgpt/) on the rails it co-developed with Stripe as [an open agentic commerce standard](https://stripe.com/newsroom/news/stripe-openai-instant-checkout). Sanctioned access isn't free access. It's a price.

Shopify picked door three. Amazon picked door one. Both were reasoning correctly from their own P&L.

## Practical takeaway

Four things you can do in the next two weeks, none of which require a strategy offsite:

1. **Measure it.** Ask whoever owns your edge or WAF for a breakdown of traffic by user-agent and behavioural signature over the last 30 days. You want one number: what share of logged-in sessions look non-human. Decide after you see it, not before.
2. **Write down which side of the split you're on.** One sentence: "We get paid when someone *sees* X" or "We get paid when someone *does* X." If it's *sees*, agents are a threat to model. If it's *does*, they're a channel to enable. Most products have some of both — say which dominates.
3. **Fix the terms before the traffic.** Copy the specific, testable parts of Amazon's clause: agents must identify themselves in the user-agent string and must stop on request. Vague "no automated access" language is unenforceable and blocks the partners you want.
4. **Ask your top five accounts.** "Is anyone on your team pointing an AI agent at us?" You'll get a clearer read in five calls than in a quarter of speculation — and if the answer is yes, you've found your design partner for door three.

## What I'd watch

Amazon sued Perplexity in late 2025 over its Comet browser and [won an injunction in March](https://www.cnbc.com/2026/03/10/amazon-wins-court-order-to-block-perplexitys-ai-shopping-agent.html), with the judge finding Comet accessed accounts with the user's permission but without Amazon's authorisation. Perplexity appealed; at [oral argument in June the Ninth Circuit wrestled with a 1986 hacking statute that has no concept of an agent](https://www.courthousenews.com/perplexity-ai-asks-ninth-circuit-to-allow-shopping-tool-on-amazon/) and hasn't ruled.

If that court decides a user's permission is enough, every "our terms forbid it" policy — including the one you're about to write — gets re-litigated.

Which is the real argument for deciding on purpose now. A policy you chose can be defended and revised. A policy your rate limiter chose for you can only be discovered, usually by a customer.

---

# Hero image

**I could not verify any image.** This session's network policy blocked direct access to unsplash.com, images.unsplash.com, pexels.com and openverse.org, so I was unable to confirm that a specific photo exists, is still published, or carries the licence I'd be claiming. Per the brief, I'm saying so plainly rather than pasting a URL I can't stand behind.

What I *can* confirm from search results is the licence landscape, which is the part that usually trips people up:

- The [Unsplash License](https://unsplash.com/license) permits free commercial and non-commercial use with no attribution required (attribution appreciated but optional). Searches that fit this article: [gate](https://unsplash.com/s/photos/gate), [turnstile](https://unsplash.com/s/photos/turnstile), [corridor](https://unsplash.com/s/photos/corridor), [open doorway](https://unsplash.com/s/photos/open-doorway).

**To finish this in about two minutes:** open the [turnstile](https://unsplash.com/s/photos/turnstile) or [corridor](https://unsplash.com/s/photos/corridor) search, pick a frame matching the description below, and record four things — the direct image URL, the photo's page URL, the photographer's name, and the licence shown on that page. If you land on a Pexels or Openverse image instead, check whether its licence is CC0 (no attribution) or CC BY (attribution required); for CC BY the line to paste under the image is: `Photo by [Creator Name](photo page URL), licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)`.

**Ideal cover image (fallback description):** A wide, minimal, high-contrast shot of two adjacent passages that resolve differently — for example a row of metal turnstiles where one barrier is closed and the next stands open, or a corridor of identical glass doors with a single one ajar. Muted industrial palette (concrete grey, brushed steel, one warm accent), shallow depth of field, no people, no text, no robots or humanoid figures. Shot slightly off-centre so the article title can sit in negative space on the left third. The image should read as *access control*, not *artificial intelligence* — the article is about who gets let in and on what terms, and literal robot imagery would undercut that.

---

# Metadata

**Tags:** Product Management, AI Agents, Agentic Commerce, Product Strategy, SaaS

---

## Unverified claims

**A note on method that affects everything below.** This environment's network policy blocked direct access to every news domain I tried (bloomberg.com, geekwire.com, forbes.com, techcrunch.com, thenewstack.io, fool.com, cnbc.com, courthousenews.com, techtimes.com, blog.cloudflare.com, pymnts.com, and others). I could run searches but could not open the source pages. So the dates and figures below come from search-engine summaries of those pages, cross-corroborated across multiple independent outlets, **not from reading the primary sources**. The links are correct as far as search results indicate, but I did not confirm any page's publication date on the page itself, which the brief asked for.

Specifically unverified:

- **Publication dates.** All dating — Muse's September 8 launch, Amazon's block beginning Sunday night (September 20), the Shopify announcement on Wednesday September 23 — is corroborated across several outlets but not confirmed on any source page. The Amazon block and the Shopify deal are consistently dated within the last 72 hours across Bloomberg, GeekWire, Forbes, PYMNTS, TechCrunch and Motley Fool summaries.
- **Amazon's ad revenue figure.** Search results attribute "$68.6 billion in 2025, up 22% from $56.2 billion" to the Forbes piece, but one other source (a Substack newsletter) cited $76 billion. I used the Forbes figure because it was the better-sourced of the two; treat the exact number as needing a check against Amazon's 10-K before publication.
- **Shopify's merchant default.** Search summaries indicate Shopify merchant catalogues were shared with Muse by default, with an explicit opt-out under Sales channels. This is a consequential detail for merchants and I could not confirm it on Shopify's own documentation. I deliberately kept it out of the draft body for that reason.
- **The Cloudflare figures** (19 verified agents, ~84% of identified AI browser traffic) come from a search summary of Cloudflare's signed-agents blog post, not from the post itself.
- **The Cisco 29% figure** is quoted in a Security Boulevard article per search results; I did not reach Cisco's 2026 State of AI Security report directly.
- **Amazon's own agents and the identification asymmetry.** The claim that Amazon's own shopping agents don't meet the identification standard it applied to Muse is an argument made by TechTimes and one independent analyst, not an established fact. I attributed it as reporting and analysis in the draft rather than stating it flatly.
- **The credentials dispute is genuinely open.** Amazon says Muse "appears to capture and store" credentials; Meta denies it; no independent traffic analysis has been published that I could find. The draft says exactly this.
- **Hero image.** No image licence confirmed — see the Hero image section. The Unsplash License terms are as described in search results but I could not load unsplash.com/license to verify the current wording.
- **The 4% OpenAI Instant Checkout fee** is widely reported in search results but I could not confirm it on OpenAI's page.
