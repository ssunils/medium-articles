# Design

**Format:** teardown

**Subtitle:** Meta's Muse renders the same activity at three depths. The interesting part is the rule for choosing yours.

**Target reader:** A B2B SaaS PM at a 50–300 person company shipping their first agentic feature — something that takes actions over seconds or minutes — who has to decide what the user sees while it runs.

**Key takeaway:** Whether you can hide your agent's work is set by two things you already measure — how long the task takes and how hard it is to undo — not by a general principle about transparency.

**Section outline:**
1. Open on the three-depth detail from the Muse interview
2. What Meta actually built, and the thread decision underneath it
3. The uncomfortable claim: speed is what buys you silence
4. The counter-case: a step list is not reasoning
5. The two variables that should drive your call
6. Practical takeaway
7. What I'd watch next

**Headline options:**

1. **Your Agent's Thinking Indicator Is Covering for a Slow Model** — *contrarian claim; challenges the belief that visible reasoning builds trust.* **RECOMMENDED** — it is the one idea here a working PM has probably never had put to them directly, and the piece pays it off with the Muse team's own reasoning rather than my opinion.
2. **Meta Shows Muse's Work at Three Depths. Pick Yours.** — *specific concrete result; names the artifact the reader can go look at.*
3. **Hide Your Agent's Reasoning and You Inherit Its Mistakes** — *stakes framing; what it costs you when the bet is wrong.*

---

# Draft

## Your Agent's Thinking Indicator Is Covering for a Slow Model

Meta's Muse renders the same piece of agent activity three different ways: a single emoji, an expandable task list, and raw execution logs.

Same work. Three depths. The user picks.

