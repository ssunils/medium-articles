# Design

**Subtitle:** Cloudflare's KV cache leak is a reminder that the limits printed on your vendor's spec sheet are not the limits running in production.

**Target reader:** A B2B SaaS product manager at a 50–300 person company who has shipped an LLM feature on a hosted inference API (Workers AI, Bedrock, Vertex, OpenRouter, or similar) and owns the customer-facing answer when something goes wrong with it.

**Word count (draft body):** 1,174 words — within the 1,000–1,400 target. Counted with markdown link syntax reduced to display text.

**Key takeaway:** When you build on shared inference, both your tenant isolation and your breach-notification clock are your vendor's property — so cap your inputs, log your token counts, and negotiate disclosure timing before you need it.

## Headline options

1. **Your Context Window Said 1,048,576. The Cache Held 681,280.**
   Hook type: specific surprising number. Pays off in the first section, which is built on exactly that mismatch.

2. **Tenant Isolation Isn't Your Feature. It's Your Vendor's Config File.**
   Hook type: contrarian claim. Challenges the common PM belief that isolation is something your architecture provides.

3. **Could You Prove Your AI Feature Wasn't In Those 155 Responses?** — **RECOMMENDED**
   Hook type: sharp question the reader cannot answer confidently. Recommended because most PMs genuinely cannot answer it, and the article delivers the two concrete things (input caps, token logging) that would let them.

## Section outline

- Open on the disclosed number and the date gap
- The advertised limit vs. the serving limit
- Why the failure landed in the tail of traffic, not the average
- The disclosure clock, and who owns it
- Why shared caching isn't going away (the cost math)
- Practical takeaway: five concrete actions

# Draft

On October 26, Cloudflare published a number worth sitting with: 155 responses from its hosted GLM-5.3 model had returned data belonging to other customers' requests.

Not a theoretical side channel. Actual prompt and generation data from one tenant, surfacing in another tenant's output, in production, for thirteen days.

