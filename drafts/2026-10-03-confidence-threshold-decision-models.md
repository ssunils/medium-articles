# Design

**Subtitle:** Four labs shipped models that return a probability instead of a sentence. Someone has to decide what probability is good enough — and that someone is you.

**Target reader:** A B2B SaaS PM at a 50–300 person company who already has an AI feature in production — support triage, ticket routing, content moderation, an agent that calls tools — and owns the quality bar on it.

**Key takeaway:** Decision models hand you a calibrated probability on every call, which turns "which model should we use" into a sharper and more uncomfortable question: what confidence threshold are you shipping, and what happens to everything below it?

## Headlines

1. **What Confidence Threshold Did You Ship? Most PMs Can't Say** — *RECOMMENDED.* It names a decision the reader already owns without realising it, and the article's spine is exactly how to set and staff that number. Sharp-question hook, and the piece pays it off rather than teasing it.
2. **Your Next AI Feature Shouldn't Write a Single Word** — contrarian hook, challenges the assumption that an AI feature means generated text.
3. **Swap "Yes" and "No" and Half the Answers Change** — surprising-number hook, built on the label-sensitivity result in the benchmarking paper.

## Section outline

- Two releases, one day, no text
- What a decision model actually returns
- The number you now own
- The part nobody demos: below the line
- The cheap baseline you should make it beat
- Two reasons to stay suspicious
- Practical takeaway
- Where I'd be careful

# Draft

# What Confidence Threshold Did You Ship? Most PMs Can't Say

On October 1, two more companies shipped AI models that cannot write a sentence. That isn't a limitation they're working on. It's the product.