That detail comes from a [How I AI interview with Alex Cornell](https://www.lennysnewsletter.com/p/how-i-ai-how-meta-designed-muse-with), the design director for Muse, published Monday. It is the most concrete answer I have seen to a question I keep watching product teams answer by accident: while your agent is working, what does the person see?

Most teams settle this in a hallway. Someone asks whether the spinner should say something. An engineer notes that the tool-call stream is already there, so it gets piped to the screen. That becomes the product.

It deserves an actual decision, and there is now enough public material to make one.

## What Meta actually built

The three tiers are the headline, and they are plain progressive disclosure: an emoji for someone glancing at their phone, a checklist for someone who wants to know what happened, [raw logs for engineers](https://www.antoinebuteau.com/daily-digest-2026-10-12/). Each audience gets the depth it needs without the others paying in screen clutter.

The structural choice under it is less obvious and probably matters more. The team built Muse as a single ongoing thread rather than spawning a separate conversation per task, which preserves context across time instead of fragmenting it into job records.

Cornell describes the governing test as asking whether the experience would still make sense if you were talking to a person, which is [what pushed the team away from conventional chat furniture](https://imasters.com/design-ux/how-meta-designed-muse-to-not-feel-like-an-ai-app) like message bubbles.

That test is portable, and it is harsher than it sounds. A competent colleague handling a task for you does not narrate every database query. They also do not vanish for four minutes and reappear with a result and no explanation.

## The part that should make you uncomfortable

Here is the claim from the episode that I think PMs have under-processed: visible reasoning is often a workaround for slow models. Muse is fast enough to simply deliver results, so it does not need to perform its thinking to hold your attention.

Read that as a product statement rather than a design preference and it reframes the whole question.

> Progress narration is a bill you pay for latency. Get fast enough and the bill goes away.

If that is right, then every team streaming chain-of-thought to the user as a trust feature should check what it is actually buying. Some of it is trust. Some of it is a waiting room with the clock painted on the wall.

I would not take this as settled. It is one team's conclusion about one consumer product, and Meta operates at a latency budget most companies cannot buy. But it is a testable claim, and the test is cheap: cut your agent's p50 latency meaningfully, then remove the narration and watch whether trust metrics move. If they do not, the narration was load-bearing for the wait, not for the trust.

## The counter-case is real

The agent-UX practitioners pushing back have the stronger argument on one specific point.

A list of steps is not reasoning. One essay on agentic UX makes the case that most implementations [confuse transparency with disclosure](https://consciousux.ai/notes/the-discipline-taking-shape-notes-on-agentic-ux) — that a chain of tool calls shows you what happened while hiding the thing you actually need, which is the alternatives the agent considered and rejected. The decision between three plausible paths is almost always invisible in the timeline.

That is the real gap in every agent UI I have used, Muse's tiers included. A task list tells me the agent searched three vendors. It does not tell me why it stopped at three, or what made it drop the fourth.

The same writing is blunt about the noise problem from both ends: silence reads as failure, constant narration reads as anxiety. Another practitioner argues step-by-step narration [is not transparency but interruption](https://www.andreamabellini.com/2026/09/24/designing-for-ai-agents-ux-patterns-that-actually-work/), and would reserve notifications for approvals, exceptions, and completion, sending everything else to a log you can open later.

The emerging middle position is to skip raw chain-of-thought and instead surface [the one or two factors that actually drove the decision](https://www.gokhanmeric.com/blog/designing-for-ai-agents-ux-principles-autonomous-systems/). That is harder to build than streaming a log, which is exactly why most products stream the log.

## The two variables that should decide it

Strip the principles away and your call comes down to two numbers you already have.

**How long does the task take?** Under a couple of seconds, narration is noise — ship a quiet result. Past roughly ten seconds, silence starts reading as a hang, and you owe the user something. Not a reasoning trace; a status that tells them it is alive and roughly where it is.

**How hard is the result to undo?** This one does the heavier lifting and gets discussed less. If the agent drafted something the user reviews before it goes anywhere, you can hide nearly all the work — the review step is the transparency. If the agent sent the email, moved the money, or changed a customer record, the user needs to see what it decided *before* it commits, because afterward their only option is cleanup.

So: fast and reversible, stay quiet. Slow and reversible, show status. Fast and irreversible, show the decision and gate it. Slow and irreversible, show the decision, gate it, and expect to earn the autonomy over several releases rather than at launch.

Note what is not on that list: how impressive the reasoning looks in a demo. Streamed thinking is genuinely compelling in a sales call and genuinely tiring on day thirty.

There is also a disclosure floor underneath all of this that is not a UX question. Meta learned that the hard way in September, when it turned out some Muse phone calls [were being completed by human call-center workers](https://www.404media.co/meta-tests-muse-ai-agent-calls-that-are-actually-made-by-humans-in-a-call-center/) and internal testers said they only found out afterward. Whatever depth you choose, what the user sees cannot misrepresent who or what did the work.

## Practical takeaway

Four things you can do this week:

1. **Write down your current choice.** Open your agentic feature and name the depths it exposes. Most teams have exactly one, chosen by whoever wired up the stream. Naming it is usually enough to start the argument you need to have.
2. **Plot each agent action on the two axes.** Latency and reversibility, one row per action. The quadrant tells you the disclosure level. Expect to find at least one irreversible action running silent — that is the bug to fix first.
3. **Add the rejected alternative to one surface.** Pick your highest-stakes action and show what the agent chose *against*, not just what it did. One line. This is the cheapest trust win available and almost nobody ships it.
4. **Run the latency test before you add more narration.** If your instinct is to show more thinking, check whether you are fixing trust or decorating a wait. Faster is the better fix when you can afford it.

And keep the colleague test on hand for review meetings. If a capable human doing this task for you would not say it out loud, your agent probably should not either — and if they *would* say it, silence is not a design choice, it is a gap.

## What I'd watch

Whether anyone ships the rejected-alternatives view as a real pattern rather than an essay recommendation. It is the clearest unmet need in agent interfaces right now, and the first team to make it legible without making it noisy will set the convention for everyone else.

**Word count:** 1,257 (draft section only, excluding link URLs and markup)

---

# Hero image

**Important:** this session's network policy blocked all outbound page fetches (every host returned `403` at the proxy CONNECT stage, and WebFetch failed DNS resolution). I could not load Unsplash, Pexels, or Openverse to confirm these images, their direct file URLs, or their licenses. What follows is sourced from search results only. **Verify both candidates in a browser before publishing**, and do not paste a direct image URL from here — I have deliberately not constructed one, because the `images.unsplash.com` form requires a file ID I cannot read without loading the page.

**Candidate 1 (primary)**
- Source page: https://unsplash.com/photos/abstract-view-of-textured-translucent-glass-IGLNYCWJUGI
- Title: "Abstract view of textured, translucent glass"
- Creator: Jason Leung
- Stated license (per search result, unconfirmed): Unsplash License — free for commercial use, no attribution required
- Direct image URL: **not obtained** — read it off the source page
- Why it fits: layered translucency is a literal visual for progressive disclosure — the same thing visible at different depths. Abstract and editorial, no robot cliché.
- Courtesy attribution line (optional under the Unsplash License, good practice anyway):
  `Photo by Jason Leung on Unsplash`

**Candidate 2 (backup)**
- Source page: https://unsplash.com/photos/modern-building-interior-with-frosted-glass-panels-Nfbw_1hhybA
- Title: "Modern building interior with frosted glass panels"
- Creator: Declan Sun
- Stated license (per search result, unconfirmed): Unsplash License
- Direct image URL: **not obtained**
- Why it fits: overlapping frosted panels read as tiers of visibility; architectural rather than abstract, and more workspace-adjacent.
- Courtesy attribution line: `Photo by Declan Sun on Unsplash`

**Fallback description, if neither verifies:** A wide, low-contrast editorial shot of three or four overlapping translucent panels — frosted glass, acrylic, or vellum — lit from behind so that a shape is fully crisp through the nearest layer, softened through the second, and only a suggestion of tone through the third. Cool neutral palette, one muted accent, generous negative space on the left third for title overlay. The image should read as the same object seen at three degrees of resolution. Avoid robots, androids, humanoid hands, glowing brains, and circuit-board motifs.

---

# Metadata

**Medium tags:** Product Management, AI Agents, UX Design, Artificial Intelligence, Product Design

---

## Unverified claims

Outbound network fetching was blocked for this entire run, so **no claim below was confirmed against a primary source page** — WebFetch failed DNS resolution on every host and direct `curl` returned `403` from the agent proxy on CONNECT. Search-engine result summaries were the only channel available. Treat everything here as needing a browser check before publishing.

- **Publication dates could not be verified.** The task calls for confirming each source's date on the page itself. I could not. The Alex Cornell / Muse "How I AI" interview is reported by search results as October 12, 2026 (two days ago, inside the 48-hour window), and that date is corroborated by a second source — a daily digest also dated October 12 describing the same three-tier model. Both dates remain snippet-sourced.
- **The three-depth disclosure model** (emoji / task list / raw logs) is attributed to the Muse interview and corroborated by the October 12 digest. Wording of the tiers is paraphrased from search summaries, not quoted from the episode.
- **"Visible reasoning is often a workaround for slow models."** This is the load-bearing claim of the piece and the basis of the recommended headline. It is attributed to the How I AI episode via search summary. I could not read the episode or its transcript. The Lenny's Newsletter post may also be partly paywalled. **Verify this directly before publishing under that headline** — if the episode does not support it, the headline and the "part that should make you uncomfortable" section both need rewriting.
- **The single-thread architecture choice** (no separate thread per task) comes from the October 12 digest only; I found no second source.
- **Cornell's "would this make sense if you were talking to a person" test** is reported by search summaries of the episode and by a secondary write-up (imasters). Paraphrased, not quoted.
- **All three agent-UX counter-sources** (consciousux.ai, Andrea Mabellini, Gokhan Meric) are opinion/practitioner pieces, not research, and are presented as such in the draft. Their arguments are paraphrased from search summaries. The Mabellini piece is dated September 24, 2026 by its URL — outside the 48-hour window, and used only as supporting argument, not as news.
- **The Muse human call-center story** is from September 2026 reporting (404 Media and Reuters), explicitly labeled as September in the draft rather than presented as fresh. Sources reportedly conflict on whether Meta rolled the feature back; the draft avoids that disputed detail and states only what internal testers reported about disclosure. Reported figures I chose not to use: human callers reaching 95–98% success rates.
- **The two-axis framework** (latency × reversibility), the latency thresholds (~2s, ~10s), the quadrant rules, and all four practical takeaways are **my own analysis, not sourced claims.** The thresholds are rules of thumb, not findings from research.
- **Both hero images are unverified** — existence, direct URL, creator attribution, and license all rest on search-result text. No image page was loaded.

**On freshness:** the 48-hour window yielded one genuinely strong, decision-shaped item (the October 12 Muse design interview) and one paywalled candidate I passed on (an October 13 Lenny's piece on startup moats). The counter-arguments that give the piece its tension are older practitioner writing, used as argument rather than as news and dated inline where known. I did not pad with older announcements.
