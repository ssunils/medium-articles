# Design

**Subtitle:** A Hacker News argument about agent architecture is really a question about who gets to correct your product when it's wrong.

**Target reader:** A B2B SaaS PM at a 50–500 person company who has "remembers user preferences" or "learns from past conversations" sitting in a spec right now, and hasn't yet decided what the memory looks like from the user's side.

**Key takeaway:** Ship memory as a small set of inspectable, editable, dated records — because the retrieval-based alternative serves superseded facts a meaningful share of the time and leaves you with nothing to show a customer when it does.

**Format:** debate-brief

**Draft word count:** 1,202 words (within the 1,000–1,400 target)

## Headline options

1. **AI Memory Served the Wrong Answer in 36% of Tests** — *RECOMMENDED.* A specific number the article actually pays off with a cited study, and it reframes memory from a feature to a reliability question.

2. **Stop Shipping AI Memory. Ship Notes Users Can Edit.** — Contrarian hook: challenges the assumption that "memory" is the obvious thing to build.

3. **Can You Show a Customer What Your AI Remembers?** — A sharp question most PMs shipping memory cannot answer confidently.

## Section outline

- Open on the Hacker News thread and the specific gap it exposed in how memory gets specced
- Separate the two things "memory" means in a spec: implicit recall vs. explicit state
- The stale-fact number, with its limits stated
- The counterargument from the comments: documentation is a maintenance surface, not a free win
- What ChatGPT, Claude and Gemini already shipped, and what that reveals
- The three decisions this actually reduces to
- Practical takeaway

---

# Draft

## AI Memory Served the Wrong Answer in 36% of Tests

