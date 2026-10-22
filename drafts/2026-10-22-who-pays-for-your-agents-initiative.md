# Design

**Subtitle:** Anthropic and OpenAI shipped proactive agents three weeks apart with opposite billing models. The split tells you what you actually need to measure.

**Target reader:** A PM at a B2B SaaS or consumer app (roughly 50–500 people) about to ship something that acts without being asked — a daily digest, a watcher, an alerting agent, an assistant that surfaces things on its own.

**Key takeaway:** Once your product initiates, engagement stops being evidence of value, because every action spends the user's attention and sometimes their budget before any value arrives — so you need a precision metric and an explicit answer to who absorbs the cost of checking.

**Headline options:**

1. *Claude Duet's background checks come out of your own usage limit*
   (hook: specific, surprising fact)
2. **RECOMMENDED** — *Engagement is the wrong metric for anything your product starts*
   (hook: contrarian claim challenging a default PM belief. Recommended because the article's practical core is the replacement metric, and this headline promises exactly that and nothing more.)
3. *Who pays when your product decides to check on something?*
   (hook: sharp question most PMs cannot answer confidently)

**Section outline:**
- Open on the specific spec detail: Duet checks every few hours, and those checks draw down your plan
- The cost of initiative has to land somewhere (Duet vs Dots vs Walmart)
- Engagement stops being evidence
- Three numbers that hold up
- The approval gate is also a measurement instrument
- Practical takeaway

---

# Draft

## Engagement is the wrong metric for anything your product starts

Anthropic's new Claude Duet checks your connected apps every few hours rather than continuously — and the reason given is budget, not battery. Continuous checking would eat through your plan limits far faster, [according to launch coverage](https://www.engadget.com/2293646/claude-duet-is-anthropics-answer-to-meta-muse-and-openai-dots/). Those background checks still [count against the same usage allowance as your own chats](https://www.macrumors.com/2026/10/21/anthropic-claude-duet/).

Read that as a product decision rather than a spec line. Anthropic shipped a feature whose whole point is acting without being asked, and billed the user's own budget for the asking.

OpenAI went the other way three weeks earlier. With Dots, [talking to your dot doesn't count toward ChatGPT limits](https://openai.com/index/introducing-dots/), though tasks it kicks off in Codex or ChatGPT Work do.

Same product category, same week in the news cycle, opposite answers to one question: who pays when the product decides to do something?

Most of us are about to face a smaller version of that question, and the honest answer is that our metrics aren't set up for it.

## The cost of initiative has to land somewhere

When a user asks your product for something, they've already decided it's worth their time. The request *is* the consent. Everything downstream — latency, compute, a mediocre answer — is a cost they opted into.

A proactive feature has no such moment. It spends something before anyone has agreed to the trade.

It spends attention, always. [Anthropic frames Duet](https://x.com/claudeai/status/2112984664256241837) as something that "comes to you with what needs your attention" — which is a promise, and also an admission that the product is the one choosing when to interrupt.

Sometimes it spends literal money or quota, as the Duet limits show. Sometimes it spends trust: Walmart's Agent Profiles, [announced the same day](https://www.cryptopolitan.com/ai-agents-walmart-profiles-spending-caps/), default to requiring customer sign-off on every purchase, with optional caps of $50, $100 or $200 if you'd rather let an agent buy on its own.

Three different companies, three different places to put the cost. None of them could avoid putting it somewhere.

> A request-driven product earns attention. A proactive one spends it, and the spending starts before any value arrives.

## Engagement stops being evidence

Here's the part that breaks the dashboard.

For a request-driven feature, usage going up is reasonable evidence that the feature is working. People keep coming back; something is landing.

For a proactive feature, the equivalent number — notifications sent, items surfaced, checks run — measures how much you spent, not what you returned. A digest that fires every morning has 100% "delivery" whether it's useful or noise. You can double the number of things your agent surfaces and make the product strictly worse.

The mobile industry already learned this the expensive way. Braze's survey of push notification behaviour found a [38.3% opt-out rate across apps](https://www.braze.com/resources/articles/opt-out-of-push-notifications-why-users-do-it), dropping to 24.5% when one outlier respondent was excluded. Opt-in benchmarks from Airship put the [median at roughly 51% on iOS and 81% on Android](https://www.businessofapps.com/marketplace/push-notifications/research/push-notifications-statistics/) — meaning a large share of users have already pre-emptively closed the channel.

Those are vendor-published numbers and should be read as directional rather than precise. But the direction is consistent and it's the one that matters: when a channel is used carelessly, users don't complain, they revoke it. The failure is silent and usually permanent.

Proactive AI features inherit that failure mode, with a twist. A push notification costs the user a glance. An agent that checks your email every few hours and gets the urgency wrong costs a glance *and* a slice of the allowance you're paying for.

## Three numbers that hold up

If "how many things did we surface" is the wrong number, here's what I'd replace it with. None of these require new infrastructure — two of them are a thumbs-up button and a query.

**1. Acted-on rate, not open rate.** Of the items your product surfaced unprompted, what fraction did the user actually do something about — click through, resolve, reply, dismiss-as-handled? Opens tell you the subject line worked. Acted-on tells you the judgment call was right. Anything below about a third and you are training people to ignore the channel.

**2. Cost per surfaced item, including the quiet checks.** Duet's design makes this concrete: the checks that find nothing still cost something. Divide total spend — compute, API calls, quota drawn from the user's plan — by the number of items that cleared the bar and got shown. If you only count the cost of the things you surfaced, you are hiding the majority of the bill.

**3. Suppression rate.** What fraction of candidate items did the system look at and deliberately *not* show? If that number is near zero, you don't have a judgment layer, you have a pipe. A healthy proactive feature should be throwing away most of what it finds, and you should be able to say what the threshold is.

The useful thing about the third number is that it forces an argument you'd otherwise have after launch. Someone has to own where the bar sits.

## The approval gate is also a measurement instrument

Both launches gate consequential actions. Duet [asks for approval before sending a message, making a payment, signing a document, or deleting a file](https://www.macrumors.com/2026/10/21/anthropic-claude-duet/). Walmart makes per-purchase approval the default and treats a spending cap as the thing you opt into.

Approval gates are usually discussed as a safety feature, and they are. But they're also the cheapest instrumentation you will ever ship.

Every approval prompt is a labelled example: the system proposed something, and a human said yes or no. That's a precision measurement you get for free, generated by the users who care most, before you've committed to automating anything.

Which suggests a sequencing rule: ship the gate first, run it long enough to learn your approval rate, then decide what to automate. Removing a gate later because the data says you've earned it is a good day. Adding one back after an incident is not.

It also means the gate should log the *no*. A rejection you don't record is a free label thrown away.

## Practical takeaway

If you're shipping something that acts without being asked, do these this week:

- **Write down who absorbs the cost of checking** — your margin, the user's quota, or their attention — and put it in the spec. Anthropic and OpenAI made opposite calls here and both documented it. If yours isn't written down, it defaults to the user and nobody decided it.
- **Replace your volume metric before launch, not after.** Acted-on rate, cost per surfaced item (including empty checks), suppression rate. A dashboard that only shows volume will tell you a worsening product is improving.
- **Instrument the approval gate to log rejections.** Treat them as your precision dataset.
- **Set the suppression threshold explicitly, and name its owner.** "We show roughly the top 10% of candidates" is a decision. "We show what the model thinks is important" is not.
- **Add a frequency control before you need one.** Anthropic says it's [still tuning Duet's judgment about when to message you](https://www.engadget.com/2293646/claude-duet-is-anthropics-answer-to-meta-muse-and-openai-dots/), with user controls for frequency and topics planned. Shipping the control alongside the feature is cheaper than retrofitting it after the opt-outs.

It's early for this category — Duet is a [research preview, US-only, Pro and Max subscribers on a waitlist](https://9to5google.com/2026/10/21/claude-duet-anthropic-ai-agent-waitlist/) — and the conventions will shift. But the measurement problem isn't going to be solved by the model getting better at judging urgency. It's a product question about what you're willing to spend on someone's behalf, and how you'll know if it was worth it.

Decide that before the feature ships. Afterwards, the only signal you get is silence.

**Word count (Draft section): 1,259**

---

# Hero image

I could **not** verify either candidate directly. Outbound fetching to image hosts (unsplash.com, pexels.com, openverse.org) was blocked by DNS in this environment, so the entries below come from search results only. Do not publish either without opening the page and confirming the license yourself.

**Candidate 1 (unverified)**
- Source page: https://unsplash.com/photos/abstract-pattern-of-light-and-shadow-on-a-window-Cqbvp9OPLzk
- Description: Abstract pattern of light and shadow on a window; minimalist, monochrome, geometric.
- Creator (per search result): Liana S
- License (per search result): Unsplash License — free for commercial use, attribution not required
- Direct image URL: **not confirmed** — could not load the page to obtain the `images.unsplash.com` file URL. Do not guess it.
- Attribution line (optional under the Unsplash License, recommended): `Photo by Liana S on Unsplash`

**Candidate 2 (backup, unverified)**
- Source page: https://unsplash.com/photos/ripples-on-dark-water-surface-at-dusk-ET7HhIWd3SQ
- Description: Ripples on a dark water surface at dusk; minimal, calm, abstract.
- Creator (per search result): H&CO
- License (per search result): Unsplash License
- Direct image URL: **not confirmed**
- Attribution line (optional, recommended): `Photo by H&CO on Unsplash`

**Fallback description (use this if neither checks out):**
A quiet, abstract editorial image suggesting something watching on your behalf without demanding attention. Ideal frame: a dim interior at dawn, a single soft light source throwing a geometric pattern across a wall or desk surface, muted and largely monochrome, with generous negative space on the left for the title to sit over. No robots, no androids, no glowing blue brains, no humanoid hands reaching toward screens. A second workable direction: a long-exposure shot of a single notification-sized point of light in a dark frame, surrounded by emptiness — the visual argument being that one signal in a lot of quiet is the whole product goal.

---

# Metadata

**Medium tags:** Product Management, AI Agents, Product Metrics, Artificial Intelligence, Product Strategy

---

## Unverified claims

Outbound web fetching was blocked for nearly every domain in this environment (DNS resolution failed for engadget.com, macrumors.com, 9to5google.com, techcrunch.com, cryptopolitan.com, unsplash.com, openverse.org and others). Only anthropic.com resolved, and it carried no Claude Duet post. **Every claim below therefore rests on search-result summaries of dated coverage rather than on a page I opened and read.** The Duet and Walmart details were each corroborated across several independent outlets, which is why I used them, but none were confirmed against a primary source.

- **Claude Duet exists, launched 2026-10-21 as a US research preview for Pro and Max subscribers via waitlist.** Reported consistently by MacRumors, 9to5Google, 9to5Mac, Engadget, Digital Trends and Cryptobriefing, all dated 2026-10-21, plus an @claudeai post on X. Anthropic's own newsroom index did not list it when checked, so I could not confirm it against Anthropic directly.
- **Duet checks connected accounts every few hours, spaced that way to conserve plan limits.** Launch coverage only.
- **Duet's background checks count against the same plan usage limits as regular Claude chats.** Multiple outlets agree; the exact session/weekly mechanics are not confirmed.
- **Duet asks for approval before sending a message, making a payment, signing a document, or deleting a file.** Launch coverage only.
- **Anthropic says it is still tuning Duet's judgment about when to message you, with frequency and topic controls planned.** Attributed to Anthropic in coverage; I could not read Anthropic's own wording.
- **OpenAI Dots launched 2026-09-29; talking to a dot does not count toward ChatGPT limits while Codex / ChatGPT Work tasks do.** Attributed to OpenAI's announcement page, which I could not open.
- **Walmart Agent Profiles announced 2026-10-21, per-purchase approval as default, optional caps of $50 / $100 / $200, launching November.** Coverage only; Walmart's corporate newsroom was unreachable.
- **Braze opt-out figures (38.3%, 24.5% excluding one outlier) and Airship opt-in medians (≈51% iOS, ≈81% Android).** Vendor-published research, not peer-reviewed, and the Airship benchmark is from 2021. Flagged as directional in the article text.
- **Both hero image candidates.** Creator names and license type come from search snippets. Licenses unconfirmed, direct file URLs unknown and deliberately not guessed.
