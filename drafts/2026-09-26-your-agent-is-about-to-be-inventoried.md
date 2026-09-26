# Design

**Subtitle:** A governance layer is being bought above your product. Here is what it will ask your agent to prove.

**Target reader:** A B2B SaaS product manager at a 50–500 person company who has shipped, or is about to ship, an AI agent feature into enterprise accounts — and who has never been asked to produce an owner, a cost, or a business outcome for that agent.

**Key takeaway:** Enterprise buyers are installing a layer that inventories every agent they run and scores it on cost versus value, so instrument ownership, spend, and outcome per agent now, and tier your controls by what the agent can actually do rather than applying one policy to all of them.

**Format:** playbook

**Section outline:**
1. Open on the launch — a product whose job is to find agents nobody remembers approving
2. The adoption/visibility gap that makes this a PM problem, not an IT one
3. Why this lands on your roadmap: your agent becomes a line item in someone else's portfolio review
4. The trap: governing every agent identically
5. The four fields a portfolio review will demand from your agent
6. Tiering by capability, not by category
7. Practical takeaway — what to do in the next sprint
8. What I would not do yet

## Headline options

1. **96% Run AI Agents. 12% Can List Them.**
   *Hook type: specific surprising number.* The gap between the two figures is the whole article.
   **RECOMMENDED** — both numbers come from the same survey, the contrast is instantly legible, and the piece pays it off by explaining exactly what closing that gap does to your product.

2. **Governing Every AI Agent The Same Way Will Kill Yours**
   *Hook type: contrarian claim.* Most PMs assume more uniform governance is safer; Gartner's position is that uniformity is the failure mode.

3. **Can You Name Who Owns Your AI Agent?**
   *Hook type: sharp question the reader cannot answer confidently.* Almost no PM can answer this for a shipped agent, and the article is the answer.

---

# Draft

*Word count: 1125*

A vendor shipped a product this week whose entire job is to find AI agents nobody remembers approving.

