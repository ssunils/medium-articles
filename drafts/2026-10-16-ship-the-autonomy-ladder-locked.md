# Design

**Subtitle:** A building-AI launch this week shipped three autonomy modes and switched the top one off on purpose. That's a product pattern worth copying.

**Target reader:** A B2B PM at a 50–500 person company shipping an AI agent into an operational workflow where a wrong action costs money, downtime, or safety — and who is right now deciding how much the agent is allowed to *do* in v1.

**Key takeaway:** Ship autonomy as explicit, switchable levels, default to advisory, and make each escalation an evidence-gated decision the customer makes — not a capability you enable because it worked in a demo.

**Section outline:**
1. A launch that shipped a switch it didn't throw
2. Why "we built it but it's off" is a product decision
3. The ladder is the product
4. What earns the next rung
5. The counter-pressure is real
6. Practical takeaway

**Headline options:**

1. **Honeywell Shipped Three Autonomy Modes and Locked the Third** — *(hook: specific, surprising result)*
2. **Your AI Agent's First Version Should Not Be Allowed to Act** — *(hook: contrarian claim)*
3. **Could You Defend Switching Your Agent's Autonomy On Today?** — *(hook: sharp question the reader can't answer confidently)*

**RECOMMENDED: Option 1.** It carries the surprising specific — a shipped-but-disabled mode — and the article delivers exactly that teardown plus the escalation playbook, so the headline doesn't overpromise.

---

# Draft

Honeywell shipped an AI platform on Wednesday with three autonomy modes and left the third one switched off.

Not "coming soon." Off, deliberately, with a timeline measured in years.

