# Design

**Subtitle:** Santander's headline savings number is a result. The thing worth copying is the apparatus that produced it.

**Target reader:** A B2B SaaS product manager at a 50–500 person company who owns an AI feature running on a frontier model API, and who has been asked by finance or engineering to cut inference cost without hurting quality.

**Key takeaway:** Per-task model switching only pays off if you already own a task-level evaluation set, because without one you are trading a known cost for an unmeasured quality risk.

**Section outline:**
1. Open on the €5 → €0.03 figure and why it is the least useful part of the announcement
2. What Santander actually built: the Model Arena
3. Why the cost-cut proposal stalls in most product orgs
4. The unit that matters is the task, not the product
5. The tradeoff you are actually choosing (one model vs. routing plus eval upkeep)
6. How to build a small arena
7. Practical takeaway
8. Unverified claims

## Headline options

1. **€5 to €0.03: Santander's AI Savings Came From Something Else** — hook type: specific surprising number. (**RECOMMENDED** — the figure is concrete and verifiable, and the article pays off the "something else" by naming the Model Arena rather than withholding it.)
2. **Switching to a Cheaper Model Is the Easy Half** — hook type: contrarian claim against the common belief that model choice is the lever.
3. **Could You Prove a Cheaper Model Didn't Hurt Your Product?** — hook type: sharp question most PMs cannot answer confidently.

# Draft

Santander says it has cut the cost of serving one AI interaction from €5 to about €0.03.

That is roughly a 99% reduction, and it is the number that will get screenshotted this week. It is also the least useful part of the announcement.