[Dataiku announced Agent Management on September 24](https://siliconangle.com/2026/09/24/dataiku-debuts-cross-platform-agent-management-expands-cobuild-building-agent/), a standalone product that connects to Salesforce Agentforce, the agent services run by AWS and Microsoft, and agents built on Databricks and Snowflake, then pulls them into a single inventory. It records who owns each agent, maps the models and tools it depends on, and measures both business and technical performance. Custom environments connect through OpenTelemetry. General availability is October.

Whether Dataiku wins this category is not the interesting part. The interesting part is that the category now exists, and that it sits *above* every vendor's stack — including yours.

## The gap that makes this your problem

[OutSystems surveyed 1,900 IT leaders](https://www.outsystems.com/news/enterprise-ai-agent-report-2026) for its 2026 State of AI Development report, fielded in December 2025 and January 2026. Ninety-six percent of those organisations were already using AI agents. Twelve percent had a centralised way to manage them. Ninety-four percent said sprawl was increasing complexity, technical debt, and security risk.

So the buying pressure is obvious. Almost everyone has agents, almost nobody has a list, and almost everyone is nervous about it. That is a category waiting to be sold into.

Here is the part that changes your job: when your customer finally builds that list, your agent goes on it.

## Your feature becomes a line item in someone else's review

Right now, an agent you ship inside your product is usually invisible to your customer's platform team. It shows up as your product. It gets renewed or churned as your product.

An inventory layer breaks that. It resolves your agent into its own row, with an owner, a model dependency, a set of tools it can call, a monthly cost, and a performance score. [SiliconANGLE's write-up](https://siliconangle.com/2026/09/24/dataiku-debuts-cross-platform-agent-management-expands-cobuild-building-agent/) makes the intent plain: sitting above every vendor's stack lets the tool answer portfolio-wide questions, like where risk is concentrated and which agents cost more than they return.

Read that last clause again as a PM. "Which agents cost more than they return" is a decommissioning query, and your feature is in the result set.

> The moment your agent has its own row in someone else's spreadsheet, it stops being a feature and starts being a budget line.

That is not hypothetical. [Gartner predicted in May](https://www.gartner.com/en/newsroom/press-releases/2026-05-26-gartner-says-applying-uniform-governance-across-ai-agents-will-lead-to-enterprise-ai-agent-failure) that by 2027, 40% of enterprises will demote or decommission autonomous AI agents because of governance gaps found only after a production incident. Demotion is the quieter outcome and probably the more common one: the agent keeps running, but with its permissions cut to the point where it no longer does anything useful. Your usage metrics go flat and you never learn why.

## The trap: one policy for every agent

The instinct, once a governance layer lands, is to apply the strictest available controls everywhere. Gartner's argument in that same May release is that this is the failure mode, not the fix — applying uniform governance regardless of an agent's autonomy level and scope is itself what causes enterprise agent programmes to fail. The distinction that matters is between what an agent can *do* and how much access it has been *granted*, and treating governance as binary — locked down or fully trusted — collapses that distinction.

Gartner sorts agents into four autonomy tiers: observe, advise, act-with-approval, and fully autonomous. That framing is more useful to a PM than it first looks, because most shipped "agents" are sitting in the first two tiers while being described in sales decks as if they were in the fourth.

If you have been marketing an advise-tier feature with act-tier language, a governance review is where that catches up with you.

## The four things a review will ask of your agent

From what these tools discover, four fields decide whether an agent survives a portfolio review. None of them are model quality.

**Owner.** A named human, on the customer's side, accountable for the agent. If your product ships an agent with no configurable owner field, the inventory records "unknown," and unknown is where cuts start.

**Blast radius.** Which tools and data the agent can reach, as opposed to which it typically uses. Reviews score the grant, not the habit.

**Cost per unit of work.** Not monthly spend. Spend divided by the thing the customer cares about — tickets resolved, documents processed, calls summarised.

**Outcome.** Evidence the work was correct and useful. [Gartner's April guidance on agent sprawl](https://www.gartner.com/en/newsroom/press-releases/2026-04-28-gartner-identifies-six-steps-to-manage-artificial-intelligence-agent-sprawl) puts a centralised inventory and ongoing behavioural monitoring at the centre of its six steps, alongside identity, permissions, and a retirement process for redundant agents.

The uncomfortable bit: most AI features I have seen instrument the first mile — prompts sent, sessions started — and almost none instrument the last one.

## Practical takeaway

Four things worth doing in the next sprint or two. None are large.

1. **Write down your agent's autonomy tier** using Gartner's four levels, and check it against your own marketing copy. If they disagree, one of them is wrong, and it is cheaper to fix the copy.

2. **Add an owner field.** Let the admin who enables your agent assign a named accountable person, and expose it in your API. When the inventory tool reads your product, you want it to find a name.

3. **Ship a per-agent cost and outcome metric to your admin surface.** Spend, volume, and one success measure your customer already reports on. If you do not define that metric, the governance layer will define one for you, and it will be a generic one.

4. **Separate the grant from the use.** Audit what your agent is *permitted* to touch versus what it actually touches, and narrow the grant. This is the single cheapest thing you can do before a security review, and it is also the field a portfolio review weights most heavily.

## What I would not do yet

I would not buy a governance platform on the strength of a launch. Dataiku's product is not generally available until October, its pricing is per instance annually with monitoring metered per agent, and nobody has run it at scale in anger yet. Cross-platform governance is a bet that a neutral layer beats each cloud's native tooling, and that bet is genuinely unresolved.

I would also be careful with the sprawl statistics. They come from vendors and analysts who sell into the problem they are describing, and survey-based adoption numbers tend to run ahead of what is actually in production.

But the direction is not really in doubt. The buyer-side question is shifting from "does your AI feature work" to "can I see it, price it, and switch it off." Those are three different engineering asks, and only one of them is on most AI roadmaps right now.

---

# Hero image

**I could not verify a hero image for this draft.** This session's network policy blocked outbound requests to unsplash.com, pexels.com, openverse.org, and every other image host I tried (HTTP 403 at the egress proxy), so I could not open a single image page to confirm it exists, check the licence, or obtain a direct image URL. I am not presenting an unverified link as verified.

**Unverified candidates** (surfaced by search index only — each needs you to open the page and confirm the licence before use):

1. "Abstract network of threads and nodes on pins" — credited in search results to Aakash Dhage — source page `https://unsplash.com/photos/abstract-network-of-threads-and-nodes-on-pins-6v_hA5gdPE8`. Physical threads-and-pins imagery reads as "mapping connections," which fits an inventory piece. Licence presumed Unsplash Licence; **unconfirmed**.

2. "Abstract illustration of interconnected lines and nodes" — credited in search results to Alex Shuper — source page `https://unsplash.com/photos/abstract-illustration-of-interconnected-lines-and-nodes-uJj_24rroJE`. Licence presumed Unsplash Licence; **unconfirmed**.

If either is genuinely under the Unsplash Licence, no attribution line is required, though crediting the photographer is good practice: *Photo by <photographer> on Unsplash*.

**Fallback cover description (use this if you cannot verify the above):** A wide, desaturated overhead shot of a pinboard or wall covered in small labelled cards connected by taut coloured string — the visual language of someone painstakingly mapping a system that grew faster than the map. Muted greys and off-whites with one accent colour in the string, plenty of empty space on the right third for the Medium title overlay, shallow depth of field so individual card text is illegible. No robots, no glowing brains, no humanoid androids. An equally good alternative: a close crop of a spreadsheet or asset-register printout on a desk, shot at a low angle, with a pen resting on one highlighted row.

---

# Metadata

**Medium tags:** Product Management, AI Agents, Enterprise Software, AI Governance, B2B SaaS

---

## Unverified claims

Outbound network access was blocked for every domain I tried (HTTP 403 from the egress proxy), so I could not open a single source page. Everything below rests on search-engine results rather than a primary source I read directly. Dates and figures were cross-checked across multiple independent search queries and against date-stamped URLs, but that is weaker verification than the brief asks for, and this section should be read as substantial rather than routine.

- **Dataiku announced Agent Management on 24 September 2026, GA in October.** Corroborated by three date-stamped URLs from independent outlets (SiliconANGLE `/2026/09/24/`, Help Net Security `/2026/09/25/`, FinancialContent `bizwire-2026-9-24`) and consistent across four separate searches. I could not open dataiku.com to read the press release itself.
- **Product details** (connectors for Agentforce, AWS, Microsoft, Databricks, Snowflake; OpenTelemetry for custom environments; records owner, maps models and tools, measures business and technical performance). Attributed to SiliconANGLE's coverage via search summary; page not read directly.
- **Pricing: per instance annually, monitoring metered per agent.** Appeared consistently in search summaries of the press release. Not confirmed against Dataiku's own page. Treat as the least reliable claim in the piece.
- **OutSystems 2026 figures** (1,900 IT leaders, fielded Dec 2025–Jan 2026; 96% using agents, 12% centralised management, 94% concerned about sprawl). Consistent across two independent searches and matching a BusinessWire release URL dated 2026-04-07. Primary page not read.
- **Gartner, 26 May 2026** (uniform governance causes failure; four autonomy tiers observe / advise / act-with-approval / fully autonomous; 40% of enterprises will demote or decommission autonomous agents by 2027). Date confirmed by the Gartner press-release URL slug `2026-05-26` and a secondary outlet dated the same day. Note this is **four months old, not fresh** — it is used as background, not as news.
- **Gartner, 28 April 2026** (six steps to manage agent sprawl). Date from the URL slug `2026-04-28`. Also background, not fresh.
- **Gartner's "150,000 agents per Fortune 500 enterprise by 2028, up from fewer than 15 in 2025."** Surfaced in a search summary; I chose **not** to use it in the draft because I could not confirm it against the release.
- **Hero images.** Both candidates are unverified: existence inferred from search results, licence unconfirmed. See the Hero image section.
- **My own framing** — the four review fields, the demotion-is-quieter-than-decommissioning argument, and the advise-tier-marketed-as-act-tier observation — is analysis, not reported fact, and is not sourced to anyone.