The exposure window ran from August 27 to September 9, 2026, [according to Cloudflare's postmortem](https://blog.cloudflare.com/kv-cache-exposure-remediation). The disclosure came seven weeks after it closed.

If you shipped a feature on that model this summer, you learned about it the same day the rest of us did.

## The advertised limit was not the enforced limit

The root cause is the part that should change how you read a model card.

GLM-5.3 on Workers AI advertised a context window of 1,048,576 tokens. The prefill GPU key-value cache actually provisioned to serve it held 681,280 tokens — [a configuration gap between what the API promised and what the hardware behind it could hold](https://aiweekly.co/alerts/cloudflare-says-kv-cache-bug-leaked-155-glm-53-responses).

On its own, that mismatch is a capacity bug. Paired with a bug in SGLang's request-rejection path, it became an isolation failure: an oversized request took an error path, and decode then read stale cache pages left behind by earlier requests. The SGLang maintainers [describe the fix as covering that rejection path and tightening cache-lifetime handling in disaggregated serving](https://www.lmsys.org/blog/2026-10-26-cf-security).

Read that sequence again as a product person. The number in the docs was a marketing surface. The number that governed safety was in a deployment config nobody outside the operator could see.

Every context window you have ever quoted in a roadmap doc has this property. You just haven't had a reason to check.

## The failure lived in your tail, not your average

Here is the detail that makes this actionable rather than merely alarming: every affected response came from a prompt longer than 681,280 tokens.

That is not normal traffic. That is the far tail — the enterprise customer who pasted their entire knowledge base, the agent loop that accumulated context for six hours, the one integration that forgot to truncate.

[Cloudflare's investigation found the affected requests looked like ordinary long-context traffic](https://gigazine.net/gsc_news/en/20261028-kv-cache-exposure-remediation/) rather than deliberate probing. Nobody was attacking. Somebody was just sending very long prompts.

So the question is not whether your vendor had a bug. It is whether you can tell, today, if your product ever sent a prompt that long.

Most teams cannot. We instrument token counts for billing, in aggregate, monthly. We rarely keep a per-request distribution we could go back and query seven weeks later.

And in a B2B product, oversized prompts are not an edge case you designed — they are a feature working as intended for your largest account. Document-grounded search that retrieves forty attachments instead of five. A support agent that replays an eighteen-month ticket history. A "summarize this workspace" button that one customer points at a workspace twelve times bigger than your test fixtures.

Those requests come from the accounts you can least afford to send an awkward email to.

> The incident you can't investigate retroactively is the incident you have to assume you were in.

## The clock belongs to your vendor

The second thing this incident hands you is a timeline problem.

The researcher who found it, Gadi Evron of Knostic, [reported it through Cloudflare's HackerOne program on September 8, 2026](https://www.unite.ai/cloudflare-says-glm-5-3-bug-leaked-155-responses-across-tenant-sessions/). The model was restored the following day. Public disclosure landed on October 26.

Whatever you owe your own customers — contractual notification, a security page update, a conversation with the one regulated account that asked hard questions during procurement — your clock started on October 26, because that is when you found out.

Most SaaS breach clauses were not written with this shape in mind. Practitioner guidance has started to catch up: one ISO 42001 implementation guide [suggests targeting 24 to 72 hours depending on severity for AI incidents](https://www.isms.online/iso-42001/ai-vendor-risk/), and a healthcare sector guide [proposes 24–48 hours for security incidents from AI vendors](https://healthsectorcouncil.org/wp-content/uploads/2026/04/AI-Third-Party-Risk-Guide.pdf). A CISO-led vendor risk piece argues the definition of "incident" itself needs widening to cover things like [modifications to AI training or inference processes](https://www.whistic.com/resources/blog/the-2026-vendor-risk-agenda-ciso-led-insights).

These are proposals, not standards. No rule compelled a seven-week timeline to be shorter. Which is precisely why it is a negotiation item and not a compliance checkbox.

It also changes what you can honestly say. "We were not affected" requires evidence you may not have kept. "We have no indication we were affected" is weaker, true, and the only sentence most teams are actually entitled to right now.

## Nobody is going to stop using shared inference

It would be easy to end at "demand dedicated capacity." That advice doesn't survive contact with a budget.

Cache sharing is the cheapest performance lever in the stack. A 2026 evaluation across OpenAI, Anthropic, and Google found prompt caching [reduces API costs by 45–80% and improves time to first token by 13–31%](https://arxiv.org/html/2601.06007v2). Giving that up to buy isolation you probably already had is a bad trade for most products.

And the tension is structural rather than incidental. Research on KV-cache side channels notes that [strict per-user cache isolation prevents cross-tenant leakage but gives up the reuse and latency benefits that make sharing worthwhile](https://arxiv.org/pdf/2508.08438). You are picking a point on that curve whether or not you know it.

The real decision is narrower and more answerable: which slice of your product can tolerate shared inference, and what do you cap so the tail never becomes the experiment?

## Practical takeaway

Five things, roughly in order of effort:

**1. Cap your max input tokens below the advertised window.** Pick a number you can defend operationally, not the one on the model card. Reject or truncate above it, with a clear error. This single control would have kept you out of all 155 responses.

**2. Log per-request token counts with retention past 60 days.** Not aggregates — distributions. The question "did we ever send a prompt over N tokens between these two dates" should take a query, not an investigation.

**3. Ask your inference vendor one specific question.** Not "are you secure." Ask: is the serving configuration's cache pool sized to the advertised context length, and what happens to a request that exceeds it? Cloudflare's own remediation advice [tells operators to verify exactly that](https://blog.cloudflare.com/kv-cache-exposure-remediation), which tells you it's a fair question to put to anyone else.

**4. Put a notification window in the contract at next renewal.** Use the 24–72 hour range as your anchor and define "incident" to include isolation and model-behavior events, not just credential breaches.

**5. Decide, explicitly and in writing, which tier doesn't run on shared inference.** For most products that set is empty, and that's a legitimate answer. It stops being legitimate when you've never asked.

None of this is exotic. Four of the five are a sprint of work, and the fifth is a one-page decision you can write this week.

What makes it worth doing now is that the next disclosure of this shape will also arrive weeks late, and the only difference between teams will be whether they can answer the first question their biggest customer asks.

# Hero image

**I could not verify a usable free image.** Outbound fetches to unsplash.com, pexels.com, arxiv.org, blog.cloudflare.com and other hosts failed DNS resolution in this session's network policy, so I could not open any photo page to confirm it exists or read its license. Rather than present a guessed direct image URL, here is what I actually established and what to do.

**Rejected candidate (do not use).** Search surfaced an Unsplash photo of arranged data servers by Planet Volumes at `https://unsplash.com/photos/data-servers-are-arranged-in-a-server-room-e-i-oN7ZDCk`. Metadata in the search result marks it as **Unsplash+ License** with `isAccessibleForFree: false` — it is a paid asset, not free for commercial use. Flagging it specifically because it ranks highly and looks like a safe pick.

**Verified starting points (collection pages, license terms confirmed via search, individual photos not verified):**

- Unsplash server room collection — `https://unsplash.com/s/photos/server-room`
- Unsplash infrastructure collection — `https://unsplash.com/s/photos/infrastructure`

Both pages state the standard Unsplash License terms: free for commercial use, no attribution required. Any photo picked from them still needs its own page checked, because Unsplash+ paid assets appear inline in the same grids (as the rejected candidate above shows).

**Attribution line to use anyway** (the Unsplash License doesn't require it, but it's good practice and Medium readers expect it):

> Photo by [Photographer Name] on [Unsplash](https://unsplash.com)

**Fallback cover image description:** An abstract, tightly cropped photograph of parallel fiber-optic or ribbon cables running in the same conduit — many separate channels bundled into one shared path, shot shallow-focus so individual strands blur into each other toward the edge of frame. Cool blues and greys, no text, no human figures, no robots or android imagery. The visual argument is shared infrastructure carrying separate traffic, with the boundaries between channels visibly imperfect. An editorial alternative: an overhead shot of a single physical mail sorting tray where one envelope sits in the wrong slot — mundane, specific, and closer to the actual failure than any data-center stock photo.

# Metadata

**Tags:** Product Management, Artificial Intelligence, Multi Tenancy, Vendor Management, AI Infrastructure

# Unverified claims

Outbound network restrictions in this session blocked direct fetches to every primary source host (blog.cloudflare.com, www.lmsys.org, arxiv.org, unsplash.com, www.unite.ai). All dates and figures below were corroborated across multiple independent secondary reports via search, and the primary source URLs are real and confirmed to exist, but **I could not open the primary pages to read publication dates or figures myself.** Treat the following as sourced-but-unopened:

- **The 155-response count, the August 27 – September 9, 2026 exposure window, and the 1,048,576 vs. 681,280 token mismatch.** Consistent across five or more independent reports (AI Weekly, GIGAZINE, unite.ai, datastudios.org, aicybr.com) and attributed to Cloudflare's own postmortem. Not read on blog.cloudflare.com directly.
- **Cloudflare's disclosure date of October 26, 2026.** Secondary coverage agrees on October 26; one search result reported the Cloudflare blog index showing October 23. The GIGAZINE write-up carries an October 28 date. The 48-hour freshness claim rests on the October 26 date plus the Hacker News thread appearing in the [October 28 digest](https://github.com/fireKylinKing/agents-radar/issues/50). If the real date is October 23, this topic is five days old, not two.
- **Gadi Evron / Knostic as the reporting researcher, and the September 8, 2026 HackerOne report date.** Appears in multiple secondary reports; not confirmed against Cloudflare's post or Knostic's own disclosure.
- **The SGLang fix version.** Sources conflict: one says the patch landed in v0.5.20, another recommends v0.5.22 or later. I deliberately left version numbers out of the draft for this reason.
- **The "45–80% cost reduction, 13–31% TTFT improvement" prompt caching figures.** From arXiv paper 2601.06007 ("Don't Break the Cache: An Evaluation of Prompt Caching") as reported in search results. Abstract not read directly; arxiv.org was unreachable.
- **The KV-cache isolation/performance tradeoff characterization.** From arXiv 2508.08438 as summarized in search results. Abstract not read directly.
- **Hacker News engagement numbers.** Deliberately excluded from the draft. Three separate digests reported the same thread at 178, 89, and 43 points, which means at least two are wrong or were captured at different times.
- **The 24–72 hour and 24–48 hour notification windows.** These are recommendations from practitioner guides (ISMS.online, Health Sector Coordinating Council), not regulatory requirements. The draft states this explicitly. Guide pages not opened directly.
- **Hero image.** No image license confirmed. See the Hero image section — I am presenting no verified image, and one highly-ranked candidate was rejected as a paid Unsplash+ asset based on search metadata alone.