The figure comes from a release [reported Monday](https://www.pymnts.com/news/banking/2026/santander-turns-to-nvidia-to-build-new-ai-banking-capabilities/) alongside news that the bank is working with NVIDIA on capabilities for evaluating AI models and agents for banking. The same report is careful about scope: the savings came from "selected experiments," not from the bank's whole production estate. Hold onto that caveat, because it is the tell.

## The part worth copying

Further down the same release is a detail that got less attention. Santander's AI lab built what it calls a "Model Arena" to [evaluate open-weight models against banking tasks and determine which model is right for each workload](https://www.pymnts.com/news/banking/2026/santander-turns-to-nvidia-to-build-new-ai-banking-capabilities/). It is also specialising models using [NVIDIA's NeMo Customizer](https://www.nvidia.com/en-us/ai-data-science/products/nemo/get-started/), a microservice for fine-tuning models on proprietary domain data.

The arena is the asset. The cheap model is just what fell out of it.

Nobody at Santander woke up and decided a smaller model would be fine. They built the thing that let them find out which smaller model was safe for which specific job, and the cost curve followed. Reverse that order and you get a budget line that looks better and a product nobody can vouch for.

## Why your version of this proposal stalls

You have probably been in the meeting. Inference spend is up, finance wants to know why, and someone sensible suggests routing the simple requests to a smaller model. Then someone asks the obvious question: will quality drop?

And the room goes quiet, because at the product level that question has no answer.

"Will quality drop" is unanswerable when the subject is your whole product. It becomes answerable the moment the subject is a named task with written-down cases. Classification, extraction, summarising a support thread, drafting a first-pass reply — each of those has a right answer you can check, and a failure mode you can describe.

> A model is not good or bad. It is good or bad at a named task, measured against cases you wrote down before you went shopping.

Without that, the proposal resolves one of two ways. Either it dies in the meeting, or it ships on vibes and you find out from a customer.

## Note the unit Santander used

The release says the bank has been moving "progressively" from large general-purpose models toward smaller, specialised models designed for specific banking tasks. Tasks, plural. Not one swap.

There is a second number in there that I find more interesting than the headline one. In an experimental customer-service use case, Santander reported it improved conversation quality while [lowering costs by more than 50%](https://www.pymnts.com/news/banking/2026/santander-turns-to-nvidia-to-build-new-ai-banking-capabilities/) by deploying a more efficient model.

Quality went up and cost went down. That is not the tradeoff story we usually tell about cheaper models, and it is worth being slightly suspicious of a single vendor-adjacent data point. But it is plausible for a narrow task: a model tuned on your domain can beat a larger generalist on the thing it was tuned for. The point is that you cannot see an outcome like that at all unless you are measuring per task. A blended quality score would have hidden it.

## The tradeoff you are actually choosing

It is not "expensive model versus cheap model." It is this:

**Option A — one model everywhere.** Simple, predictable, one vendor relationship, one set of behaviours to document. You overpay on the high-volume mechanical work, which is often most of your calls.

**Option B — per-task selection.** A smaller bill. You also now own a routing layer, a regression suite per routed task, and a standing obligation to re-run that suite every time any model in the mix changes version. That last cost is permanent and it is not small.

Santander can carry Option B. It has a dedicated AI lab, it [publishes some of its AI work as open source](https://github.com/SantanderAI), and it has pushed AI tooling out to [185,000 employees](https://www.fintechfutures.com/ai-in-fintech/santander-to-extend-ai-capabilities-to-185-000-employees-worldwide). A forty-person product org with one ML-adjacent engineer probably cannot carry it across ten tasks.

So the usable rule is narrower than the headline suggests: route only where you have an eval set, and build eval sets only for the two or three tasks that actually move your bill.

## Build the arena small

You do not need a lab. You need a golden set per task, which is less work than it sounds.

Capture real request and response pairs from your own production traffic rather than starting from a public benchmark. Public benchmarks have a known problem here — practitioners argue they get [saturated, gameable, or simply irrelevant](https://thenewstack.io/enterprise-ai-benchmarks-are-broken/) to the specific workflows a company runs. Procurement-focused guidance makes the same point from the buyer's side: [no vendor-reported score substitutes](https://www.automationanywhere.com/company/blog/ai-agent-benchmarks) for evaluation on tasks that represent your actual deployment. Worth noting that several of the "neutral" enterprise benchmarks now in circulation are themselves published by vendors.

Include the ugly cases, not just the clean ones. Ambiguous prompts. Empty result sets. Permission denials. At least one request that should fail. A set made only of easy cases will pass every model you try, which makes it worse than no set at all, because it manufactures confidence.

Then gate on it. Engineering guidance on golden datasets suggests [running the set automatically in CI](https://langfuse.com/resources/engineering/golden-dataset-evaluation) so any change that touches a prompt or a model fails loudly rather than quietly. That is vendor material and reads like it, but the mechanism is right: a routing change is a code change and deserves the same gate.

Tooling for the measurement side is arriving too, if thinly. Mixpanel shipped [Agent Intelligence](https://www.prnewswire.com/news-releases/mixpanel-introduces-agent-intelligence-helping-product-teams-build-and-measure-more-effective-ai-agents-302895602.html) in early access on 1 October, aimed at stitching scattered agent events back into whole conversations and tying them to resolution and business outcomes. I have not used it and there are no independent reviews yet. Treat the category as early.

## Practical takeaway

Concrete things to do, roughly in order:

1. **Name your three highest-volume AI tasks this week.** Not features — tasks, at the granularity of one model call with a checkable output.
2. **Pull 100–300 real request/response pairs per task** out of production logs. This is the whole project. Everything else is cheap once you have it.
3. **Write down the failure cases** alongside the happy path, including the ones where the correct behaviour is to refuse or return nothing.
4. **Put the set behind a CI gate** that fails the build on regression, before you change a single model.
5. **Route exactly one task first** — the highest-volume, most bounded one. Report its per-task quality number and its per-task cost, never a blended average.
6. **Re-run the suite on every model version change,** including upgrades to the model you already trust. Silent regressions on a minor version bump are the common failure here.
7. **If a task has no eval set, it does not get routed.** Hold that line, including when the savings estimate is tempting.

Santander's 99% figure is a result, and results do not transfer. The arena is a method, and methods do. If you copy one thing from Monday's announcement, copy the order of operations: measurement first, then the cheaper model, then the number you get to show finance.

**Word count: 1,214**

# Hero image

WebFetch and direct HTTP are both blocked in the environment this draft was produced in, so I could not open any image page to confirm it with my own eyes. Everything below was surfaced and described by web search against the image hosts, including the photographer names and photo metadata. Verify the page before publishing — it takes one click.

**Primary option**
- Title: *Analog Pressure Gauges in Close-up Shot* — three industrial pressure gauges on pipelines, shot indoors
- Source page: https://www.pexels.com/photo/analog-pressure-gauges-in-close-up-shot-5532838/
- Photographer/creator: cottonbro studio
- License: [Pexels License](https://www.pexels.com/license/) — free for personal and commercial use, no attribution required; you may not sell unaltered copies or redistribute the file on other stock platforms
- Attribution line: not required. If you want to credit anyway, Pexels suggests this format: `Photo by cottonbro studio via Pexels`
- Why it fits: three gauges side by side reads as a comparison rather than as AI imagery, and it avoids the robot cliché entirely
- Direct image URL: not verified. Pexels serves files from `images.pexels.com` under a predictable pattern, but I will not paste a constructed URL as if I had confirmed it. Download the file from the page above instead.

**Backup option**
- Title: *Cockpit dashboard with control console and gauges* — close-up of an aircraft control panel with levers and instruments
- Source page: https://www.pexels.com/photo/cockpit-dashboard-with-control-console-and-gauges-3850907/
- Photographer/creator: Ricky Esquivel
- License: [Pexels License](https://www.pexels.com/license/) — same terms as above, no attribution required
- Attribution line: not required. Optional form: `Photo by Ricky Esquivel via Pexels`
- Metadata per search result: Sony ILCE-7M3, 85mm, f/1.4, uploaded March 2020

**Fallback description, if neither page checks out**

A tight, shallow-depth-of-field photograph of three or four identical analogue dials mounted side by side on an industrial panel, each needle resting at a visibly different position. Cool desaturated palette — steel, slate, a little muted teal — with one dial in sharp focus and the rest falling off softly, shot horizontally so it crops cleanly to Medium's wide cover ratio. The image should read as *instruments being compared*, not as technology in the abstract. Avoid robots, androids, humanoid faces, glowing blue brains, circuit-board motifs, and anything with legible branding on it.

# Metadata

**Medium tags:** Product Management, Artificial Intelligence, AI Evaluation, Machine Learning, Product Strategy

## Unverified claims

Being specific here, because the research environment was degraded in a way that matters.

**Environment limitation.** WebFetch failed with DNS errors on every domain attempted, and direct HTTPS via the command line was refused by the egress proxy for every non-allowlisted host. I could therefore not open a single source page directly. Every claim below rests on what the web search tool read and reported back, not on my own read of the page. That is weaker verification than this process is supposed to use, and it applies to all sources in the draft.

**Could not confirm against a primary source:**

- **The Santander figures** (€5 → €0.03 per interaction; >50% cost reduction with improved conversation quality in an experimental customer-service case; the "Model Arena"; use of NeMo Customizer). All of these trace to a single outlet's report of a Santander press release, dated Monday 19 October 2026. I could not locate the press release itself on santander.com or an NVIDIA newsroom post, and I found no independent coverage. The cost figures are explicitly described in that report as coming from "selected experiments," not production-wide deployment — the draft says so, but it bears repeating.
- **The publication date of that report.** The search tool described it as published today and the text references "Monday (Oct. 19)," which matches. I could not confirm a timestamp on the page.
- **Santander's 185,000-employee AI rollout.** Reported by FinTech Futures and referenced in several secondary roundups, originally announced around June 2026. Not confirmed on a primary Santander page.
- **The github.com/SantanderAI organisation** as Santander's official open-source AI presence. Surfaced by search and consistent with separate coverage of the bank publishing AI projects under an open-source licence, but I could not open the org page to confirm it is official rather than a lookalike.
- **Mixpanel Agent Intelligence**, launched 1 October 2026 in early access. Sourced from the company's own press release via search. All product claims are Mixpanel's own; no independent reviews found. The draft states this.
- **The New Stack, Automation Anywhere, and Langfuse links.** Used as practitioner or vendor opinion, which is how the draft frames them. None is an authoritative source and I did not open any of them. The Automation Anywhere post promotes that company's own benchmark suite; the Langfuse piece promotes its own tooling.

**Deliberately left out as unverifiable.** Several widely repeated figures turned up during research and are not in the draft because I could not get within one hop of a primary source: a claimed ~37% gap between benchmark scores and real-world performance attributed to Kili Technology; RouteLLM's reported cost reduction and quality-retention percentages; a Stanford "Minions" study's 87% / 97.9% quality-retention split; and vendor claims that routing layers cut bills by 40–85%. Also excluded: specific current model prices, which move fast enough that a figure from a July 2026 comparison is not worth printing.

**Image licensing.** Neither Pexels page was opened. Photographer names, titles, and the camera metadata on the backup image come from search results. The Pexels License terms quoted are from search results reading pexels.com/license and the Pexels help centre. No direct image URL is given for either option, because I would have had to construct it. Confirm both the photo and the licence on the page before publishing.
