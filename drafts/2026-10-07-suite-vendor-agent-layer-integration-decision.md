# Design

## Headline options

1. **SAP Shipped 224 Agents. Three Percent of Customers Use Them.** *(hook: two specific numbers whose gap is the whole argument)*
2. **Your AI Roadmap Matters Less Than Your Integration Policy** *(hook: contrarian claim against the common PM belief that the AI feature list is the strategic work)*
3. **When Your Customer's ERP Grows an Agent, Who Calls You?** *(hook: a sharp question most PMs cannot answer confidently about their own product)*

**RECOMMENDED: Option 1** — the two numbers are the article's actual spine, both are sourced, and the piece pays the headline off instead of teasing it.

## Subtitle

A suite vendor just turned on an agent layer across finance, procurement, HR and supply chain. The decision it forces on you is not about building agents.

## Target reader

A B2B SaaS product manager at a 50–500 person company whose product sits inside or next to an enterprise workflow (spend, invoicing, procurement, HR ops, logistics) and whose customers run a large suite like SAP, Salesforce or Microsoft. Also useful to internal platform PMs who own integrations into those suites.

## Key takeaway

When a suite vendor ships an agent layer, the strategic question is not whether to build your own agents — it is whether your product stays reachable when the agent, not a person, decides which tool to call, and the vendor's endorsed-integration rules decide that for you.

## Section outline

1. Open on the two numbers from October 6 and February 2026
2. What actually shipped
3. The adoption number that says don't panic
4. The API policy that says don't wait either
5. The real decision: front door, tool, or both
6. How to size the bet when adoption is 3%
7. Why this is not only an SAP story
8. Practical takeaway

---

# Draft

## SAP Shipped 224 Agents. Three Percent of Customers Use Them.

