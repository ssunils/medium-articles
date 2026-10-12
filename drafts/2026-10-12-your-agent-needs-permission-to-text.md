# Design

**Subtitle:** Twenty-two AI agents now live inside text messages. The two channels that matter are gated, and the gatekeepers decide what kind of product you're allowed to be.

**Target reader:** A product manager at a 20–200 person consumer or SMB-facing AI company deciding whether to ship their assistant into iMessage, WhatsApp, or SMS instead of (or alongside) their own app.

**Key takeaway:** Messaging is not a distribution channel you choose — it's a permission you apply for, and the application asks what category of product you are, so answer that question before you pick the channel.

**Format:** channel-decision

## Section outline

1. Open on the list: 18 agents on Oct 3, 22 on Oct 10
2. The bet everyone is making — no app to install
3. What the list doesn't show — there is no open door
4. The same company won one lane and lost the other
5. Three doors, and the product each one permits
6. The question to answer before the channel question
7. What the thread costs you that an app doesn't
8. Practical takeaway

## Headline options

**1. "22 AI agents now live in texts. One got permission."** (10 words)
Hook: specific surprising number plus stakes. — **RECOMMENDED**
Reason: the number is concrete and checkable, and the second clause sets up exactly the tension the article resolves.

**2. "iMessage isn't a distribution channel. It's a permission slip."** (9 words)
Hook: contrarian claim challenging the PM belief that messaging equals free reach.

**3. "Can your AI agent legally live in a text message?"** (10 words)
Hook: sharp question most PMs cannot answer confidently about their own roadmap.

---

# Draft

## 22 AI agents now live in texts. One got permission.

On October 3, TechCrunch's running list of AI agents you can reach by text message had 18 entries. By October 10, [it had 22](https://techcrunch.com/2026/10/10/all-the-ai-agents-that-can-live-in-your-text-messages/) — Comma, Szn, Tab, and Underdog joined a roster that already included Caddy, Folk, Instinct, Martin, Ohai, Poke, Tomo, and a dozen others ([full roster here](https://daily.dev/posts/here-are-the-top-ai-agents-that-can-live-in-your-text-messages-6a1nzvssj)).

Four new entrants in a week, all making the same bet: people would rather text an assistant than install one.

