# Design

**Subtitle:** OpenAI's Intelligent UI moves the interface from something you design to something the model emits at runtime. That breaks three things PMs rely on.

**Target reader:** A B2B SaaS product manager at a 50–500 person company who already ships an LLM-backed feature and is now deciding whether to build into ChatGPT's plugin surface — or whether to let a model generate UI inside their own product.

**Key takeaway:** When the interface becomes a runtime output instead of a designed artifact, you lose design review, stable instrumentation, and A/B testing — so decide deliberately which screens stay deterministic and which you are willing to stop measuring.

**Section outline:**
1. Hook: the most capable reasoning mode doesn't get the new interface
2. What actually shipped on October 7
3. Why this is a roadmap problem, not a demo
4. The three things generated UI quietly breaks
5. What nobody has measured yet
6. What you still own
7. Practical takeaway

**Headline options:**

1. **How Do You QA a Screen That Doesn't Exist Until Runtime?** — *RECOMMENDED* (hook: sharp question the reader can't answer confidently). Reason: it names the exact gap most PMs have not thought about yet, and the Practical takeaway section answers it directly, so the hook pays off.
2. **OpenAI's Smartest Mode Doesn't Get Its New Interface** (hook: specific surprising result)
3. **Your AI Feature's Interface Is No Longer Yours to Design** (hook: contrarian claim challenging a common PM belief)

---

# Draft

## How Do You QA a Screen That Doesn't Exist Until Runtime?

OpenAI's most expensive reasoning mode does not get its newest interface.