On October 6, SAP used its Connect conference to [expand Joule from an assistant into what it calls an agentic work layer](https://siliconangle.com/2026/10/06/sap-expands-joule-into-an-agentic-work-layer-as-autonomous-enterprise-goes-live/), with its Autonomous Enterprise architecture going live across lines of business.

Eight months earlier, SAP's German-speaking user group surveyed 198 member companies and found [3% investing in SAP Business AI while 43% invested in AI generally](https://change-orchestration.com/en/articles/dsag-investitionsreport-2026-sap-ai).

Both numbers are real. The gap between them is where your next planning cycle actually lives.

## What shipped

SAP's pitch at Connect was a three-layer stack: a platform underneath, an autonomous suite of agents in the middle, and Joule as the layer people and agents actually work through. The suite tally SAP has been quoting — [224 agents and 51 domain-specific Joule Assistants](https://sapinsider.org/blogs/at-sap-connect-sap-expands-joule-across-every-line-of-business) spanning finance, spend, supply chain, HR and customer experience — got named reference deployments rather than a bigger number.

The part that matters for anyone building adjacent software is quieter. Joule Studio lets customers build agents that reach tools over [Model Context Protocol and the Agent2Agent protocol](https://sapinsider.org/blogs/at-sap-connect-sap-expands-joule-across-every-line-of-business), and SAP says bi-directional A2A — third-party agents calling Joule agents, and the reverse — is [slated for general availability around Q4 2026](https://www.altivate.com/insights/white-papers/sap-ai-live-vs-roadmap/).

So there is a defined way for your product to be something the suite's agent calls. That is new, and it is not neutral.

## The number that says don't panic

Three percent is a small number, and it is worth sitting with before you reshuffle a roadmap.

The same user-group survey found [77% of AI-active SAP enterprises using non-SAP AI solutions](https://change-orchestration.com/en/articles/dsag-investitionsreport-2026-sap-ai), with licence complexity and heavily customised landscapes cited as the barriers. Analysts covering the survey described customer spending as [selective, with AI dragging](https://www.constellationr.com/insights/news/dsag-sap-customer-spending-selective-ai-drags).

Nor is the agent catalogue as finished as the count implies: most of those 224 agents and 51 assistants sit in [mixed GA, early-adopter and preview status](https://www.innobu.com/en/articles/sap-joule-2026-agentic-enterprise-ai.html). Reporting earlier this year had large customers including Volkswagen finding Joule [short on maturity and cost-effectiveness](https://www.gurufocus.com/news/8651387/sap-faces-skepticism-over-ai-tool-joule).

If your bet is that enterprise buyers will route daily work through their ERP's agent by next quarter, the evidence does not support it yet.

## The policy that says don't wait either

Here is the part that is easy to miss, because it is a licensing document rather than a launch.

SAP published an API policy this year that [restricts third-party access to its published APIs and specifically addresses autonomous and generative AI systems](https://aimagazine.com/news/can-ai-agents-still-access-sap-data-under-new-api-rules). The prohibition, as read by practitioners in SAP's own community, covers [integration with semi-autonomous or generative systems that plan, select or execute sequences of API calls](https://community.sap.com/t5/technology-blog-posts-by-members/sap-s-api-policy-on-ai-agents-what-it-prohibits-allows-and-leaves-open/ba-p/14475119), except through endorsed architectures — an MCP gateway on the integration suite, SAP-provided MCP servers, or A2A.

Read those two things together. The suite is opening a door for agents to call your product, and closing the one where your agent calls theirs on its own terms.

Forrester has been blunt about the direction, arguing SAP is [positioning itself as a gatekeeper of enterprise AI and that CIOs should push back](https://www.forrester.com/blogs/sap-is-attempting-to-become-the-gatekeeper-of-enterprise-ai-cios-should-push-back/), and separately that the autonomous-enterprise story is credible but carries [concentration risk](https://www.forrester.com/blogs/sap-sapphire-2026-the-autonomous-enterprise-is-credible-but-it-comes-with-concentration-risk/). Whether or not you share the alarm, the practical point holds: the integration route is being defined now, while adoption is still low.

> Adoption tells you how fast to move. Policy tells you what you will be allowed to do when you get there.

## The decision you actually own

Strip away the agent talk and there are three positions, and most PMs have not said out loud which one they are in.

**Front door.** Your UI stays where the work happens. You invest in your own experience and treat the suite as a system of record you sync with. Defensible when your product's value is in judgment, collaboration or craft that does not compress into a tool call.

**Tool.** You make your product callable — clean, documented, permissioned actions the suite's agent can invoke — and accept that your interface is seen less often. You trade surface area for being present at the moment the work happens.

**Both.** You keep your UI and ship a callable surface, knowing you will maintain two front doors and that your analytics will get harder to read.

Nobody avoids this by not choosing. Not choosing is the front-door position with no one defending it.

## Sizing the bet honestly

The asymmetry is what makes this tractable. Being uncallable in 2028 is expensive and slow to fix; being callable early is cheap if you scope it to what you already expose.

That argues for a small, specific move rather than an agent strategy. Pick the two or three actions in your product that an enterprise agent would plausibly want — create the request, check the status, approve within a limit — and make exactly those callable, with real permissions and an audit trail. That is weeks of work, not a quarter.

What it does not argue for is rebuilding your product around someone else's orchestration layer on 3% adoption. The honest read: the protocol work is a hedge worth buying, and the platform bet is not yet worth making.

## This is not only an SAP story

The same shape is appearing in every large suite. Microsoft has been adding deterministic control points to Copilot Studio — [hooks that fire a workflow every time a defined event occurs, such as before a tool runs](https://learn.microsoft.com/en-us/microsoft-copilot-studio/agents-experience/hooks-overview), rather than when the model decides it is relevant. Salesforce used Dreamforce this year to put [a CRM reasoning model behind Agentforce](https://www.salesforce.com/blog/dreamforce-2026-announcements/).

Different vendors, same move: the suite wants to be the layer that decides which tool runs. Your product is on one side of that decision or the other.

## Practical takeaway

Four things worth doing in the next two weeks:

1. **Write down your position.** Front door, tool, or both — one sentence, shared with engineering and sales. Most of the confusion in these conversations is that different people assume different answers.
2. **Audit your top three actions.** Which operations in your product would an agent want to invoke? Can they be called with scoped permissions today, and is there a record of who or what called them?
3. **Read your biggest platform partner's API terms, not their keynote.** Ask specifically whether agent-mediated calls are permitted, and through which route. This is where the constraint lives.
4. **Instrument the share of actions that arrive non-interactively.** Today it is probably near zero. That line moving is your signal to invest, and you want the baseline before it moves.

The uncomfortable part of this decision is that it does not come with a deadline. Nothing breaks if you skip it this quarter. You just find out later, from a customer, that their agent could not reach you.

---

# Hero image

**I could not verify either candidate first-hand.** This session's network egress blocked `unsplash.com` and `pexels.com`, so I could not open the photo pages to confirm they exist, check the photographer credit, or read the licence. The two candidates below came back from web search against those domains and are leads to verify manually, not confirmed images. Please open each before publishing.

### Candidate 1 (to verify)
- Source page as surfaced by search: `https://unsplash.com/photos/modern-architectural-structure-with-layered-abstract-shapes-Qm-LWk_KX_M`
- Described in search results as: "Modern architectural structure with layered, abstract shapes," free photo, Unsplash License
- Direct image URL: **not obtained** — Unsplash direct `images.unsplash.com` URLs must be read off the photo page, and the page was unreachable
- Photographer: **unknown** — not shown in search results
- Licence: search results indicate Unsplash License (free for commercial use, attribution appreciated but not required). **Unconfirmed.**
- Why it fits: layered horizontal structure reads as stacked platform layers without any robot imagery

### Candidate 2 (to verify)
- Source page as surfaced by search: `https://www.pexels.com/photo/abstract-minimalist-concrete-architecture-30167961/`
- Described in search results as: minimalist abstract concrete architecture, free stock photo
- Direct image URL: **not obtained** — page unreachable
- Photographer: **unknown**
- Licence: Pexels License per site-wide terms (free for commercial use, no attribution required). **Unconfirmed for this specific photo.**

### Attribution line
Not written, because neither photographer is confirmed. If Candidate 1 checks out, the Unsplash convention is:
`Photo by [Photographer Name] on Unsplash`

### Fallback cover-image description

A tight, abstract architectural photograph of a modern facade shot from below, so that three or four horizontal bands of concrete and glass stack cleanly across the frame with the top band partly cut off. Cool neutral palette — grey, off-white, a little sky — with strong directional light creating one hard shadow line between layers. No people, no screens, no robots. The read should be "layers of a stack, one of them above you," which is the article's argument: a platform layer has appeared above your product, and the question is how your layer connects to it. Shot wide with generous negative space on the left so a Medium title overlay sits comfortably.

---

# Metadata

**Medium tags:** Product Management, Artificial Intelligence, Enterprise Software, API, Product Strategy

---

## Unverified claims

- **Publication dates were not confirmed on source pages.** This session's network egress proxy blocked almost every domain I tried to fetch directly (`siliconangle.com`, `news.sap.com`, `sapinsider.org`, `www.sap.com`, `learn.microsoft.com`, `techcrunch.com`, `prnewswire.com`, `blog.mean.ceo`, `aiagentsdirectory.com`, `unsplash.com`, `pexels.com`). Dates below rest on datestamps in URLs and on search-result metadata, not on a first-hand read of the page. Every claim in the draft should be spot-checked against its link before publishing.
- **The 48-hour peg is the SAP Connect news of October 6, 2026** (Joule as agentic work layer, Autonomous Enterprise going live). The SiliconANGLE URL carries `/2026/10/06/` and search metadata agrees, but I could not open the article.
- **The "224 agents and 51 Joule Assistants" count** was, per search results, first announced at SAP Sapphire earlier in 2026 and restated at Connect with named reference deployments. I could not confirm on a primary page whether SAP quoted the same figures on October 6 or revised them. Treat the number as SAP's own marketing tally either way.
- **Q4 2026 general availability for bi-directional A2A** comes from a partner-authored roadmap summary, not from SAP's own roadmap document. SAP roadmap timing changes routinely; verify before repeating.
- **The 3% / 43% / 77% figures** are from the DSAG Investment Report 2026 (survey of 198 member companies, fielded December 2025–January 2026, published February 2026) as reported by secondary sources. I did not read DSAG's own report.
- **The API policy reading** — that it prohibits agent-mediated API call sequences except through SAP-endorsed architectures — is practitioner and press interpretation of SAP's policy document, not a quote from the policy itself. This is a licensing question with real commercial consequences; have someone read the actual policy text rather than relying on this article.
- **The Volkswagen maturity and cost-effectiveness criticism** is secondary reporting of earlier 2026 coverage. I could not reach the original.
- **The Forrester positions** (SAP as gatekeeper, May 2026; concentration risk, Sapphire 2026) are cited from blog titles and search summaries; I did not read either post in full.
- **The Salesforce Dreamforce 2026 Agentforce reasoning-model claim** is from a search summary of Salesforce's own announcements blog. Date not confirmed, and it is background rather than 48-hour news.
- **The Microsoft Copilot Studio "hooks" description** matches Microsoft's documentation as summarised in search results; the page itself was unreachable. Hooks are in preview, so behaviour may change.
- **Both hero-image candidates are unverified**, as stated in the Hero image section. No image existence, photographer or licence was confirmed first-hand.
