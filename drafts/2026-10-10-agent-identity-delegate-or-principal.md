# Design

**Subtitle:** Google just gave an AI agent its own email address. That makes an identity decision you have probably been deferring urgent.

**Target reader:** A B2B SaaS PM at a 50–500 person company whose product has an API, an OAuth app, or an MCP server — and who is starting to see traffic that is clearly not a human clicking.

**Key takeaway:** Decide now whether an agent in your product is a human's delegate or its own principal, because your audit log, rate limits, offboarding and billing all inherit that choice, and changing it later is a data migration rather than a setting.

**Format:** field-guide

## Section outline

1. Open on the concrete thing Google shipped on October 8
2. What was actually announced (identity, permissions, audit, spend caps, preview status)
3. The two models: delegate vs. principal — and why most products are accidentally delegate
4. What breaks under the delegate model (audit, rate limits, offboarding, billing, support)
5. The five questions that are genuinely yours to answer
6. What is still unsettled — the protocol layer has no spec yet
7. Practical takeaway

## Headline options

1. **Google's Agent Got Its Own Email, Calendar, and Spending Cap**
   *Hook: concrete, specific, slightly absurd detail — the spending cap is the surprising part.*

2. **Your Audit Log Is Already Lying About Who Did What** — RECOMMENDED
   *Hook: contrarian claim that challenges the assumption that logging is a solved problem. Recommended because it names the reader's actual exposure rather than Google's news, and the article pays it off directly: under the delegate model every agent action is recorded as a human's.*

3. **When An Agent Logs Into Your Product, Whose Seat Is It?**
   *Hook: a sharp question most PMs cannot answer confidently about their own product today.*

---

# Draft

On October 8, Google gave an AI agent its own email address.

