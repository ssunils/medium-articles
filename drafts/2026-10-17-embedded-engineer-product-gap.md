# Design

**Subtitle:** The forward-deployed engineer boom is a measurement of how far your AI product still is from working on its own.

**Target reader:** A B2B SaaS PM at a 50–500 person company whose AI feature is already in production, where the accounts that are succeeding are the ones that got hands-on help from your team.

**Key takeaway:** Embedded engineers are a reasonable investment only if each deployment measurably reduces the work the next one needs — if hours per deployment aren't trending down, you've quietly started a services business instead of shipping a product.

**Format:** adoption-brief

**Section outline:**
1. Open on the contradiction: two opposite, well-funded bets landing in the same window
2. The hiring numbers, and what the market has priced
3. What the embedded engineer is actually buying (specification, not intelligence)
4. Decagon's real position vs. the slogan attached to it
5. The ratio that settles the question for your team
6. Why PMs end up on the wrong side of it
7. Practical takeaway
8. What I'd watch next

**Headline options:**

1. **7,300 Job Ads Say Your AI Product Isn't Finished**
   *(Hook: specific surprising number.)*

2. **Stop Calling White-Glove AI Onboarding a Go-To-Market Win**
   *(Hook: contrarian claim challenging a common PM belief.)*

3. **Could Your AI Feature Ship Without the Engineers Deploying It?** — **RECOMMENDED**
   *(Hook: a sharp question the reader cannot answer confidently. It's the exact question the article hands the reader a test for, so the headline promises nothing the body doesn't deliver.)*

---

# Draft

*Word count: 1330 (link URLs excluded; target 1000–1400).*

Two well-funded bets landed within about two weeks of each other, and they contradict each other.