The money agrees. Instinct, which works over text and phone calls, [raised $1 billion at a $10 billion valuation](https://www.vktr.com/ai-platforms/instinct-raises-1b-at-10b-valuation-to-scale-its-personal-ai-agent/) on September 28 — roughly four times its valuation from a month earlier.

If you run a product team, this looks like a distribution channel opening up. It isn't. It's a permission regime, and most of the doors are closed.

## The bet, and why it's a good one

The pitch for a message-thread agent is genuinely strong, and I don't want to undersell it.

No install. No onboarding screens. No push-notification opt-in. Caddy, in [public beta since April 2026](https://techcrunch.com/2026/10/10/all-the-ai-agents-that-can-live-in-your-text-messages/), reaches iPhone users over iMessage and Android users over RCS, with no separate inbox to check.

For an assistant whose whole job is "handle this for me," the thread is the right surface. Your user is already there. Group chats come free. Retention is whatever their habit of opening Messages already is.

That's a real advantage over an app you have to convince someone to download, and it explains why four more teams shipped into the channel last week.

## The part the roster doesn't show

Here's what the list of 22 doesn't tell you: Apple does not publish a general-purpose iMessage API for arbitrary agent conversations. [There is no open door](https://www.clawmessenger.com/blog/imessage-api-for-ai-agents).

The sanctioned route is Apple Messages for Business, which was built for companies doing support and transactions with their own customers. It requires an approved commercial messaging provider, a registration review, and — critically — a human. Apple's own guidance says escalation to a human agent is mandatory and that it [won't approve a deployment using virtual agents exclusively](https://register.apple.com/resources/business-chat/faq/business-chat-faqs.html); a blend of automated and human agents [is required](https://register.apple.com/resources/messages/messaging-documentation/faq). Providers add that a live agent has to be reachable [whenever a customer texts "help"](https://knowledgecenter.cm.com/knowledge-center/communications-platform/other-channels/apple-messages-for-business/do-i-need-a-human-agent-with-apple-messages-for-bu).

One AI agent has publicly been reported through that door. Poke was [approved on June 4, 2026](https://www.techwyse.com/news/platform-updates/apple-messages-for-business-first-ai-agent-poke-approved) as the first AI agent cleared to operate on the platform. The conditions: clear branding, an opt-in prompt, a disclosure that the user is talking to an AI, and [the option to switch to a person](https://www.devx.com/daily-news/poke-wins-approval-for-apple-messages/).

The unofficial route has a precedent, and it isn't encouraging. Beeper Mini reverse-engineered the iMessage protocol in December 2023 and stopped working [three days after launch](https://www.tomsguide.com/news/game-over-apple-blocks-android-imessage-app-beeper-mini), after Apple said it had blocked techniques that "exploit fake credentials to gain access to iMessage."

Szn, the iMessage agent from a former Siri engineer, launched this month, and public reporting [doesn't say which route it uses](https://macdailynews.com/2026/09/28/former-siri-engineer-launches-imessage-ai-agent-szn-that-can-shop-talk-to-vendors-and-act-on-your-behalf/). That's the open question worth watching.

## The company that won one lane and lost the other

WhatsApp went the other way.

Meta added an "AI Providers" section to its WhatsApp Business Platform terms, barring general-purpose AI assistants from the API, [effective January 15, 2026](https://techcrunch.com/2025/10/18/whatssapp-changes-its-terms-to-bar-general-purpose-chatbots-from-its-platform). Task-specific bots — support, order status, appointments — [remain allowed](https://respond.io/blog/whatsapp-general-purpose-chatbots-ban). Meta's position is that the Business API exists for customer support and notifications, [not consumer-facing assistants](https://www.eesel.ai/blog/meta-policy-changes-affecting-third-party-ai-chatbots-on-whatsapp).

That rule hit ChatGPT, Perplexity, Luzia — and Poke, the same product Apple had just let in. Poke's WhatsApp support is now limited; [it runs over SMS and Telegram instead](https://techradar.com/ai-platforms-assistants/meta-will-ban-rival-ai-chatbots-from-whatsapp).

> The same company won Apple's lane and lost Meta's in the same year. Nothing about its product changed — only the category the platform assigned it.

Regulators are pushing on this. The EU, Italy, and Brazil have opened antitrust probes into Meta over the rules, which means the policy may not be stable either. "It might get better" is not a plan you can staff.

## Three doors, three different products

Stop asking "should we be in iMessage." Ask which door, and what it permits.

**Door 1: Sanctioned business rails.** Apple Messages for Business, WhatsApp Business Platform. Durable, reviewed, and scoped to you doing your own business with your own customers. Costs: provider integration, a review cycle, AI disclosure, and a staffed human escalation path. If your agent is support, order status, or booking, this is your door.

**Door 2: An unofficial bridge.** Works today, ships this quarter, and is one enforcement action from zero. Beeper Mini is the base rate. Only sane if the channel is an experiment, not the product.

**Door 3: Channels that want bots.** Telegram, SMS, RCS. Stable, documented, no category police. Smaller and differently-shaped reach than iMessage, and SMS costs real money per message. This is where general assistants actually live, including Poke now.

Most teams I've seen debate this treat it as a reach question and pick Door 1 or 2 by install base. It's a category question, and the category determines which doors even exist for you.

## The question to answer first

Before the channel decision, answer this one: **is your agent conducting your company's business with your own customer, or is it a general assistant acting on the user's behalf?**

If it's the first, the sanctioned rails are built for you, and the human-escalation requirement is a staffing line item to budget, not a blocker.

If it's the second, the two biggest channels are closed to you by policy. Door 3 is your real option, and any iMessage plan is a bet on an approval you cannot schedule.

Teams get hurt by answering this question implicitly. You build a general assistant, launch on a business-messaging integration, grow, and get reclassified. The reclassification is the risk, not the API.

## What the thread costs you

Two costs worth naming up front, because they land on your team and not on engineering.

The human escalation requirement means the sanctioned rails come with a staffing commitment. A support rota is now part of shipping an AI feature, and "help" has to reach a person.

And the disclosure requirement shapes your product copy, not just your legal page. The user has to know it's an AI, be offered a person, and opt in. If your positioning depends on the agent feeling like a friend in the thread, read those conditions before you write the launch narrative.

## Practical takeaway

1. **Write one sentence classifying your agent** — "our business, our customer" or "general assistant" — and get your legal and support leads to agree with it. That sentence decides your channel options.
2. **Read the actual terms**, not a vendor's summary: Apple's [Messages for Business FAQ](https://register.apple.com/resources/messages/messaging-documentation/faq) and the WhatsApp Business Platform AI Providers terms. Twenty minutes each.
3. **Price the human path.** If you're going through sanctioned rails, cost the escalation rota and put it in the launch budget now.
4. **If you're on an unofficial bridge, timebox it.** Set a date to either be approved or be on Telegram/SMS, and tell your exec team the Beeper Mini number: three days.
5. **Add one line to your channel risk register:** "platform reclassifies our agent's category." Name an owner. Poke's year is the case study.
6. **Don't make messaging your only surface** until you've been through a review cycle and come out the other side.

The agents on that list of 22 aren't winning because they found a loophole. The ones that will still be there in a year are the ones whose product matches the door they walked through.

---

# Hero image

**I could not verify any image for this article.** The environment's network policy blocked every image host I tried — `unsplash.com`, `images.pexels.com`, `www.pexels.com`, and `api.openverse.org` all failed to resolve, and direct requests returned `403` from the outbound proxy. I was able to surface candidate pages through web search, but I could not open them to confirm the photo exists, read its license, or capture a direct image URL. I'm listing the candidates as leads only — **do not publish either link without opening it first.**

### Candidate 1 (UNVERIFIED — search result only)
- Source page: `https://www.pexels.com/photo/close-up-shot-of-a-person-texting-7120144/`
- Title: "Close-Up Shot of a Person Texting"
- Creator (per search result): cottonbro studio
- Expected license: Pexels License (free for commercial use, no attribution required)
- Direct image URL: **not captured** — Pexels builds these dynamically and I will not guess one.
- Attribution line if you want to credit anyway: `Photo by cottonbro studio on Pexels`

### Candidate 2 (UNVERIFIED — search result only)
- Source page: `https://www.pexels.com/photo/a-person-texting-9898360/`
- Title: "A Person Texting"
- Creator (per search result): Ron Lach
- Expected license: Pexels License (free for commercial use, no attribution required)
- Direct image URL: **not captured**
- Attribution line if you want to credit anyway: `Photo by Ron Lach on Pexels`

Both are literal "person texting" shots rather than the abstract or editorial framing I'd prefer. Worth 60 seconds of browsing before settling.

### Fallback cover image description

A tight, slightly overhead shot of a hand holding a phone in a dim room, the screen's message thread glowing but deliberately out of focus so no text is readable, with a lot of dark negative space to the left or above for the Medium title to sit. Cool blue-grey cast from the screen, no visible app branding, no robot or android imagery, no illustrated chat bubbles. The feeling to aim for is a private conversation whose other participant you can't see — which is the article's subject. An acceptable alternative: a close-up of a closed glass door or turnstile with a soft light behind it, shot abstractly enough to read as "gatekeeping" rather than as stock-photo architecture.

---

# Metadata

**Medium tags:** Product Management, AI Agents, Product Strategy, Messaging, Platform Risk

---

## Unverified claims

Network access in this environment blocked direct page fetches for most news and image domains (`techcrunch.com`, `news.ycombinator.com`, `register.apple.com`, `respond.io`, `www.pexels.com`, `unsplash.com` and others returned DNS failures or `403` from the outbound proxy). I could search the web but could not open most source pages, so **publication dates below come from search results and URL date slugs rather than from the pages themselves**, contrary to how I'd normally verify them. Please spot-check before publishing.

- **The TechCrunch roster grew from 18 entries on October 3 to 22 on October 10.** The October 10 URL slug and multiple secondary summaries support this, and the 22-name roster came from a daily.dev summary, not from the TechCrunch page. I could not open TechCrunch to confirm the count, the four additions, or the Caddy "public beta since April 2026" detail.
- **Poke was approved on June 4, 2026 as the first AI agent on Apple Messages for Business.** Reported by two secondary outlets. Apple has not independently confirmed the "first and only" framing, per one of those reports. The article hedges this as "publicly reported."
- **Apple's human-escalation and AI-disclosure requirements.** The escalation requirement is quoted from Apple's own FAQ pages via search results, but one of those pages is roughly four years old and still uses the former "Business Chat" name, so current wording may differ. The "reachable whenever a customer texts help" detail comes from a provider's knowledge base, not Apple. I did not use the "welcome message within 5 seconds" figure I saw in one secondary source, because I could not confirm it.
- **Meta's AI Providers terms, effective January 15, 2026.** Consistently reported across many secondary sources and a TechCrunch piece from October 2025, but I could not read Meta's actual WhatsApp Business Solution terms. The task-specific-bots-still-allowed carve-out comes from vendor explainers interpreting the policy.
- **Poke's current WhatsApp status and the EU/Italy/Brazil antitrust probes.** From secondary coverage only. I also saw a single-source claim that the ban was reversed for EU/EEA markets on July 13, 2026 following EU intervention; no other source mentioned it, so I left it out of the article entirely.
- **Instinct's $1B Series C at a $10B valuation, September 28, 2026.** Widely reported, but one aggregator lists the valuation as $6.47 billion and sources disagree on the earlier Series B amount ($250M vs $350M) and the launch month. I used only the Series C figures and the "roughly four times" comparison.
- **Szn's access method.** Correctly stated as unknown — that is itself the sourced claim.
- **"There is no general-purpose public iMessage API."** Sourced to a developer blog (clawmessenger.com), not to Apple. Consistent with everything else I found, but it's a vendor source.
- **Both hero images.** License, existence, and direct URLs all unconfirmed, for the reasons above.
- **"Most teams I've seen debate this..."** — that's my read, not a sourced claim, and it's phrased as such.