Not a service account. Not an API key with a friendly label in a settings page. A Workspace account — with a calendar, Drive storage, and an entry in the company directory, [reportedly on a dedicated agents domain](https://www.developersdigest.tech/blog/gemini-agent-coworker-agents-own-email-2026).

If you build software, the interesting part is not Google's product. It is the question the announcement puts to yours: when an agent does something in your app, who does your system think did it?

Most of us have never actually answered that. We inherited an answer by accident.

## What Google actually shipped

At Gemini at Work 2026, Google [introduced a single "Gemini agent" for enterprise work](https://cloud.google.com/blog/products/ai-machine-learning/welcome-to-gemini-at-work-2026), including a persistent "coworker" mode where the agent [gets its own Workspace account, email address, calendar, and Drive storage](https://venturebeat.com/orchestration/google-cloud-unveils-persistent-gemini-agents-for-long-running-tasks-and-they-get-their-own-gmail-calendar-and-drive-storage).

Four details matter more than the email address.

It acts under its own identity, not the employee's — each coworker agent gets a [cryptographically attested identity that is stamped into its logs](https://redreamality.com/blog/gemini-enterprise-agent-identity-audit-spend-caps/) and into any virtual machine it starts.

Its permissions are approved by administrators and deliberately narrow: the agent is [limited to the information team members choose to make available](https://www.marktechpost.com/2026/10/08/google-cloud-launches-gemini-agent-one-universal-agent-for-enterprise-work/) rather than inheriting broad organizational access.

Every action is [logged to the agent rather than to a person](https://thenextweb.com/news/gemini-agent-workspace-identity-europe).

And it has a budget. Spend caps are set per project, and [when a cap is hit the agent pauses until an admin resumes it](https://redreamality.com/blog/gemini-enterprise-agent-identity-audit-spend-caps/).

It is early — the thing is in private preview, with [no published pricing and no general availability date](https://www.beri.net/article/google-gemini-agent-coworker-workspace-account-identity-audit-spend-caps-gemini-at-work-2026). Treat it as a direction of travel, not a shipped standard.

## Two ways to model an agent

Strip away the branding and there are only two options.

**The delegate.** The agent borrows a human's credentials. It acts inside that person's session, with that person's permissions, and your database records that person as the actor. This is what an OAuth token gives you by default.

**The principal.** The agent is its own entity in your data model. Its own identifier, its own permission grant, its own rate limit, its own line on the invoice, its own audit trail.

Almost every product I have looked at is in the first camp — not because a PM chose it, but because tokens belong to users and nobody ever questioned that. The delegate model is the default you get for free.

Free is not the same as correct.

## What breaks under the delegate model

**Audit.** This is the expensive one. If an agent acts on Priya's token, your log says Priya did it. Not "Priya's agent." Priya. When a customer asks who deleted the records, your answer is confidently wrong.

> An agent that borrows a human's identity makes every log entry a small lie.

Worth noting that the other direction has its own gap. One critique of Google's design points out that if the [audit trail names only the agent, the person who delegated the work has to be recorded somewhere else](https://www.beri.net/article/google-gemini-agent-coworker-workspace-account-identity-audit-spend-caps-gemini-at-work-2026). The fix is not one actor field or the other. It is two: who acted, and on whose behalf.

**Rate limits.** Yours are tuned to human pace — a person clicking a few times a minute. An agent either trips them constantly doing legitimate work, or sails through limits that were never meant to bound a machine.

**Offboarding.** Priya leaves. You revoke her account. Did you just silently break a workflow three teams depend on? Or worse: does the agent keep running on a token nobody owns and nobody is watching?

**Billing.** Per-seat pricing assumes one human, one seat. Deloitte's 2026 predictions flagged the visibility problem plainly — [AI agents do not show up in an admin's license dashboard](https://helply.com/blog/per-seat-saas-pricing-dying). You cannot price what you cannot count.

**Support.** Every one of the above lands in a ticket eventually, and your support team has no field to look at.

## The five questions that are yours

Not Google's, not a standards body's. Yours, this quarter.

**1. Does an agent get its own identifier?** Adding a nullable `agent_id` and `on_behalf_of` to your actor model costs little now. Backfilling months of logs to figure out which actions were really human costs a great deal.

**2. What are a new agent's default permissions?** Today the answer is implicit, which usually means "whatever the user has." The Personal Agent Protocol's proposed answer is a useful reference: an agent [starts as a guest and gets read-only or write access once the customer signs in](https://aicoder.com/news/news-20261007-sierra-meta-personal-agent-protocol-open-standard). Three tiers, not one.

**3. Who pays, and for what?** Some vendors have already moved off seats — Zendesk bills per automated resolution, and Intercom's Fin charges [roughly $0.99 per resolution](https://www.getmonetizely.com/blogs/the-2026-guide-to-saas-ai-and-agentic-pricing-models). You do not need to reprice this quarter. You do need to know whether your current model undercharges by 10x when one customer points an agent at it.

**4. Who owns an agent when its author leaves?** This is a policy question that will become a support escalation if you skip it.

**5. Can an admin pause one agent without pausing the person?** Google's answer is the spend cap — a budget that halts the agent and leaves the human alone. If your product has no equivalent, your only lever is revoking a human's access.

## What is still unsettled

Be honest about how early this is, because the protocol layer is genuinely unfinished.

The Personal Agent Protocol was [announced on October 6 by Meta and Sierra](https://fourweekmba.com/ai-meta-and-sierra-announce-personal-agent-protocol-spec-due/) with Shopify, Stripe, Walmart and others attached — but without a specification at launch. A v0.1 is planned for later in October, and payments are a future extension. OpenAI, Anthropic and Google are not on the partner list.

It also is not the only one. UCP, ACP and Visa's Trusted Agent Protocol all overlap, and analysts argue they are [complementary rather than winner-take-all](https://aaif.io/blog/there-is-no-one-agentic-commerce-protocol).

Which means: do not go implement a spec that does not exist yet. The identity modelling is the part that pays off regardless of which protocol wins, because every one of them needs your product to know what an agent is.

## Practical takeaway

Five things, in order, none of which require a roadmap slot:

1. **Open your audit log schema and count the actor fields.** If there is one, that is the finding. You need two — actor, and on-behalf-of.
2. **Add the nullable columns this sprint,** before you need the history. This is the cheapest item on the list today and the most expensive one to retrofit.
3. **Write down the default permission for an agent you have never seen before.** One sentence. Right now it is undocumented, which means it is whatever your OAuth scope happens to allow.
4. **Ask your billing owner one question:** what happens to the invoice if a single customer's agent multiplies their API calls by fifty? Get the actual answer, not the theory.
5. **Add one line to the offboarding runbook:** what happens to agents this user authorized.

Then stop. Do not pick a protocol, do not reprice, do not build an agent marketplace. The decision in front of you is narrow and unglamorous — whether your product can tell a machine from the person who sent it — and it is the one that everything else gets built on top of.

Google answered it with an email address and a spending cap. Your answer can be two database columns. But it should be an answer you chose.

---

# Hero image

**I could not verify a real image for this article, and I am not going to present an unverified link as if I had.**

This session's network policy denied every image source. Unsplash (`unsplash.com`, `images.unsplash.com`, `api.unsplash.com`), Pexels (`www.pexels.com`), Openverse (`openverse.org`, `api.openverse.org`) and Wikimedia Commons (`commons.wikimedia.org`) all failed to resolve through the egress proxy, which returned HTTP 403 on connect. Page fetching was unavailable for every host except GitHub, so I could not confirm that any candidate image exists, nor read its license page to confirm commercial use or attribution requirements.

Quoting an image URL from a search snippet without opening it would be guessing, which the brief rules out. So there is no primary pick and no backup pick below — only the fallback description.

**Fallback description of the ideal cover image:**

An editorial, abstract shot of an empty desk in a shared office — a clean monitor, a keyboard, an empty chair pushed slightly back — photographed in soft, neutral daylight with a shallow depth of field. The emptiness is the point: the seat exists, the workstation is provisioned, and nobody is sitting in it. A desk nameplate or badge lanyard just out of focus in the foreground would sharpen the idea further. Alternatively, a macro photograph of an office door nameplate holder with a blank insert, or a row of identical mail slots with one unlabelled, both carry the "an identity has been issued to something that isn't a person" idea without resorting to robot or android imagery. Muted greys, warm wood and a single accent colour; no glowing blue circuitry, no humanoid hands reaching toward each other.

**To source it when the network allows:** search Unsplash or Pexels for *empty desk office*, *vacant workstation*, *blank nameplate*, or *mail slots* and verify the licence on the photo's own page before use.

---

# Metadata

**Medium tags:** Product Management, AI Agents, SaaS, Identity And Access Management, Product Strategy

---

## Unverified claims

Two environment limits shaped this draft, and both affect how much weight the sourcing carries.

**WebFetch was unavailable for the entire session.** Every host except GitHub failed DNS resolution through the agent proxy, and direct connections returned HTTP 403 from the egress policy — including the primary sources I most wanted to open (`cloud.google.com`, `thenextweb.com`, `venturebeat.com`, `x.com`). The brief asks me to confirm each item's publication date on the source page. **I could not do that for any claim in this article.** Everything below is sourced from search-result summaries, which quoted the pages, rather than from the pages themselves.

Specific items I could not confirm against a primary source:

- **The October 8, 2026 date for Gemini at Work 2026.** Search results consistently place it on October 8, and one URL carries `/2026/10/08/` in its path, which is corroborating but not conclusive. I did not open Google's own announcement.
- **The agent's own email address, calendar, Drive storage and company-directory presence.** Consistent across several outlets; not read on Google's blog. The "dedicated agents domain" detail appeared in only one secondary source.
- **The cryptographically attested identity stamped into logs and VMs.** Appears in one secondary analysis. One search pass explicitly noted it found no independent confirmation of the audit and spend-cap specifics beyond vendor and analyst write-ups.
- **Spend caps set per project, pausing the agent until an admin resumes.** Secondary coverage only.
- **Audit actions attributed to the agent rather than the person**, and the critique that the delegating human must then be recorded elsewhere. The critique is one commentator's argument, not a documented limitation.
- **Private preview status, and the absence of published pricing or a GA date.** Secondary coverage. Availability details may have changed.
- **Model routing across Google's models and Anthropic's Claude** — reported in search results. I left this out of the draft body for that reason.
- **The Personal Agent Protocol's October 6 announcement, its partner list, its OAuth guest/read-only/write tiers, and the v0.1 spec planned for later in October.** Sources agreed, but one noted that some posts describe the standard as already published while others say no spec was attached at launch. The guest/read-only/write progression is reported, not read from a specification — because at the time of writing there may not be one to read.
- **Intercom Fin at roughly $0.99 per resolution and Zendesk's per-automated-resolution billing.** From a vendor-adjacent pricing blog. The word "roughly" in the draft is doing real work; treat the figure as indicative.
- **Deloitte's 2026 TMT Predictions claim that AI agents do not appear in an admin's license dashboard.** Attributed to Deloitte by a secondary blog. I did not see the Deloitte document.
- **Every hero image and its licence.** Nothing verified; see the Hero image section.

On freshness: the Google announcement (October 8) falls inside the 48-hour window. **The Personal Agent Protocol material is from October 6–7, which is outside it.** I used it as supporting context for a decision framework rather than as today's news, and have dated it explicitly in the body so readers can judge.

One thing in the draft is not a sourced claim and should not be read as one: "almost every product I have looked at is in the first camp" is my own characterisation from experience, not a survey finding.
