# Design

**Subtitle:** Agent Skills moved to a neutral foundation yesterday. The spec it moved with still has no tagged releases, and no written rule for who can change it.

**Target reader:** B2B SaaS PM at a 50–200 person company whose product has an extensibility or agent surface, and who has either shipped Agent Skills support or has it on the roadmap this quarter.

**Key takeaway:** The donation to the Agentic AI Foundation reduces vendor-capture risk but does not yet give you anything to pin, diff, or point a security reviewer at — so the compatibility promise in your docs is currently stronger than the standard's promise to you.

## Headline options

1. **280 Million Installs, Zero Version Numbers** — *RECOMMENDED*
   Hook type: specific surprising number. Reason: both halves are verifiable from primary sources, the gap between them is the entire article, and it pays off in the second section rather than teasing.

2. **A Linux Foundation Donation Is Not a Stability Guarantee**
   Hook type: contrarian claim. Challenges the common PM reflex that foundation governance means a dependency is now safe to build on.

3. **Which Version of Agent Skills Does Your Product Support?**
   Hook type: sharp question the reader cannot answer confidently — because, today, there are no versions to answer with.

## Section outline

- Open on the two facts that belong in one sentence
- What actually moved (the donation, the numbers, the maintainers)
- Read the project proposal, not the press release (living document; no written approval rule)
- Why this is a product decision, not a platform problem
- The security guidance does not exist yet either
- The adoption numbers disagree with each other
- Practical takeaway

# Draft

*Word count: 1,086 (target 1,000–1,400).*

Yesterday Anthropic handed the Agent Skills standard to a neutral foundation. The specification it handed over does not have version numbers.

Those two facts belong in the same sentence, and most of the coverage I read kept them in separate paragraphs.

## What actually moved

