# Design

**Subtitle:** Three major agent launches in three weeks, and none of them shipped to the EU on the same day as the US. That is a roadmap problem, not a legal one.

**Target reader:** A B2B SaaS product manager at a 50–500 person company with paying EU and UK customers, who is shipping an assistant or agent feature in the next two quarters and has been told "legal will sort out the EU part later."

**Key takeaway in one sentence:** The regional gate on frontier agent features is driven by the DMA, GDPR and already-live transparency rules — not by the high-risk AI Act obligations that just got postponed — so region availability is a product decision you design for in the spec, not a compliance cleanup you do the week before launch.

**Section outline:**
1. The week three agents skipped a continent
2. Why the delay you celebrated doesn't cover this
3. What actually gates an agent in Europe
4. Your three options, and what each one costs
5. If you ship inside someone else's assistant, you inherit their map
6. Practical takeaway

**Headline options:**

1. "Three Big Agent Launches, Zero Day-One EU Availability" — *hook: specific surprising result*
2. "The AI Act Delay Bought Your Roadmap Nothing" — *hook: contrarian claim challenging a common PM belief* — **RECOMMENDED**: most PMs read the December 2027 postponement as 14 months of breathing room, and this piece shows the rules actually gating agent launches were never the ones that moved.
3. "Which Of Your AI Features Can Legally Run In Germany?" — *hook: a sharp question most PMs cannot answer confidently*

# Draft

