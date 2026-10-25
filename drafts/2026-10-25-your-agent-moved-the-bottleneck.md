# Design

**Note on freshness:** The anchor story (Fujitsu/MISUMI, October 23) is within 48 hours. The Kognitos launch (October 21) and the review-bottleneck research are older supporting material, used deliberately as context rather than presented as new. This is flagged again in the unverified-claims section.

**Format:** case-study (rotating away from the last three entries: spec-brief, dependency-brief, metrics-brief)

**Subtitle:** Two October agent deployments both end with a human clicking approve. Nobody sized that step.

**Target reader:** A B2B SaaS or internal-tools PM at a 50–200 person company who is shipping an agent feature whose output a human must approve before it takes effect — and who wrote "human review" in the spec without a headcount or a throughput number next to it.

**Key takeaway:** Once an agent makes generation cheap, your product's throughput ceiling is set by review capacity, not model quality — so the approval step needs a spec, metrics and a backpressure rule, the same as the generation step.

**Section outline:**
1. Nine agents, tens of thousands of products, one human clicking approve — the Fujitsu/MISUMI deployment and the Kognitos launch, and the shape they share
2. The number that should bother you — Harvard's 718-firm finding, vendor benchmarks, the approval-queue paper
3. This is a queue, and queues have math — arrival rate vs. service rate; why "10x faster agent" doesn't show up in outcomes
4. The gate is usually load-bearing — why not to remove the human step (accuracy, liability)
5. Four things to specify before you ship — review fraction, reviewer UI, review duration, backpressure
6. What this evidence doesn't tell us — limits of the coding-agent analogy, self-reported vendor figures
7. Practical takeaway — four concrete actions, plus redoing the business case

## Headline options

1. **Agents Wrote 30% More Code. Shipped Work Didn't Budge.** — *(specific surprising number)* — **RECOMMENDED**: it is the article's load-bearing finding, the piece opens on it and pays it off with the source, and the gap between input and output is exactly the argument.
2. **Your Agent's Bottleneck Isn't the Model. It's Your Reviewer.** — *(contrarian claim challenging a common PM belief)*
3. **Can You Name Who Approves Your Agent's Output Today?** — *(sharp question the reader can't answer confidently)*

# Draft

## Nine agents, tens of thousands of products, one human clicking approve