On October 22, Anthropic [donated the Agent Skills standard](https://www.anthropic.com/news/donating-agent-skills-to-the-agentic-ai-foundation) to the Agentic AI Foundation, which operates under the Linux Foundation. The donation covers the Agent Skills name and logo, the GitHub organization, and the agentskills.io domain. Anthropic co-founded the AAIF with Block and OpenAI, and had [already donated the Model Context Protocol](https://www.anthropic.com/news/donating-agent-skills-to-the-agentic-ai-foundation) to the same home.

The adoption figures in the announcement are genuinely large. Anthropic says [more than 70 agent platforms](https://www.anthropic.com/news/donating-agent-skills-to-the-agentic-ai-foundation) have integrated Agent Skills since the standard was published in December 2025, with roughly 1 million skills published and nearly 280 million installed.

Going forward, engineers from Anthropic, Google, OpenAI and other companies will [maintain the standard as individuals](https://www.anthropic.com/news/donating-agent-skills-to-the-agentic-ai-foundation), with David Soria Parra and Mahesh Murag as lead maintainers.

If your product has an extensibility surface, that all reads like good news, and some of it is. A format you may already depend on is no longer steered by a single vendor.

## Read the project proposal, not the press release

The foundation's own [Agent Skills project proposal](https://github.com/aaif/project-proposals/issues/47) is the more useful document, because it describes the current state rather than the intended one.

Two lines in it matter more than anything in the announcement.

The first: "The specification and documentation are maintained as living documents on main and published continuously." No tagged release. No changelog. Moving "from a living document to tagged releases with a changelog" is [listed as roadmap work](https://github.com/aaif/project-proposals/issues/47) — which means that today, what those 70-odd platforms implement is whatever sits on `main` this morning.

The second: "Today, spec changes are merged on GitHub without a written approval rule." Not an ambiguous rule, or a rule under review. No written rule.

The proposal is refreshingly candid about the rest. A Technical Steering Committee, a GOVERNANCE.md, a MAINTAINERS.md, CI on every pull request and an OpenSSF Best Practices badge are all [described as onboarding work](https://github.com/aaif/project-proposals/issues/47), not as things that currently exist. It also states plainly that "today the maintainers listed above are all at Anthropic."

> A donation transfers ownership. It does not retroactively create the release engineering that ownership was missing.

## Why this is a product decision, not a platform problem

Here is the practical shape of the problem.

Your product makes a compatibility promise. "We support Agent Skills" sits in your docs, your sales deck, maybe your pricing page. That sentence has an implicit version in it: the customer assumes a skill that worked last month still works this month.

The standard underneath that promise currently makes no matching commitment. You cannot pin it, because there is no release to pin to. You cannot diff versions, because there are none. If a normative detail shifts on `main`, the way you find out is a customer bug report.

None of which is an argument against adopting Agent Skills. The format has real gravity: the project's own Client Showcase listed 46 agent products shipping support as of September 21, 2026, and [44 of those 46 were built by organizations other than Anthropic](https://github.com/aaif/project-proposals/issues/47). The donation also genuinely lowers the odds that one vendor reshapes the format around its own client.

It is an argument for demoting "supports the standard" from a stable claim to a managed dependency.

The gap is not news to the community, either. A contributor filed a [semantic versioning proposal](https://github.com/agentskills/agentskills/discussions/415) in June 2026, arguing that "many agent frameworks lack a consistent mechanism for communicating compatibility guarantees when skills evolve." It was marked a community contribution, drew [no maintainer reply, and was closed as a duplicate](https://github.com/agentskills/agentskills/discussions/415) to consolidate discussion elsewhere. Four months on, versioning is still a roadmap line.

## The security guidance does not exist yet either

Anthropic's roadmap also includes [security guidance for people who write and install skills](https://www.anthropic.com/news/donating-agent-skills-to-the-agentic-ai-foundation). Note the tense.

A skill is natural-language instruction text that runs with your agent's tool access. If your product lets customers install skills, you have shipped a path for third-party instructions to reach your agent's permissions — and right now there is no official guidance document to hand your security reviewer.

I would not overstate this. Naming security guidance as a roadmap item is better than not naming it, and the donation is the start of fixing the governance gap rather than evidence of neglect. But a roadmap item is not a control. Until it ships, install-time review is entirely yours to design.

## The adoption numbers disagree with each other

One smaller thing, because it will show up in your own internal deck.

Anthropic's announcement says [more than 70 agent platforms](https://www.anthropic.com/news/donating-agent-skills-to-the-agentic-ai-foundation). The project proposal, dated September 21, 2026, says the Client Showcase ["lists 46 agent products that have shipped support for the format"](https://github.com/aaif/project-proposals/issues/47).

Both are probably true of different things — different dates, different definitions of platform versus product, different inclusion rules. But if you quote one as *the* adoption number without naming the document, someone will eventually find the other. Cite the source on the slide.

## Practical takeaway

If your product supports Agent Skills now, or is scheduled to:

1. **Pin to a commit, not to "the spec."** Record the specification `main` SHA you built against in your own repo. It is the only version identifier that currently exists.
2. **Write your own conformance subset.** One page listing the specific spec behaviors your product actually relies on. When `main` moves, you diff against that page instead of re-reading the whole document.
3. **Name an owner for spec drift.** Someone should watch the [agentskills repository](https://github.com/agentskills/agentskills) and the Discussions where proposals land. It is a twenty-minute-a-week job that prevents a bad quarter.
4. **Decide your install-time review now.** Who signs off before a third-party skill reaches your agent's tool access? Write it down while the official guidance is still a roadmap item, then revise it when guidance lands.
5. **Date the docs claim.** Replace "supports Agent Skills" with the commit or date you validated against. It costs nothing and it is true.
6. **Watch for artifacts, not announcements.** The real maturity signals are the first tagged release and a merged GOVERNANCE.md. When those appear, revisit items 1 and 2.

The donation is good news. It is just earlier news than the headlines suggest: the governance that makes a standard dependable is still roadmap, and until it arrives, the compatibility promise your customers hear is one you are making on your own.

# Hero image

**Important:** I could not independently verify either image below. This environment's network policy blocks `unsplash.com`, `pexels.com`, `openverse.org`, the Openverse API and `commons.wikimedia.org`, so I could not load the photo pages to confirm the files exist, capture their direct CDN image URLs, or read the license text. The details below come from search results, not from the source pages. **Open each page and confirm before publishing.** I have not invented any URL, but I also cannot vouch for these.

### Primary candidate

- **Photo page:** https://unsplash.com/photos/building-under-construction-with-scaffolding-and-blue-sky-UK3vs6Z7PaE
- **Direct image URL:** not captured — Unsplash's CDN path (`images.unsplash.com/photo-...`) is not derivable from the page slug, and the page is unreachable from here. Use the Download button on the photo page.
- **Photographer:** Troy Mortier (@troyscanon)
- **License (per search result, unconfirmed):** Unsplash License — free for commercial use, no attribution required
- **Why it fits:** A building everyone is already working on, held up by scaffolding that is explicitly temporary. Editorial and abstract rather than a robot cliché.
- **Optional attribution line:** Photo by [Troy Mortier](https://unsplash.com/@troyscanon) on [Unsplash](https://unsplash.com)

### Backup candidate

- **Photo page:** https://www.pexels.com/photo/scaffolded-building-under-construction-against-blue-sky-35757191/
- **Direct image URL:** not captured — same reason as above.
- **Photographer:** not shown in search results; check the page
- **License (per search result, unconfirmed):** Pexels License — free for commercial use, no attribution required
- **Why it fits:** Same visual idea from a second source, so if the Unsplash page has gone the theme survives.
- **Optional attribution line:** Photo from [Pexels](https://www.pexels.com)

### Fallback description, if neither verifies

A wide, slightly underexposed editorial shot of scaffolding on an unfinished building, framed so the scaffolding fills the left two-thirds and open sky occupies the right — leaving clean negative space for a Medium title overlay. Cool blue-grey tones, strong diagonal lines, no people and no visible branding. The idea to convey is a structure already in use while its supports are still provisional: plenty of people standing on something whose final form has not been fixed. Avoid robots, androids, glowing brains and circuit-board motifs.

# Metadata

**Tags:** Product Management, AI Agents, Open Source, Developer Platform, Technology Standards

## Unverified claims

- **Snyk's malicious-skills research — deliberately excluded.** Several secondary sources attribute figures to a Snyk "ToxicSkills" audit (variously 3,984 skills scanned, 534 critical, 1,467 with any issue, 76 confirmed malicious payloads, 36% containing prompt injection). The accounts contradict each other, `snyk.io` is blocked from this environment, and I could not reach the OWASP or Cloud Security Alliance pages citing it either. I left all of it out of the draft rather than cite numbers I could not check. If you want the security section to carry a hard number, verify it at the source first.
- **Adoption figures are each single-sourced.** The ">70 agent platforms", ~1 million skills published and ~280 million installs figures come only from Anthropic's own announcement; the "46 agent products / 44 non-Anthropic" figures come only from the AAIF project proposal. Neither is independently audited, and as the draft notes, they do not reconcile with each other.
- **Linux Foundation press release not read.** Search results reference a release announcing four AAIF projects (Agent Skills, Open Responses, OpenEnv, OpenSandbox). `linuxfoundation.org` is unreachable from here, so I did not cite it or rely on it.
- **Simon Willison's commentary not read.** A post dated Oct 22, 2026 on the donation appears in search results, but `simonwillison.net` is blocked here, so no commentary from it informed the draft.
- **Both hero images are unverified**, for the reasons stated in full in the Hero image section. Licenses are as reported by search snippets, not read from the source pages.
- **Everything else is sourced to a primary document I fetched and read directly:** Anthropic's announcement of October 22, 2026, AAIF `project-proposals` issue #47, and `agentskills` discussion #415. All quoted sentences come from those three.
- Fresh-material note: there was enough genuinely 48-hour material for this article. The donation was announced October 22, 2026 and verified against Anthropic's own page.