Anthropic committed $100 million to train 10,000 deployment engineers by the end of 2027, with first cohorts nominated from Accenture, Bain, Capgemini, Deloitte, McKinsey, Morgan Stanley and others ([Anthropic](https://www.anthropic.com/news/claude-frontier-academy)). AWS had already put $1 billion into its own forward-deployed engineering unit, staffed from internal teams and outside hiring ([CNBC](https://www.cnbc.com/2026/06/30/aws-amazon-ai-forward-deployed-engineers.html)). On October 15, CNBC described the three largest players as racing to field these engineers, and tied the push directly to investor doubt about whether AI spending will produce a return ([CNBC](https://www.cnbc.com/2026/10/15/aws-anthropic-racing-to-deploy-army-of-specialized-ai-engineers.html)).

Meanwhile Decagon reportedly crossed $100 million in annualized revenue while declining to build a forward-deployed engineering team at all, on the stated grounds that leaning on embedded engineers is evidence the software is too hard to use ([Newcomer](https://www.newcomer.co/p/decagon-hit-100-million-betting-against), [PYMNTS](https://www.pymnts.com/news/artificial-intelligence/2026/enterprise-ais-hottest-job-just-found-its-biggest-skeptic)).

Both camps are selling AI to enterprises. They disagree about whether a human in the customer's building is the solution or the symptom.

That disagreement is worth your attention, because if you have an AI feature in production right now, you are probably answering this question already — just without noticing that you've answered it.

## The number the market has already priced

U.S. job postings for forward-deployed engineers went from fewer than 200 in 2023 to more than 7,300 across the first nine months of 2026, according to Lightcast data cited by CNBC. Median advertised salary came in at $195,456, up about 40% from 2023 and roughly three times the median across all U.S. postings ([CNBC, via FourWeekMBA](https://fourweekmba.com/ai-awss-1b-fde-push-meets-openais-4b-deployment-company/)).

The most interesting part isn't the growth rate. It's who is posting.

The largest advertisers are Deloitte with 872 unique postings and Accenture with 688, ahead of Google at 499 and KPMG at 447 ([Lightcast](https://lightcast.io/resources/blog/forward-deployed-engineer-ai-job)). The gap between "the model works" and "it works here" is being filled mostly by services firms, not by the people who built the models.

So the market has put a price on that gap: roughly $195,000 a head, plus margin, per enterprise deployment.

If your product requires a scaled-down version of the same thing — a solutions engineer, a customer-success person who writes prompts, a founder who gets on the call — you are paying that price too. You're just paying it out of a different budget line, and probably not tracking it.

## What the embedded engineer is actually buying

The honest answer is not intelligence. It's specification.

Forbes, covering the same hiring surge, landed on undocumented process knowledge as the core obstacle: enterprises run on business logic that lives in people's heads and was never written down anywhere a system could read it ([Forbes](https://www.forbes.com/sites/ronschmelzer/2026/09/19/why-forward-deployed-engineers-are-suddenly-in-high-demand/)).

That reframes the whole thing. The embedded engineer isn't there because the model is weak. They're there because nobody has ever written down how this particular company does returns, or approvals, or escalations — and your product assumed someone had.

> An embedded engineer is a very expensive way to discover your own requirements. Worth it once. Ruinous as a habit.

The distinction matters because the two readings lead to opposite roadmaps. If the problem is intelligence, you wait for better models. If the problem is specification, you build the surfaces that let a customer state their own rules — and you ship those instead of flying someone out.

## Decagon's real position is more useful than its slogan

It's worth reading past the headline version of Decagon's stance, because the company does do field work.

Sunny Rekhi, who leads forward-deployed engineering there, describes the role as advisers who turn one-off customer work into self-serve product features, with forward-deployed and product engineering sharing a reporting structure ([daily.dev](https://daily.dev/posts/how-forward-deployed-engineering-is-done-at-decagon-sunny-rekhi-yttztofti), [BigGo Finance](https://finance.biggo.com/news/25bf3c9c39d661d1)).

So the real split isn't embedded engineers versus none. It's whether what the engineer learns in the field reliably ends up in the product — or dies in a customer-specific repo that one person maintains.

Critics make a fair counterpoint: rivals reportedly win large accounts precisely on the hands-on model Decagon won't build, and Decagon hasn't published retention figures ([ValueAdd VC](https://valueaddvc.com/pulse/decagon-100m-arr-ai-customer-agents-2026)). Treat the $100M ARR claim as the company's own number.

## The ratio that settles it for your team

Here's the test I'd actually apply, and it doesn't require you to pick a side in the industry argument.

Measure the human hours it took to get your AI feature working for each of your last five or six deployments. Not sales hours — implementation hours. Then look at the slope.

If deployment three took 60% of the hours deployment one took, and deployment six took 30%, your embedded work is compounding. Each engagement is finding a gap, and the gap is getting closed in the product.

If it's flat, every deployment is being solved from scratch. The learning is going into people's heads and customer-specific configuration, not into anything a new customer benefits from.

Flat is the condition to worry about, and it's easy to miss, because flat still looks like growth. Revenue goes up. Logos go up. Headcount goes up right alongside them, and the two curves never separate.

I should be straight that I haven't found a public benchmark for what a healthy slope looks like across companies. This is a diagnostic to run on your own numbers, not a figure I can source.

## Why PMs end up on the wrong side of this

Mostly because the hands-on version works, immediately and visibly.

A customer is stuck, an engineer goes in, the deal closes. Nobody involved is rewarded for noticing that the same gap has now been closed by hand four times. The account team gets credit for saving the account. The engineer gets credit for the save. The gap stays open.

This is also where the instrumentation argument gets concrete. Mixpanel shipped Agent Intelligence on October 1, aimed at exactly this blind spot: tying agent conversations to the same user identity as other product events so teams can see task resolution rates and drop-off points rather than counting custom events ([PR Newswire](https://www.prnewswire.com/news-releases/mixpanel-introduces-agent-intelligence-helping-product-teams-build-and-measure-more-effective-ai-agents-302895602.html)). That's vendor framing, and the product is in early access — but the problem it names is real. Most teams genuinely cannot tell which accounts are self-sufficient and which are being carried.

And there is pushback on the vendor side of the trade, too. CIO ran a piece arguing that enterprises don't want more vendor engineers in the building, and that the labs are misreading what buyers are asking for ([CIO](https://www.cio.com/article/4233864/stop-sending-me-engineers-what-openai-anthropic-and-microsoft-misread-about-enterprise-ai.html)). If that's broadly true, the services-heavy model has a ceiling, and it's worth not building your roadmap on the assumption that customers will always accept hand-holding.

## Practical takeaway

Four things you can do this week:

1. **Pull implementation hours for your last five or six AI deployments** and chart the slope. One afternoon of work. If nobody logged the hours, that's your first finding.

2. **Make the gap a ticket, not a favor.** Every time an engineer or CSM solves something by hand, require a one-line entry naming what the product couldn't do. Review the list monthly and look for the same entry appearing more than twice — that's your next roadmap item, already validated.

3. **Separate the two kinds of custom work.** Work that exposes a missing product surface is investment. Work that only serves one account's unwritten process is cost. Name which is which on every engagement, out loud.

4. **Set a number before you hire.** If you're about to add implementation headcount, write down the hours-per-deployment figure you expect it to reach in two quarters. Hiring against an unstated expectation is how a product company becomes a services company without anyone deciding to.

The useful thing about this week's news is not that AWS and Anthropic are spending heavily on embedded engineers. It's that they're doing it because the deployment gap turned out to be the binding constraint, not model quality. If that's true for them, with their resources, it's almost certainly true for your feature.

The question isn't whether you need humans in the loop right now. You probably do. The question is whether the number is going down.

---

# Hero image

**I could not verify any image for this article, and I'm not going to present a link I couldn't open.**

This session's network policy blocked outbound page fetches: every attempt to open unsplash.com, pexels.com and other hosts failed (DNS refusal through the agent proxy, and `403` on the CONNECT tunnel via curl). Web *search* worked, but confirming that an image exists at a URL and reading its license text requires loading the page, and I couldn't. Candidate URLs below came from search results only — treat them as leads to check manually, not as verified assets.

**Unverified candidate leads (check before use):**
- Pexels photo IDs `2182981` and `8062306` surfaced in search as free-to-use two-person office/laptop photos. Existence and license text unconfirmed.
- One Unsplash result matching this theme (`O6may9pAdKs`, two engineers at a desk with tablet and laptop) appeared in search as **Unsplash+**, which is the paid tier. Likely not usable for free — noted so the lead isn't chased.

**Fallback cover image description (use this to pick one manually):**

A wide, editorial overhead shot of an ordinary working desk at a slight angle: an open laptop pushed off-center, a notebook with handwritten notes beside it, and a second chair pulled in close — empty. Muted, natural light; cool greys and desaturated blues; plenty of clean negative space in the upper third for the Medium title overlay. The empty second chair is the point: it reads as the person who was brought in to make this work and has now left, which is exactly the article's question. Avoid robots, androids, glowing brains, circuit-board motifs and anything with visible AI iconography — the piece is about staffing and specification, not about machines. Crop to roughly 2:1 for Medium's cover treatment.

If you want attribution ready to paste once you've picked one: Unsplash images need no attribution under the Unsplash License but crediting is encouraged as `Photo by [Name] on Unsplash`; Pexels is the same pattern, `Photo by [Name] from Pexels`. Fill in the name from the page you actually open.

---

# Metadata

**Medium tags:** Product Management, Artificial Intelligence, Enterprise Software, SaaS, Product Strategy

---

## Unverified claims

Before the list, one honest caveat about method: **I was unable to open a single source page.** This environment's network policy blocked WebFetch and curl for all external hosts (DNS refusal; `403` on CONNECT through the agent proxy), so every date and figure below is confirmed only by web-search results and syndicated summaries, not by reading the publisher's page. The brief asked me to verify publication dates on the source page itself, and I could not. Dates should be re-checked before publishing.

- **The 48-hour freshness anchor is weaker than ideal.** The CNBC "race to deploy" piece carries an October 15, 2026 URL date, which is roughly 48 hours before this draft — at the edge of the window, not comfortably inside it. I found no qualifying October 16–17 development on this specific topic. I did not pad the article with older news, but the anchor is a two-day-old story rather than a same-day one.
- **Lightcast figures conflict across sources.** CNBC (via secondary coverage) is cited for fewer than 200 postings in 2023 rising to 7,300+ in Jan–Sep 2026. Lightcast's own blog reportedly gives a different baseline — roughly 200 in 2024, ~1,200 in 2025, 5,200+ in the first seven months of 2026. I could not open either page to reconcile them. The direction of travel is consistent; the exact figures are not. The $195,456 median salary and the per-company posting counts (Deloitte 872, Accenture 688, Google 499, KPMG 447) come from secondary summaries of CNBC and Lightcast, unverified at source.
- **"Sign of a weak product" is a paraphrase, not a quote.** Search results indicate this is Newcomer's characterization of Jesse Zhang's position rather than his verbatim words. I avoided quoting it as his phrasing, and I could not open Newcomer or PYMNTS to check.
- **Decagon's $100M ARR is a company-reported figure** with no disclosed retention or churn data, per critical commentary. Unaudited.
- **OpenAI's deployment business figure ($4B+) was omitted from the draft deliberately** — sources disagreed on whether it describes investment or valuation, so I left it out rather than state it ambiguously.
- **Anthropic's 10,000 engineers / $100M is a stated 2027 target, not a headcount achieved.** First certifications are reportedly expected in early 2027. Anthropic's own naming is "Frontier Deployed Engineers"; much press coverage says "forward deployed."
- **The CIO.com article's publication date and author are unconfirmed.** I could not open it; I know its headline and general argument from search results only. Its characterization of CIO sentiment is one outlet's reporting, not survey data.
- **Mixpanel Agent Intelligence (October 1, 2026) is described from the company's press release and reprints.** No independent testing of its claims exists in what I found; it is in early access.
- **The hours-per-deployment slope test is my own framework, not a sourced benchmark.** This is flagged in the body as well. No public data on healthy ratios was found.
- **No image license could be confirmed** — see the Hero image section. All image candidates are unverified.