On October 23, Fujitsu said it had put a multi-agent system into production for [MISUMI Group's product information management](https://www.tradingview.com/news/reuters.com,2026-10-23:newsml_JCN111056:0-fujitsu-implements-multi-ai-agent-infrastructure-to-enhance-product-information-management-for-misumi-group/) — the catalog work behind an e-commerce site carrying tens of thousands of products.

The agents generate series names, suggest categories, extract specifications, and check for restricted characters. [Trade coverage puts the count at nine](https://itbusinesstoday.com/tech/business-analytics/fujitsu-launches-multi-ai-agent-for-misumis-e-commerce-site/).

The platform took [about two and a half months to build](https://www.jcnnewswire.com/pressrelease/111056/3/Fujitsu-implements-multi-AI-agent-infrastructure-to-enhance-product-information-management-for-MISUM). The last step in the workflow is a human confirming and approving what came out.

Two days earlier, Kognitos launched ["AI Employees" for finance and banking](https://www.globenewswire.com/news-release/2026/10/21/3385463/0/en/kognitos-launches-ai-employees-and-expands-context-graphs-for-finance-and-banking.html): 61 role-based agents backed by 515 standard operating procedures. The agents run on a deterministic engine and, per the company, never add a step that isn't in an approved SOP. The agent that drafts new SOPs, Quill, publishes nothing until a person signs off.

Different vendors, different industries, identical shape at the end. Generation is automated. Approval is not.

If you are shipping an agent feature this quarter, that approval step is almost certainly in your design too. The question is whether you specified it, or just assumed it.

## The number that should bother you

A Harvard working paper by Fiona Chen and James Stratton looked at 718 firms adopting AI coding agents. Engineers wrote roughly [30% more code. Review took 49% longer. Finished work did not measurably rise](https://complexdiscovery.com/harvard-researchers-find-ai-coding-agents-shifted-the-bottleneck-to-code-review/).

More went in. The same amount came out. The difference piled up in review.

Vendor benchmarks point the same way, with bigger numbers. Opsera's 2026 benchmark reported AI-generated pull requests waiting 4.6x longer in review; LinearB put pickup time for agentic PRs at 5.3x. Those figures come from vendors with a product to sell, and the [write-ups](https://blog.codacy.com/ai-breaking-code-review-how-engineering-teams-survive-pr-bottleneck) relay them secondhand — but the direction is consistent across independent sources.

There's even a formal treatment of it. An [arXiv paper on approval queues](https://arxiv.org/html/2603.13870) argues that once generation is cheap, human approval becomes the binding constraint, and that review is a capacity decision as much as an accuracy one.

That last phrase is the one to keep.

## This is a queue, and queues have math

Here is the part that gets missed in planning. An approval gate isn't a checkbox in a flow diagram. It's a queue with an arrival rate and a service rate.

Your agent sets the arrival rate. Your reviewers set the service rate. If arrivals exceed service, the queue grows without bound, and no amount of model improvement fixes it.

This is why "the agent is 10x faster" so often fails to show up in any metric a CFO cares about. You raised arrivals 10x and left service flat.

And arrival rates are still climbing. Agent harnesses that can run [a single task for more than 24 hours](https://aiagentstore.ai/ai-agent-news/this-week) produce far more reviewable output per invocation than a prompt-and-response tool did.

> If generation is cheap and approval is not, then approval capacity — not model quality — is your product's throughput ceiling.

## The gate is usually load-bearing

To be clear: I am not arguing you should remove the human step. In both October examples, the gate is doing real work.

MISUMI's catalog feeds purchasing decisions for industrial parts. A wrong specification isn't an embarrassing typo, it's a returned shipment. Fujitsu's own description frames the human confirmation step as what keeps accuracy and consistency across the catalog.

In finance, it's liability. Someone has to be accountable for a reconciliation entry, and "the agent did it" has not yet been tested as a defense anywhere I'd want to rely on.

So the gate stays. The problem is that it usually arrives in the spec as one word — "approval" — while the generation side gets a model choice, an eval suite, a latency budget and a cost ceiling.

## Four things to specify before you ship

**What fraction actually gets reviewed.** "All of it" is a decision with a headcount attached. If you can't staff it, you'll get sampling by accident instead of by design — and accidental sampling means the fastest-clicking reviewer sets your quality bar. Decide the sampling rate, write it down, and tie it to risk tier rather than to whoever is on shift.

**What the reviewer sees.** A reviewer approving catalog copy needs the old value, the new value, and the reason the agent changed it. Reviewers given only the output will approve almost everything, because rejecting requires work they have no basis for. This is a UI problem and it belongs to you.

**How long a review takes.** Measure it. If a reviewer needs 90 seconds per item and your agent emits 4,000 items a day, you need about 100 reviewer-hours a day. That arithmetic should appear in the PRD, not in a postmortem.

**What happens when the queue backs up.** Does output expire? Auto-approve below a confidence threshold? Page someone? Silently grow? Pick one deliberately, because the default is the last one.

## What this evidence doesn't tell us

Be careful with the analogy. The hard numbers above are about coding agents and pull requests, which is a well-instrumented domain with a culture of review. Catalog enrichment and invoice processing are not the same thing, and I found no comparable study of approval queues for non-coding enterprise agent output.

The two October launches are also vendor announcements. The agent counts, SOP counts and build times are self-reported, and neither company has published throughput or reviewer-load figures. What they show is that the architecture is converging, not that it's working.

The Harvard paper is a job-market working paper, not peer-reviewed. Treat the 30% and 49% as a strong signal, not a settled fact.

## Practical takeaway

If you own an agent feature with a human approval step, do these four things this week.

1. **Find your service rate.** Time ten real reviews. Multiply by expected daily volume. If the result exceeds the hours you actually have, you have a capacity problem today, not later.

2. **Instrument the queue, not just the agent.** Add three metrics: items awaiting approval, median time in queue, and approval rate. An approval rate near 100% usually means reviewers lack the context to say no, not that the agent is excellent.

3. **Give reviewers a diff and a reason.** Before/after plus the agent's justification. This single change does more for review throughput than most model upgrades.

4. **Write the backpressure rule into the spec.** State explicitly what the system does when the queue exceeds some depth. Make it a product decision with a named owner.

Then the harder conversation: if your business case assumed the agent's generation speed was the gain, redo the model with review capacity as the constraint. The honest number is usually much smaller, and much easier to defend.

The teams that get value from agents over the next year won't be the ones with the best models. They'll be the ones who noticed that they'd moved the bottleneck and then went and designed the new one.

**Word count:** 1,149 words (prose only, excluding link URLs and the Design/Hero/Metadata sections). Within the 1000–1400 target.

# Hero image

**Important caveat up front:** this session's network policy blocked all direct page fetches (every host returned a DNS failure, and direct HTTPS was refused by the proxy with a 403 on CONNECT). I could search the web but could **not** load the image pages themselves. So the photographer names and license labels below come from search-result metadata, not from a page I was able to open and read. I have deliberately **not** constructed direct CDN image URLs, because guessing an Unsplash or Pexels file hash would be inventing a link. Verify each page in a browser before publishing — it is a 30-second check.

## Option 1 (primary)

- **Source page:** https://unsplash.com/photos/stacks-of-paper-documents-and-file-folders-snNHKZ-mGfE
- **Subject:** Stacks of paper documents and file folders — reads as an approval backlog without using a robot cliché.
- **Creator:** Wesley Tingey
- **License (per search metadata):** Unsplash License — free for commercial use, no attribution required
- **Direct image URL:** not recorded. Use the page's Download button to get it.
- **Attribution line (optional under this license, but good practice):**
  `Photo by Wesley Tingey on Unsplash`

## Option 2 (backup)

- **Source page:** https://www.pexels.com/photo/piles-of-documents-in-paper-office-4277209/
- **Subject:** Piles of documents in a dimly lit paper office — messier, more editorial in feel.
- **Creator:** Chengxin Zhao
- **License (per search metadata):** Pexels License — marked "Free to use"
- **Direct image URL:** not recorded. Use the page's Download button.
- **Attribution line (optional under this license):**
  `Photo by Chengxin Zhao on Pexels`

**Watch out for Unsplash+.** Search results surfaced visually similar paperwork photos that are licensed under the **Unsplash+ License**, which is paid and not free for commercial use. One example flagged in results was "a stack of papers sitting on top of a table" by A F. Check for the Unsplash+ badge on the photo page before downloading.

## Fallback description (if neither link verifies)

A wide, desaturated editorial shot of an in-tray or desk corner stacked high with uniform paper documents, shot slightly from above with shallow depth of field so the top sheet is sharp and the stack recedes into blur. Natural window light from the left, muted office palette — grey, white, pale wood. No people's faces, no screens, no robots or android hands. The visual argument is volume arriving faster than one pair of hands can process it, which is the article's thesis; a tall stack beside a single empty chair would work equally well. Avoid anything with visible brand names, legible document text, or stock-photo "businessperson looking stressed" framing.

# Metadata

**Medium tags:** Product Management, AI Agents, Artificial Intelligence, Product Strategy, Workflow Automation

## Unverified claims

Listed honestly. The network restriction described in the Hero image section applies throughout: **I could run web searches but could not open a single source page directly**, so every item below was verified against search-result content rather than against the primary document.

- **The 48-hour window is only partly satisfied.** The anchor story — Fujitsu's multi-agent deployment for MISUMI Group — is dated **October 23, 2026**, which is inside 48 hours of today (October 25). The Kognitos "AI Employees" launch is **October 21** and the review-bottleneck research is older. I used them as supporting context and labelled them as such in the text rather than padding the piece with stale news presented as new. I also checked two other stories from this window — US banks blocking third-party AI agents, and the 1Password for Agents launch — and excluded both: the reporting broke October 18–22, outside the window, and both overlap topics already covered in this series.
- **"Nine agents" (Fujitsu/MISUMI):** reported by trade outlets (IT Business Today and others). Search results explicitly noted that no official Fujitsu or MISUMI statement confirming the count of nine was found. Treat as trade-press reporting, not a vendor-confirmed figure.
- **Build time of ~2.5 months, "tens of thousands of products," and the human confirmation step:** all from Fujitsu's own press release as distributed via JCN Newswire / ACN Newswire / TradingView. Vendor-stated, not independently verified.
- **Kognitos figures (61 roles, 515 SOPs, Quill, deterministic engine, "never adds a step not in an approved SOP"):** all from the company's own GlobeNewswire release. Self-reported. No independent verification, and no customer-reported throughput data exists yet.
- **Harvard working paper (Chen & Stratton, 718 firms, ~30% more code, 49% longer review, no measurable rise in finished work):** accessed only via a secondary summary on ComplexDiscovery, not the paper itself. It is described as a job-market working paper with no indication of completed peer review. The specific numbers should be treated as a strong signal, not settled fact — which the article says explicitly.
- **Opsera 4.6x and LinearB 5.3x figures:** vendor benchmarks relayed secondhand through a third-party blog post. Search results noted these numbers are cited inconsistently across sources. I attributed them to vendors and hedged them in the text; I would not put either number in a headline.
- **arXiv paper on approval queues (2603.13870):** I could not open it. The characterisation of its argument ("once generation is cheap, human approval becomes the binding constraint; review is a capacity decision as much as an accuracy decision") comes from a search-result summary. The paraphrase may not match the paper's own framing, and I did not verify the paper's status or venue.
- **"Agent harnesses running a single task for more than 24 hours":** attributed in search results to Notion's rebuilt agent harness, sourced from an aggregator page (aiagentstore.ai), not from Notion. Weakest citation in the piece; it supports a secondary point only, and the article does not name the vendor.
- **Both hero image candidates are unverified.** Photographer names and license labels come from search-result metadata only. Neither page was loaded; no direct image URL is given for either. Confirm the license badge — particularly that it is not Unsplash+ — before publishing.
- **Not a factual claim, but worth stating:** the queueing argument in "This is a queue, and queues have math" is my own reasoning applied to the cited evidence, and the 90-seconds/4,000-items arithmetic is an illustrative example, not measured data from any company named in the article.