That detail sits in the rollout notes for Intelligent UI, which [OpenAI shipped alongside GPT-6 in ChatGPT on October 7](https://qz.com/openai-chatgpt-gpt-6-intelligent-ui-interactive-visuals-100826). The feature is available from Instant through Extra High reasoning, but [the Pro reasoning option continues to use GPT-6 Astra and doesn't support Intelligent UI](https://9to5mac.com/2026/10/07/openai-brings-gpt-6-to-chatgpt-and-debuts-intelligent-ui/). Pay the most, think the hardest, get plain text.

Hold onto that, because it hints at what generated interfaces are currently good for — and what they are not.

## What actually shipped

Intelligent UI lets the model decide when a visual beats a paragraph. Instead of returning prose, ChatGPT can [dynamically combine text, visuals, and interactive elements based on the question](https://www.xda-developers.com/gpt-6s-new-feature-adds-interactive-elements-to-your-chat/) — tappable buttons, forms, charts. It can also [build small working tools inside the conversation, like calculators and bill splitters](https://the-decoder.com/chatgpt-with-gpt-6-ditches-mostly-text-output-for-interactive-ui-with-charts-buttons-and-mini-apps/). The interface renders progressively as the response generates.

Rollout was staged: paid tiers first, with [free and Go users getting GPT-6 Luna from October 8](https://qz.com/openai-chatgpt-gpt-6-intelligent-ui-interactive-visuals-100826).

If you only ship inside your own app, that reads like consumer news. It isn't, because of what landed at DevDay a week earlier. Plugins can now [take a home in ChatGPT's sidebar with interactive panels people use alongside the chat](https://openai.com/index/devday-2026-recap/), plus custom file viewers. Two announcements, one direction: the conversation surface is becoming a place other people's products get rendered.

The Gradient's read on DevDay — ["Always-On Agents, Borrowed Interfaces"](https://thegradient.com/thinking/what-openai-devday-2026-means-for-product-teams) — puts the question well. When your product appears inside an interface you don't own, who decides what it may do, and how does anyone check?

## This is a roadmap problem, not a demo

Here is the decision actually in front of you. It is not "should we use Intelligent UI" — you don't control that. It's whether you put part of your product into a surface where the presentation layer is generated per request, and whether you start generating UI inside your own product because this is now table stakes.

Both versions trade the same thing away. A designed interface is an artifact: it exists before a user arrives, it can be reviewed, instrumented, and held still long enough to measure. A generated interface is an output. It exists for one user, once.

That trade breaks three things product teams quietly depend on.

**Design review.** Your design system encodes accessibility, error states, and empty states that someone argued about for a week. A model composing controls at runtime has no obligation to any of it.

> You cannot run a design review on a screen that doesn't exist until the moment someone asks for it.

**Instrumentation.** Funnel analytics assume stable elements. If the model decides this user gets a chart and that user gets three buttons, "click-through on the primary CTA" stops being a coherent metric, because there is no stable primary CTA.

**A/B testing.** Experiments need two fixed variants. If no two sessions render the same interface, you cannot isolate the change you made from the change the model made.

None of that means generated UI is a bad bet. It means the bet costs you measurement, and most roadmaps haven't priced that in.

## What nobody has measured yet

Worth being plain about how early this is: one launch guide notes there is [no independently validated benchmark for Intelligent UI](https://kingy.ai/blog/gpt-6-intelligent-ui-chatgpt-guide/), and that calculation accuracy, working controls, accessibility, mobile usability, and task completion without user repair all still need independent measurement. The same piece flags the real failure mode — a weak generated interface that adds decoration, or hides a fragile calculation behind convincing controls.

That last one should worry you most. A wrong number in a paragraph looks like a claim you might check. The same wrong number inside a calculator with working buttons looks like a tool.

Early reaction is mixed. On [Hacker News](https://news.ycombinator.com/item?id=49996425), one commenter hoped the interactive features wouldn't spread into professional tools, and another named the overreach risk directly: sometimes what you want is just a simple response. OpenAI's own [developer forum thread](https://community.openai.com/t/gpt-6-and-intelligent-ui-in-chatgpt/1404139/6) ran negative, with posters reading the update as consumer-first and speculating that API access would lag.

Which brings back the Astra detail. The mode aimed at the hardest reasoning is the one without generated UI. Read conservatively, that suggests Intelligent UI is a presentation-layer bet, not a reasoning upgrade — useful where the answer is simple enough that the interface is the hard part, and withheld where the reasoning is the hard part. That reading is my inference, not OpenAI's stated rationale.

## What you still own

Scope, approvals, and logs. The Gradient's practical advice for product teams is to design for [how far an agent's scope reaches, where human approvals sit, and what action logs record](https://thegradient.com/thinking/what-openai-devday-2026-means-for-product-teams).

Those three survive the interface becoming generated, because they are not interface concerns. They sit underneath it. A model can render your data however it likes and still be unable to exceed the scope you granted, skip the approval you required, or act without leaving a record.

If the presentation layer is becoming someone else's output, the layer worth investing in is the one that constrains it.

## Practical takeaway

Concrete next actions, in rough order of effort:

1. **Split your surfaces into two lists.** Screens where variation is fine (exploration, summaries, Q&A) and screens where it isn't (anything involving money, permissions, destructive actions, or a compliance claim). Generated UI is a candidate for the first list only.
2. **Re-check which metrics assume a stable DOM.** Any funnel step, CTA conversion rate, or click heatmap on a surface you're considering generating. Decide now whether you're willing to lose it, or whether you need event-level instrumentation that fires on intent rather than on a specific element.
3. **Write down what a generated interface may not do** before you ship one — not as a design guideline, but as an enforced scope: which actions it can trigger, which require confirmation, what gets logged.
4. **Add one QA question to your AI feature reviews:** if the model rendered a control here and the underlying number were wrong, how would anyone notice? If the answer is "they wouldn't," the interface is doing harm, not work.
5. **Don't rebuild your product around plugin panels this quarter.** Make your product easy for an agent to call — clear actions, clear scopes, readable responses — and let the rendering surface settle. That investment pays off regardless of which surface wins.

The useful instinct here isn't to chase generated UI or refuse it. It's to notice that you're being offered speed in exchange for measurement, and to choose where that trade is actually worth making.

---

# Hero image

I could not open any image page to verify these, because this environment's network policy blocked every outbound page fetch I attempted. The two candidates below came back through search, including photographer and license, but **I did not confirm them on the source page** — check both before publishing.

**Candidate 1 (preferred)**
- Source page: https://unsplash.com/photos/symmetrical-abstract-pattern-of-modern-buildings-XIWA8_767pU
- Title: "Symmetrical abstract pattern of modern buildings"
- Photographer: Mike Hindle
- License (per search result, unconfirmed): Unsplash License — free to use, no attribution required
- Published (per search result): October 1, 2025
- Direct image URL: not verified. Unsplash direct URLs live on `images.unsplash.com` and are generated per size; open the source page and use its download link rather than a guessed URL.
- Why it fits: repeating modular facade reads as "many near-identical variants of one structure" — the generated-interface idea without a robot.
- Attribution line (optional under the Unsplash License, but good practice): `Photo by Mike Hindle on Unsplash`

**Candidate 2 (backup)**
- Source page: https://unsplash.com/photos/an-abstract-image-of-a-building-made-of-blocks-E2Edd5xR7VQ
- Title: "An abstract image of a building made of blocks"
- Photographer: A Chosen Soul (shot in Surat, India)
- License (per search result, unconfirmed): Unsplash License — free to use, no attribution required
- Published (per search result): January 23, 2024
- Direct image URL: not verified, same caveat as above.
- Attribution line: `Photo by A Chosen Soul on Unsplash`

**Fallback description, if neither verifies:** A tight, abstract shot of a modular building facade or a grid of identical structural units, photographed straight-on so the repetition reads as pattern rather than architecture. Cool neutral tones — concrete grey, pale blue glass — with one unit visibly out of alignment or a different shade. Editorial and quiet, no screens, no robots, no glowing brains. The visual idea is a system assembling itself from interchangeable blocks, where one block doesn't match.

---

# Metadata

**Medium tags:** Product Management, Artificial Intelligence, Product Design, UX, Software Development

---

## Unverified claims

Flagging honestly: **this environment's network policy blocked every outbound page fetch** (DNS resolution failed for every host I tried — OpenAI, Unsplash, Wikipedia, and four news sites). Server-side web search worked, so all research below rests on search results and the excerpts they returned. **I could not open a single source page to confirm a publication date or a license.** Every claim in the draft is attributed to a real URL, but the dates and quotes come from search excerpts rather than the pages themselves.

Specific items to re-check before publishing:

- **The October 7, 2026 launch date for GPT-6 and Intelligent UI.** Multiple independent outlets reported it (Qz, 9to5Mac, the-decoder, The AI Insider), and one URL is date-stamped `2026/10/07`, so I'm reasonably confident — but unconfirmed on-page.
- **That Pro reasoning / GPT-6 Astra does not support Intelligent UI.** This is the article's opening hook and rests on a single source's rollout detail. Verify against OpenAI's own release notes before publishing. If it's wrong, headline option 2 must be dropped and the opening rewritten.
- **The staged rollout detail** (paid tiers on GPT-6 Sol first, free and Go on GPT-6 Luna from October 8) — reported, not confirmed.
- **Model naming is genuinely inconsistent across sources.** Some coverage says the chat experience runs GPT-6.0 while GPT-6.1 exists; DevDay coverage variously headlines "GPT-6.1 Sol" and "GPT-6 Astra." I deliberately avoided version numbers in the draft for this reason.
- **DevDay plugin-extension details** (sidebar home, interactive panels, custom file viewers). DevDay itself was roughly 9–10 days ago, outside the 48-hour window; I used it as context, not as fresh news, and said so in the draft. The specific feature list came partly from third-party roundups.
- **The Gradient article's framing and its three-part advice** (scope, approvals, logs). The article exists at the cited URL and its title and argument came back consistently in search, but I could not read it. Its claim that OpenAI shelved GPT-6.1 Astra before the event appeared in only one source, so **I excluded it from the draft entirely.**
- **Both Hacker News comments and the OpenAI developer-forum reaction.** Paraphrased from search excerpts of those threads; I could not load either thread. Comment attributions are to the thread, not to named individuals, deliberately.
- **The Kingy AI "no independently validated benchmark" claim.** This is a single blog's assessment, not a formal study. I characterised it as a launch guide's view in the draft rather than as established fact.
- **Both hero images.** Existence, license, publication date, and photographer are all per search result only. Neither direct image URL is verified, and I have not invented one.
- **My reading of why Astra lacks Intelligent UI** is explicitly labelled in the draft as my inference, not OpenAI's stated rationale.