OpenAI's new always-on agents connect to more than [4,000 apps](https://thenextweb.com/news/openai-dots-always-on-ai-agents-cloud-computers-devday). For Pro subscribers in the EEA, the UK and Switzerland, they connect to nothing — because they [don't launch there at all](https://www.trendingtopics.eu/dots-muse-siri-ai-europe/).

That carve-out is the most useful thing to come out of last week's announcements, and almost nobody is writing about it.

## The week three agents skipped a continent

OpenAI announced Dots at [DevDay on September 29](https://www.cnbc.com/2026/09/29/openai-devday-2026-live-updates.html) in San Francisco, alongside roughly twenty other products. Each dot runs on its own cloud machine with its own browser, takes a goal, and keeps working without being prompted.

The availability line is the interesting part. Business Premium gets it in all supported regions. Pro does not launch in the EEA, Switzerland or the UK, and the announcement gives [no dated rollout](https://www.trendingtopics.eu/dots-muse-siri-ai-europe/) for those markets.

It is not an isolated case. Meta's Muse agent launched in the US only. Apple confirmed in June that Siri AI would [not ship in the EU](https://www.apple.com/newsroom/2026/06/due-to-dma-siri-ai-delayed-in-eu-for-ios-27-and-ipados-27/) with iOS 27 and iPadOS 27, though it stays available to European users on macOS and visionOS.

Three companies, three different architectures, same gap on the map. When that happens, it usually isn't a coincidence about any one product.

## Why the delay you celebrated doesn't cover this

Most PMs I talk to have one fact about the EU AI Act in their heads: the deadline moved. That is true. Negotiators [agreed in May](https://www.traverssmith.com/knowledge/knowledge-container/eu-agrees-to-delay-key-ai-act-compliance-deadlines/) to push obligations for stand-alone high-risk systems from August 2026 to [December 2027](https://www.gibsondunn.com/eu-ai-act-omnibus-agreement-postponed-high-risk-deadlines-and-other-key-changes/), and embedded high-risk systems to 2028.

So the natural conclusion is that Europe got easier and you have more than a year to think about it.

Look at what shipped, though. If the high-risk rules were what blocked agent launches, the postponement should have opened the gate. It didn't. The launches that skipped Europe happened months *after* the delay was agreed.

The rules doing the gating are different rules, and none of them moved.

## What actually gates an agent in Europe

Four things, roughly in order of how often they bite.

**The DMA.** This is what Apple names directly. The European Commission's position is blunt: a spokesman said the decision not to launch was "Apple's and Apple's alone," arguing Apple had [been unable to develop interoperability solutions](https://en.ilsole24ore.com/art/siri-isnt-coming-to-europe-its-apples-decision-and-heres-why-AIFu6hgD) meeting EU privacy and security standards. For Meta, gatekeeper status means separate consent before combining data across Facebook, Instagram, WhatsApp and Messenger — and an agent that works across all of them [sits squarely inside those rules](https://www.trendingtopics.eu/dots-muse-siri-ai-europe/). If you are not a gatekeeper this one may not touch you. Your platform partner probably is.

**GDPR, specifically around standing access.** A chatbot sees one prompt. An agent with persistent access to a user's mail, calendar and connected tools is continuously processing personal data — including data about people who never used your product, like everyone who emailed your user. That changes your legal basis, your retention story and whether you need a DPIA.

**Transparency obligations that are already live.** The AI Act's Article 50 disclosure and labelling duties became enforceable on [2 August 2026](https://www.softwareimprovementgroup.com/blog/eu-ai-act-summary/). Those did not get postponed. If your product generates content or converses with EU users, that one applies to you today.

**The DSA**, if you host or distribute anything user-facing at scale.

I'd treat the specific legal reasoning here as informed inference rather than settled fact — OpenAI has not published a reason for its carve-out. But the pattern across three unrelated companies is evidence enough to plan against.

> Region availability stopped being a legal footnote and became a product decision. Make it in the spec, not the week before launch.

## Your three options, and what each one costs

**Ship and gate.** Launch where you can, flag the feature off elsewhere. Cheapest, fastest, and what the big labs just did. The cost lands on your EU account managers, who now sell a product that demos features their customers cannot buy. Decide who owns that conversation before the launch, not after the first renewal call.

**Build a reduced EU variant.** Same feature, narrower permissions: no standing inbox access, explicit per-action approval, shorter retention. Genuinely useful for a lot of B2B workflows, because enterprise buyers often want the approval step anyway. The cost is a second code path and a second set of evals, forever.

**Hold for parity.** Ship nowhere until you can ship everywhere. Defensible if Europe is most of your revenue and the feature is central to positioning. Expensive if it isn't. Meta AI eventually [did reach Europe](https://www.yahoo.com/news/meta-ai-finally-arrives-europe-060003114.html) after working through regulatory friction, so the gate is not permanent — but "eventually" was measured in quarters.

There is no clean answer. There is a wrong process, which is picking by default because nobody asked the question until the release checklist.

## If you ship inside someone else's assistant, you inherit their map

One more thing from DevDay that matters more than it looks. OpenAI is launching plugin extensions — developers can build what the keynote described as [entire applications that feel native to ChatGPT](https://www.progressiverobot.com/2026/09/29/devday-keynote-openai-10am-pt-announcements/), distributed by OpenAI.

That is real distribution. It also means your EU availability becomes a function of your host's EU availability, on your host's timeline, with no say from you.

If a surface like that is in your plan, price in that your reach there may be smaller and less predictable than the headline user number suggests.

Worth noting the mood is not uncritical. On Hacker News the Dots launch drew 750 points and 629 comments, while a privacy analysis of conversational AI agents pulled [422 points the same day](https://github.com/kouweizhu/agents-radar/issues/284). Your EU customers are reading the second one.

## Practical takeaway

Four things you can do this week.

1. **Add a region row to your feature spec template.** For every AI feature in flight: available where, gated where, who tells the customer. One line. It forces the conversation early.

2. **Write down what standing access your agent needs**, separately from what it would merely like. Standing inbox access is the thing that turns a modest compliance question into a hard one. Features that work with per-action approval travel further.

3. **Check your Article 50 position today.** Disclosure and labelling have been enforceable since 2 August 2026. This is the one obligation on this list that is already live and genuinely small to fix.

4. **Ask every AI vendor and platform in your stack one question:** what is your EU and UK availability for this capability, and on what timeline? Put the answer in your build-vs-buy doc. A dependency that cannot serve a third of your customers is not the same dependency.

None of this requires a legal team on retainer. It requires asking in the spec what you would otherwise discover at launch.

# Hero image

**I could not verify a real, usable image for this article.** This session's network policy blocks outbound access to every image host I tried — unsplash.com, images.unsplash.com, pexels.com, openverse.org and commons.wikimedia.org all returned egress denials. I am deliberately not pasting a direct image URL or a license claim I could not load and confirm, because an unverified hotlink is exactly the thing that breaks after publishing.

**What to do instead (two minutes):**

- Unsplash, search `europe map abstract` or `fragmented map` — filter to the Unsplash License, which needs no attribution.
- Pexels, search `world map dark minimal` — Pexels License, no attribution required.
- Openverse, search `map europe` and filter to CC0 if you want a public-domain option.

If you pick a CC BY image, the attribution line to paste under the image on Medium is:

`Photo by [CREATOR NAME] on [SOURCE], licensed under CC BY 4.0`

**Fallback cover image description (use this if you'd rather generate or commission one):** A wide, muted editorial shot of a world map rendered as a sparse dot grid or faint topographic lines on a dark slate background, with the European landmass left visibly empty or unlit while North America and Asia remain densely filled. No robots, no androids, no glowing blue brains. The visual argument should be absence rather than technology — a map with a hole in it. A desaturated palette with one warm accent reads well against Medium's white body text at the 1500x750-ish crop Medium favours, and the empty region should sit right of centre so the headline overlay doesn't cover it.

# Metadata

**Tags:** Product Management, Artificial Intelligence, AI Agents, Product Strategy, Tech Regulation

## Unverified claims

Honest accounting of what I could and could not confirm.

- **Blocked source verification.** This environment's network policy denied outbound access to nearly every news domain I tried (openai.com, thenextweb.com, medianama.com, prnewswire.com, trendingtopics.eu, technology.org, nerdschalk.com, felloai.com, cnbc.com and others). Only github.com was reachable. Every claim below therefore rests on search-result content and dated source URLs rather than on me loading the page and reading its publication date. The links in the draft are correct as destinations but I did not render them.
- **Freshness window.** DevDay itself was 29 September 2026, which falls just outside a strict 48-hour window from 2 October. What is inside the window is the analysis and debate wave: the Europe-exclusion coverage dated 30 September–1 October, and the Hacker News discussion of 1 October. I chose the topic on that basis and am flagging the launch date rather than implying the launch was yesterday.
- **Dots regional carve-out.** That Pro does not launch in the EEA, Switzerland and the UK while Business Premium is available in all supported regions comes from secondary reporting, consistent across several outlets. Not confirmed against OpenAI's own announcement, which I could not load.
- **Reason for the carve-out.** OpenAI has published no reason. The DMA/GDPR/DSA explanation is inference from the Apple and Meta cases plus commentary, and the draft says so in the text rather than only here.
- **Dots product details** (GPT-6 Astra, 4,000+ apps, own cloud computer and browser, first dot at no extra cost) — secondary reporting only. I did not include a Dots subscription price in the draft because sources disagreed.
- **DevDay scale** (~2,500 attendees, 20+ products) — secondary reporting, not verified against OpenAI.
- **Apple Siri AI / EU.** The Apple Newsroom URL is dated June 2026 and the substance is widely reported; I could not load the page. The Thomas Regnier quote is reproduced as an English-language outlet rendered it and may be a translation rather than his exact words.
- **EU AI Act dates.** The move of Annex III high-risk obligations to 2 December 2027, Annex I to 2 August 2028, and Article 50 transparency becoming enforceable 2 August 2026, come from several law-firm summaries that agree with one another. Not checked against the published Official Journal text. The "3:47 AM Brussels time on 7 May 2026" detail appeared in one source only, so I left it out of the draft and reduced it to "agreed in May."
- **Hacker News numbers** (Dots 750 points / 629 comments; privacy analysis 422 points, both 1 October) — from a third-party HN digest on GitHub, the one source I could actually load. Not checked against news.ycombinator.com, which was blocked.
- **Hero image.** No image verified. See that section — I did not present a link I could not confirm.