Cloudflare released [Clef and Clef-flash](https://blog.cloudflare.com/clef-decision-models/), its first in-house trained models: open-weight "decision models" that take some state plus a set of typed questions and return [calibrated probabilities over predefined answers instead of text](https://www.marktechpost.com/2026/10/01/cloudflare-releases-clef-and-clef-flash/), under Apache 2.0. The same day, AWS Strands Labs released [Strands Decider 2B](https://www.marktechpost.com/2026/10/01/aws-strands-labs-releases-strands-decider-2b/), a 1.9-billion-parameter model that picks from fixed answers in a median of about 115 milliseconds on a single RTX 3090 and runs on a laptop.

Both follow TypeSafe AI's [Jev](https://www.infoq.com/news/2026/10/typesafe-ai-jev-released/), which started the category in mid-September, and OpenAI's Decisions API, [announced at DevDay on September 29](https://trilogyai.substack.com/p/jev-open-decision-models) and still in limited preview. Four entrants in under three weeks is not one startup's framing catching on. It's a category.

## What a decision model actually returns

The mechanics matter more than the benchmarks here, so: you define the questions and the complete set of allowed answers *before* the call. The model reads unstructured state — a ticket, a page, an agent trace — and returns a choice plus a probability. [It never generates a string](https://www.width.ai/post/what-is-jev-ai-typesafe), so it cannot invent an enum value you don't handle, and there's nothing to parse.

Cloudflare's own pitch is "smart if-statements" for software: routing, classification, scoring, guardrails, agent monitoring. The speed is the reason anyone cares — Clef-flash lands [around 39 milliseconds at the median](https://ai-tldr.dev/models/clef/), fast enough to sit in front of a tool call rather than beside it. Pricing runs [$0.24 per million input tokens for Clef and $0.09 for Clef-flash, with output not billed at all](https://www.developersdigest.tech/blog/cloudflare-clef-decision-models-2026).

So if you've been paying a general-purpose model to answer "is this ticket about billing" in three paragraphs you then regex, that's the arbitrage. Fine. That part is an engineering win and you don't need a PM for it.

## The number you now own

Here's the part that is yours.

Every call comes back with a probability. Which means somebody has to decide the cutoff: above this number we act automatically, below it we escalate. Cloudflare describes exactly this pattern — [high-confidence decisions go straight through, low-confidence ones escalate to an LLM](https://byteiota.com/cloudflare-clef-decision-models-agents/).

That cutoff is not a tuning parameter. It sets your automation rate, your error rate, your support load, and what a customer experiences at the exact moment your product is unsure about them. For three years, PMs have shipped AI features where that tradeoff was buried inside a prompt and a vibe check. The API now hands it to you as a number you have to write down.

> The threshold isn't a setting your engineers pick. It's the product decision, and it quietly determines how much of your product is the escalation path.

## The part nobody demos

Launch posts show the confident cases. The research is more useful about the rest.

A recent evaluation of these models on agent security decisions found that [under strict limits on missed attacks, the policies allow few inputs automatically](https://arxiv.org/abs/2609.33401) — and that choosing separate allow and block thresholds increases automation mainly by blocking more inputs. Read that twice. If your tolerance for bad outcomes is low, most traffic does not clear the bar, and the easy way to raise your automation number is to start refusing more customers.

A benchmarking paper on automated decision gates puts a figure on the leakage: a held-out threshold tuned for five percent in-scope risk [still let Jev accept 0.310 of out-of-scope requests](https://arxiv.org/abs/2610.00346).

The practical consequence is a planning one. If half your volume lands below the line, the below-the-line experience isn't a fallback you bolt on in week eleven — it's the majority of your product, and it needs the same design and staffing attention as the happy path.

## The cheap baseline you should make it beat

Before anyone buys anything, there's a result worth putting in front of your team. In that same benchmarking work, [with the task's own labels, small trained classifiers were the most accurate on intents](https://arxiv.org/abs/2610.00346) and not significantly different from the best decision models on workflows.

And on cost: an intent-trained first stage that escalates to Jev matched Jev's accuracy at 0.43 of its cost.

If you have labeled data — and if you've been running this feature in production, you do, in your resolution logs — a small classifier you train yourself is the baseline to beat, not the legacy approach you're replacing. Decision models earn their keep where you *don't* have labels, or where you need many different questions answered about the same state without training a model per question.

## Two reasons to stay suspicious

First, calibration can look good on average and still be wrong where it counts. The security evaluation found that [strong average calibration can hide systematic failures on particular attack groups, including attacks the models confidently classify as safe](https://arxiv.org/abs/2609.33401), and that policies meeting error limits during validation exceeded them on unseen inputs. A second model checking the first one helped some, but repeated the first model's high-confidence mistakes.

Second, the wording of your options is now load-bearing. The benchmarking paper found that [swapping yes and no flips 50.5 answers per hundred for Jev](https://arxiv.org/abs/2610.00346). Your question text and answer labels are product copy with a measurable error rate attached, and nobody on your team currently owns them.

## Practical takeaway

Concrete things to do this week:

1. **Inventory by shape.** List your AI features and mark each one "decision" or "drafting." Anything that ends in a routing choice, a score, a yes/no, or a tool-call approval is a decision, and is a candidate.
2. **Write down today's implicit threshold.** For each decision feature, what confidence does it currently require, and what happens below it? If nobody can answer, that's the finding.
3. **Build a labeled set.** Two to five hundred rows from your own logs, labeled by someone who knows the domain. You need this for every option below.
4. **Run a three-way bake-off.** Your current LLM call, a small classifier trained on your labels, and a decision model. Score accuracy, calibration, cost per request, and p95 latency — all four, not just the first.
5. **Report coverage next to accuracy.** "94% accurate" is meaningless without "on the 23% of traffic that cleared the threshold." Make coverage a tracked metric.
6. **Freeze and version your option wording.** Treat the question and answer set like schema. Re-run the eval when it changes.

## Where I'd be careful

These models are days old, most published numbers come from the vendors, and the independent evaluations that exist are mainly about security decisions rather than your use case. The open weights are genuinely useful — you can run Strands Decider on a laptop and test it against your own data this week, for free, which is the fastest way to find out if any of this helps you.

But I wouldn't put one in front of an irreversible action yet. Put it where a wrong answer costs a re-route, not a refund.

**Word count: 1,160 words** (draft body, headline through final line, counting visible prose with link URLs excluded — within the 1000–1400 target).

# Hero image

**I could not verify a real, usable image for this article.** This session's network policy blocks outbound page loads to every image host I tried — `unsplash.com`, `pexels.com` and `openverse.org` all returned egress denials, so I could not open a photo page to confirm the photographer's name or the license that specific photo carries. I'm not pasting a direct image URL or a license claim I couldn't load and read myself.

Web search *did* surface these two real Unsplash photo pages, which I am listing as **unverified candidates** rather than confirmed picks — the license and credit still need a one-click check in your browser:

- Candidate 1: `https://unsplash.com/photos/black-and-white-analog-gauge-8JSkpssuPxk` — a black-and-white analog gauge. Fits the threshold-dial idea, no robot clichés.
- Candidate 2: `https://unsplash.com/photos/0A7cA6PEjz4` — an orange-and-white analog gauge, warmer and more editorial.

**Two-minute check before you publish:** open either page, confirm the banner says *Unsplash License* (free for commercial use, no attribution required), and copy the photographer's name from the page. If you'd rather have a guaranteed-attribution-free source, Pexels search `gauge dial macro` carries the Pexels License; Openverse search `pressure gauge` filtered to CC0 gives public-domain options.

If you land on a CC BY image instead, the attribution line to paste under the image on Medium is:

`Photo by [CREATOR NAME] on [SOURCE], licensed under CC BY 4.0`

**Fallback cover image description (use this if you'd rather generate or commission one):** A tight, desaturated macro shot of a single analog dial — a pressure gauge or VU meter — with the needle resting in the middle of the sweep rather than pinned at either end. Shallow depth of field, the numbers on the face just legible, one warm accent against a cool grey-slate background. No robots, no androids, no glowing neural networks. The visual argument is a needle between two zones, because the whole article is about where you draw the line on a scale. Shoot or crop it wide at roughly 1500×750 for Medium's cover, with the dial sitting right of centre so a headline overlay has clean space on the left.

# Metadata

**Tags:** Product Management, Artificial Intelligence, AI Product Development, Machine Learning, Product Strategy

# Unverified claims

This session's network policy blocked outbound page loads on every domain I tried (`blog.cloudflare.com`, `developers.cloudflare.com`, `marktechpost.com`, `prnewswire.com`, `mixpanel.com`, `arxiv.org`, `huggingface.co`, `en.wikipedia.org`, and all three image hosts). **Everything below was triangulated across multiple independent search results rather than read on the primary source page**, which is a weaker standard than this column normally uses. Specifically:

- **Dates.** The October 1, 2026 release dates for Clef/Clef-flash and Strands Decider 2B are consistent across several independent write-ups and appear in the Cloudflare changelog slug (`2026-10-01-clef-workers-ai`) and the MarkTechPost URLs, but I could not open a source page to confirm a publication date directly. Same for Jev (mid-September) and the OpenAI Decisions API at DevDay (September 29).
- **OpenAI's Decisions API** is the thinnest-sourced claim in the piece: limited preview, built on GPT-6 Luna, roughly 150ms. It came from secondary commentary, not an OpenAI post I could read. Verify before publishing, or cut the clause.
- **Clef pricing and latency** ($0.24 / $0.09 per million input tokens, output unbilled; ~39ms median for Clef-flash, with one source reporting 38.8ms and ~209ms for Clef) come from third-party summaries of Cloudflare's own figures. Vendor-published performance numbers, unaudited.
- **Benchmark scores** I deliberately left out of the draft — Decision Index 61.2 / 57.9 / 57.1 and a BANKING77 macro-F1 of 94.20 — because they trace to a vendor leaderboard and a community project I couldn't inspect.
- **The two arXiv papers** (2609.33401 on agent security decisions, 2610.00346 on automated decision gates) are quoted from search-surfaced abstract text. The specific figures — 0.310 of out-of-scope requests accepted, 50.5 answers per hundred flipped, 0.43 of cost — are quoted as they appeared and I could not open the papers to check context, methodology, or whether these are headline or cherry-picked results. The 2610.00346 identifier implies early October; I could not confirm its exact submission date, so I describe it in the draft without a date.
- **The "23%" figure** in takeaway #5 is illustrative, written as an example of how to report coverage. It is not a measured number from any source and should not be read as one.
- **Hero image:** license unconfirmed for both candidate images, for the reason given above.

One note on freshness, honestly: the 48-hour peg (two decision-model releases on October 1) is solid and multiply sourced. The supporting research is two to three weeks old and is presented in the draft as context rather than news.