On Monday, an essay with a flat, almost rude title landed on the Hacker News front page: [*Agents Don't Need Memory. They Need Documentation.*](https://liao.gg/blog/agents-dont-need-memory) By Tuesday morning it had [371 points and 290 comments](https://github.com/kouweizhu/agents-radar/issues/356) and was [still climbing](https://news.ycombinator.com/item?id=49945933).

I don't particularly care who wins the architecture fight. What caught me is that it exposed something I keep seeing in specs, including ones I've written.

Roughly half the AI features I review this quarter contain a line like "remembers user preferences" or "learns from previous conversations." Almost none of them say what the user sees when that memory is wrong.

That's not a detail. It turns out to be the whole decision.

## "Memory" is doing two different jobs in your spec

When a spec says memory, it usually means one of two things, and the author rarely says which.

The first is **implicit recall**: take the conversation history, chop it into chunks, embed them, and retrieve by similarity at prompt time. Nothing is declared. The system just seems to know things.

The second is **explicit state**: a short, readable record of decisions, preferences and constraints that the system reads before it works and updates afterwards.

The [essay's](https://liao.gg/blog/agents-dont-need-memory) argument is that the first approach is the one most memory plugins took, and that it's a design error. Vectorizing conversation history into thousands of snippets and pulling them back by similarity produces fragments stripped of their original context — fragments that can be stale, can be wrong, and are essentially unauditable. Its proposal is a versioned workspace of structured Markdown: specs, decisions, research notes, indexes. A readable brain.

For a PM, the useful part isn't the Markdown. It's the word *auditable*.

## The number worth putting in your spec review

Here's where the debate stops being aesthetic.

A study on [real software histories](https://arxiv.org/abs/2608.20685) built a benchmark from 707 GitHub issues (SWE-bench Lite and Verified), extracting 130 clean cases where a fix changes one identifiable value from a pre-fix to a post-fix form. Then it asked retrieval-based memory which value was current.

Forced to answer, RAG served the superseded value **36.1%** of the time. Allowed to abstain, 26.2%. Adding an LLM reranker made it slightly worse, at 37.7% — because reranking reorders retrieved chunks but cannot distinguish a stale value from a current one. A deterministic supersession layer, which retires the old value from the store before retrieval, drove the error to roughly zero.

A [companion line of work](https://arxiv.org/abs/2606.26511) puts the general range at 15–40% stale answers when the system is forced to commit, depending on domain.

Two honest caveats. This is a code-assistant benchmark, not your product, and the authors are proposing their own alternative — treat the headline figure as directional, not as your expected error rate. The direction is what matters: similarity search has no model of time, so it cannot tell "true" from "was true."

> A vector index is not a policy. It can tell you what looks similar; it cannot tell you what is still true.

## The counterargument is also right

The comment thread didn't just nod along, and the pushback is worth reading before you over-rotate.

One strand argued there's no real difference between typing your constraints at the start of every session and putting them in a file — except that redoing work after an agent's mistake costs [one to three orders of magnitude more tokens](https://viblo.asia/p/agents-dont-need-memory-they-need-documentation-a-practical-agentsmd-playbook-G24B8g6WLz3) than including the constraint up front. Which is an argument *for* the file, but a cost argument, not an architecture one.

The sharper point was about what belongs in documentation at all: the narrow, non-inferable things. The custom build flag. The weird test harness. The constraint the agent would otherwise burn thirty tool calls discovering. Not everything the user ever said.

So documentation isn't a free win. It's a maintenance surface, and surfaces need owners. If your answer to "who keeps this current" is "it updates itself," you've reinvented the problem you were trying to leave.

## What the large assistants already decided

This is the part I'd bring to a roadmap conversation, because it's evidence rather than opinion.

[ChatGPT splits memory in two](https://gptprompts.ai/chatgpt-memory-guide): saved memories, which are an explicit editable list, and reference chat history, which is implicit recall. [Claude](https://www.ai-toolbox.co/claude-management-and-productivity/claude-memory-how-it-works-2026) makes every entry visible in a memory panel you can edit, delete, pause or reset. [Gemini](https://blog.memoryplugin.com/claude-vs-chatgpt-vs-gemini-memory/) lets you edit saved instructions per entry, but offers no single list of what it absorbed from past chats — you largely have to ask it.

Notice the pattern. The explicit, inspectable list is the part everyone shipped and put in settings. The implicit recall is the part that's harder to show, harder to correct, and the part users describe as a black box.

The UX writing on this is blunt: if users can't see what shaped an answer, [personalization reads as surveillance rather than a feature](https://aiuxplayground.com/pattern/memory-manage). That's a support-ticket problem, a churn problem, and in enterprise deals, a security-review problem.

## The decision, reduced

Strip the architecture talk out and you're left with three questions. They're answerable this week.

**What is the smallest set of facts worth persisting?** Not everything the user said. The handful of things that change the output materially — their stack, their tone, their constraints, the decision you already made together. If the list doesn't fit on a screen, you're storing transcripts, not memory.

**Who can see and correct it?** If the answer is "nobody outside engineering," you have no correction path, which means your only tool when a customer reports a wrong answer is an apology.

**How does a fact die?** This is the one most specs skip entirely. Facts get superseded. Preferences change. A memory store with no expiry, no validity date and no supersession rule will confidently serve last quarter's answer, and the retrieval layer won't flag it.

## Practical takeaway

Concrete things to do before your next AI feature review:

1. **Find the word "remembers" in your spec and replace it with a list.** Write out the specific fields you intend to persist. If you can't enumerate them, the feature isn't specced yet.

2. **Add a "wrong memory" row to the spec.** What does the user see, where do they click, and how long until the correction takes effect? If there's no answer, that's your next ticket.

3. **Give every stored fact a date and a source.** Even a timestamp and a "learned from conversation on X" string. Dated records can be aged out, audited and explained. Undated ones can only be trusted or deleted.

4. **Build a tiny stale-fact test set.** Twenty cases where a value changed: known-correct facts, deliberately stale ones, and contradicting updates. Measure how often your system serves the old value. You want this number before a customer finds it.

5. **Decide, out loud, who owns the memory surface.** Not the storage layer — the content. Name a person in the spec.

The fight on Hacker News is about agent architecture. The question for you is older and narrower: when your product gets a fact wrong about a customer, can you show them what it believed and let them fix it?

If not, you haven't shipped memory. You've shipped a guess that's hard to argue with.

---

# Hero image

**Honest status: I could not verify any image.** This session's network policy blocked Unsplash, Pexels and Openverse at the egress proxy, so I was unable to confirm that any specific image exists or that its license permits commercial use. Rather than present a URL I couldn't load, I'm giving the fallback description below. Two search routes are noted so this takes about ninety seconds once the network allows it.

**Fallback cover image description:**

An overhead, slightly desaturated shot of a physical index-card file or library card catalogue — a drawer pulled partway open, handwritten or typed cards visible in a neat row, with one card lifted or set apart from the others. The appeal is that it's editorial rather than literal: it reads as structured, human-readable, correctable records, which is exactly the argument of the piece, and it avoids the robot-and-android cliché entirely. Muted wood and paper tones, shallow depth of field, strong enough contrast that Medium's title overlay stays legible. A close second would be a wall of labelled archive boxes or a legal-style filing room shot straight on, which carries the same "records you can open and check" feeling with more geometry.

**To source it once the network allows (two routes, pick whichever verifies first):**

- Unsplash, search terms `card catalog`, `index cards`, `library catalogue drawer`. Unsplash License permits commercial use with no attribution required, though crediting the photographer is the norm and I'd do it.
- Openverse, search terms `card catalog`, filtered to CC0 or CC BY. If the chosen image is CC BY, the attribution line under the image must read: `"<Image title>" by <Creator name> is licensed under CC BY <version>.` with both the image page and the license deed linked.

Do not publish any image until the license is confirmed on the source page itself.

---

# Metadata

**Medium tags:** Product Management, AI Agents, Artificial Intelligence, Product Strategy, Software Development

---

## Unverified claims

The environment's network policy blocked outbound access to every domain I tried except github.com, so I could not open most source pages directly. Search results were the only route to the rest. Flagging everything that follows from that:

- **The essay's publication date.** Search results and two dated digests place *Agents Don't Need Memory. They Need Documentation.* on Hacker News on 5 October 2026, but `liao.gg` and `news.ycombinator.com` were both blocked, so I could not read the byline date on the post itself. The article says "Monday," which is correct for 5 October 2026.
- **The 371 points / 290 comments figure.** This I did verify first-hand, from a [dated digest on GitHub](https://github.com/kouweizhu/agents-radar/issues/356) (6 October 2026) — the one source I could load. Note that other search results reported different counts for the same thread (324; 297 with 173 comments; 348 in the [5 October digest](https://github.com/kouweizhu/agents-radar/issues/344)), which is consistent with a thread still accumulating votes, but means the figure is a moving snapshot, not a stable fact.
- **The 36.1% / 26.2% / 37.7% stale-fact figures, the 130-transition and 707-issue benchmark details, and the near-zero result for deterministic supersession.** All from search results describing arXiv 2608.20685. `arxiv.org` was blocked; I could not read the paper. Two independent searches returned the same numbers, which is reassuring but is not the same as reading the abstract. The article states the directional caveat in-line.
- **The 15–40% general range.** From search results describing arXiv 2606.26511. Not read directly.
- **The Hacker News counterarguments** (the "no difference between typing it each session" point, the "one to three orders of magnitude more tokens" figure, and the "narrow, non-inferable directives" framing). These came through search summaries of the comment thread and a secondary write-up. I could not open the thread, so I cannot confirm wording, attribution, or whether these were prominent comments or minor ones. The article attributes them loosely ("one strand argued") for this reason.
- **ChatGPT, Claude and Gemini memory behaviour.** From search summaries of third-party guides, not from vendor documentation. The specific mechanics — ChatGPT's saved-memories/reference-chat-history split, Claude's editable memory panel, Gemini's lack of a single absorbed-facts list — are plausible and consistently reported across several of those guides, but no vendor help page was reachable. I dropped one claim I'd found (that Claude memory reached free plans on 2 March 2026) from the draft rather than assert a precise date I couldn't confirm.
- **The UX framing** that invisible personalization reads as surveillance, cited to aiuxplayground.com. From search summary; page not reachable.
- **Both hero images.** No image URL, photographer or license was confirmed. Nothing is presented as verified; see the Hero image section.

Everything else in the draft is argument and judgement rather than reportage, and is mine.