Its CTO, Suresh Venkatarayalu, [told Fortune](https://fortune.com/2026/10/14/honeywell-technologies-brain-behind-the-bulding-forge-cognition-dell-nvidia/): "We have not opened up an autonomy right now." On how long the advisory posture lasts: "Maybe we will start running in this mode for probably next two to three years." After that, he said, customers choose when to switch it on.

That is an unusual thing to say during your own launch. And if you are a PM deciding how much your agent gets to do in v1, it is the most useful thing that happened this week.

## A launch that shipped a switch it didn't throw

The product is Forge Cognition, [announced October 14](https://www.honeywell.com/us/en/news/press-releases/2026/10/honeywell-technologies-launches-forge-cognition-with-nvidia-and-dell-technologies-advancing-physical-ai-across-buildings-and-industrial-operations) as an agentic AI and simulation platform for buildings, campuses, and industrial sites, built with NVIDIA and Dell technology. Agents classify and verify building-management alarms so operators can prioritize the events that actually need attention.

The detail that matters is in the announcement's own description of how it runs: customers can operate it in manual, semi-autonomous, or autonomous modes, operators set the level of oversight, and they can override it at any time.

Three named modes. One of them inert at launch.

The pilot numbers are not bad, either. NVIDIA's operations and real estate team ran a 90-day trial at its Voyager campus, and Honeywell reports up to a 90% average reduction in unnecessary alerts, roughly 10% in identified energy and utility savings, and a weighted comfort score above 95%. These are vendor-reported figures from a single pilot, not independent benchmarks — treat them as directional.

So: a system good enough to cut nine out of ten nuisance alerts, and the company still won't let it act by itself.

## Why "we built it but it's off" is a product decision

The instinct is to read this as timidity, or as a roadmap gap dressed up in safety language. I don't think that's what it is.

Venkatarayalu described the thing as a "brain behind a building" that advises, while operators decide. That's a posture, and posture is a product choice with real consequences — it determines what you instrument, what you put in the UI, what your support team handles, and what your contract says.

Consider what the autonomous tier would actually require in a building. An agent that can act on its own has to be right about an alarm *and* right about the response *and* right about the second-order effects on comfort, energy, and equipment, in a physical environment where the rollback for "we cooled the wrong floor for six hours" is not a git revert.

Shipping that capability dark is cheaper than shipping it live and wrong once.

> Capability is not permission. Deciding which of the two you're shipping is the actual product work.

## The ladder is the product

Here's the part worth stealing, regardless of whether you sell building systems.

Most agent features I see ship with autonomy as an implicit property of the feature. The agent does what the agent does. If it acts, it acts. There's no named level, no switch, and no language in the product for "this agent advises" versus "this agent acts."

That's a mistake, because it collapses three separate things into one release decision:

- what the model is **capable** of
- what the product is **allowed** to do
- what a specific customer has **turned on**

Make those three separable and a lot of hard problems get easier. You can ship the capability to a design partner without exposing it to your whole base. You can let a sophisticated customer move faster than a conservative one without forking the product. You can roll back permission without rolling back code. And you can have an honest sales conversation, because "autonomous mode exists and you decide when to enable it" is a very different promise from "our agent is autonomous."

Honeywell made the escalation the customer's call on the customer's timeline. That's not hedging. That's putting the switch where the liability already lives.

## What earns the next rung

The weakness of a staged autonomy ladder is that the stages become decorative. Everyone ships "human in the loop" in v1 and then escalates whenever the demo looks good or a big deal demands it.

If you're going to build the ladder, define the gate before you need it. Concretely, write down — before launch — what evidence moves your agent from advising to acting:

**Agreement rate on real traffic.** Not eval-set accuracy. When your agent recommends and a human decides, how often does the human take the recommendation? That gap is the cheapest autonomy signal you will ever get, and advisory mode generates it for free. This is the part teams skip: they run advisory mode for months and never instrument the override.

**The cost of being wrong, by action type.** Autonomy is rarely all-or-nothing. Classifying an alarm as low priority and dispatching a technician are different bets. Rank your agent's actions by reversibility and let the cheap, reversible ones graduate first.

**A tested stop path.** Override "at any time" is a claim that needs a test, not a checkbox. Someone should have actually stopped the agent mid-action in staging.

**A named owner for the switch.** If nobody's name is on enabling autonomous mode for a given account, it will get enabled by drift.

## The counter-pressure is real

I don't want to pretend the market is rewarding restraint right now. It mostly isn't.

The day before Honeywell's launch, Workday [made its Trusted Agent Platform headless](https://en-gb.newsroom.workday.com/2026-10-13-Workdays-Trusted-Agent-Platform-Now-Delivers-Headless-Access-to-HR-and-Finance,-Letting-Customers-Build-and-Run-Lawful-AI-Agents) — agents doing real work in HR and finance with no user signed in. Notably, it shipped with governance as the headline rather than an afterthought; CTO Gabe Monroy's framing, [per The New Stack](https://thenewstack.io/workday-headless-mcp-agents/), was that "headless can't mean lawless." Google, meanwhile, [made Gemini 4 Argon generally available](https://venturebeat.com/technology/google-makes-gemini-4-argon-broadly-available-with-limited-time-low-api-pricing-of-2-10-per-1m-token) and pitched it at long, multi-step work.

The platform layer is sprinting toward agents that act without a human present. That's the context your roadmap is being graded against, and "ours advises" will sound slow in a board meeting.

Which is exactly why the ladder beats a binary. You are not choosing between autonomous and irrelevant. You are choosing whether the escalation is a decision with evidence behind it or an accident with a changelog entry.

## Practical takeaway

If you're shipping an agent into an operational workflow in the next quarter:

1. **Name your modes in the product**, not just in the spec. If a customer can't see which mode they're in, you don't have modes.
2. **Default to advisory for v1**, even if the model is better than that. You lose less than you think and you learn the override rate.
3. **Instrument the override now.** Log every recommendation, every human decision, and the delta. Without this, you will never have the evidence to escalate, and you'll escalate on vibes instead.
4. **Rank actions by reversibility** and write down which tier graduates first.
5. **Put the escalation switch in the customer's hands**, with a named internal owner for flipping it per account.
6. **Test the stop path** before launch, with a real interruption, and write down who confirmed it.

The useful reframe from this week: shipping an autonomy mode you don't turn on isn't an unfinished feature. It's a finished decision about who is accountable, made early, while it's still cheap to make.

**Word count: 1,237** (draft body only, excluding link URLs; within the 1,000–1,400 target)

---

# Hero image

**I could not verify a real, usable image for this article.** Outbound page fetching is blocked in this environment — every direct fetch of an image, source page, or license page failed (DNS/proxy refusal), and web search alone cannot confirm that a specific photo exists, who shot it, or what license it carries. Per the brief, I am not presenting an unverified link as if it were checked.

What I can offer are two **unverified leads** to check by hand before use. Do not publish either without opening the page and reading the license:

- **Lead 1 (unverified):** Unsplash surfaced a photo page in search results at `https://unsplash.com/photos/the-control-room-of-a-ship-with-multiple-monitors-PWY7d4kBFIQ` — described as a ship control room with multiple monitors. Photographer unknown; I will not guess a name. Unsplash's collection pages state images are free for commercial use with no attribution required, but I could not confirm that for this specific photo.
- **Lead 2 (unverified):** Pexels' [control panel collection](https://www.pexels.com/search/control%20panel/) surfaced industrial panels with switches and dials, which fits the "switch you don't throw" theme better than a robot cliché. Individual photo URLs, creators, and licenses unconfirmed.

**Fallback cover image description (use this to source or commission):** A wide, editorial shot of an industrial or building-systems control panel in muted tones — matte metal, physical toggle switches and dials, shallow depth of field — with one switch clearly in the "off" position and slightly separated from the rest of the row by light or focus. Cool neutral palette, no faces, no screens full of fake dashboards, no robots or androids. The visual argument is a capable system with one control deliberately left down. A close second: an empty operator's chair in front of dim monitors, shot from behind, implying a system running in advisory mode with a human still holding the decision.

If a verified image is required before publishing, source it manually from Unsplash or Pexels and paste the attribution line the photo's own page specifies.

---

# Metadata

**Medium tags:** Product Management, Artificial Intelligence, AI Agents, Product Strategy, Automation

---

## Unverified claims

- **All image licenses are unconfirmed.** Outbound fetching was blocked, so neither hero image lead was opened or license-checked. Both are flagged above as unverified leads, and no direct image URL, photographer name, or attribution line is asserted.
- **No publication date was independently verified on any source page.** The brief asks for date confirmation on the source page itself; WebFetch and curl both failed for every host in this environment, so all dates below come from search results and URL date slugs rather than from the pages. This affects every citation in the draft.
- **Honeywell's pilot figures are vendor-reported, not independent.** The up-to-90% reduction in unnecessary alerts, ~10% identified energy savings, and 95%+ weighted comfort score are Honeywell's own numbers from a single 90-day NVIDIA Voyager pilot. At least one outlet noted the 90% figure was not independently confirmed at publication. The article states this inline.
- **The Fortune quotes are relayed through search results,** not read on Fortune's page. The CTO's wording ("We have not opened up an autonomy right now"; "Maybe we will start running in this mode for probably next two to three years") and his name (Suresh Venkatarayalu) are consistent across multiple result sets, but I could not read the article directly. Note that one aggregator attributed the launch commentary to a different Honeywell executive; I went with the name Fortune's own coverage carried.
- **The two-to-three-year horizon is one executive's estimate**, not a committed product roadmap.
- **Workday and Gemini 4 Argon items are dated October 13, 2026** — three days old, just outside the 48-hour window. They are used only as supporting context for the competitive picture, not as the article's basis. The Honeywell launch (October 14) is inside the window.
- **I did not reach Hacker News, Reddit r/ProductManagement, Product Hunt, or any PM newsletter directly.** Searches for 48-hour-fresh material from those sources returned only aggregators and older posts, so no claim in the draft rests on them. The r/ProductManagement "can AI replace PMs" thread that surfaced was ~2 weeks old and was not used.
- **"Operators can mark whether they agree with a classification"** appeared in an early search summary but was **not** confirmed by Honeywell's announcement or Fortune's coverage. It has been removed from the draft; the agreement-rate recommendation in "What earns the next rung" is my own advice, not a described Honeywell feature.
