# Design

**Subtitle:** Seven South Korean financial firms were breached through loan-broker portals and employee support tools. Core banking was never touched.

**Target reader:** A PM at a 200–2,000 person B2B SaaS or fintech company who owns — or has quietly inherited — a partner, broker, reseller or internal-admin surface alongside the main product.

**Key takeaway:** The Korean bank breaches landed on auxiliary partner- and staff-facing systems rather than core banking, which means the surface most likely to leak your customer data is the one with no PM, no roadmap and no threat model — and deciding who sees what on it is a product decision, not a security one.

**Format:** audit-guide

**Section outline:**
1. The attackers skipped the front door (open on the specific entry point)
2. What a side door actually looks like (the enumeration mechanics)
3. Nobody owns the partner portal (why this lands on PM, not security)
4. The friction you keep getting asked to remove (the real tradeoff)
5. What's new here, and what isn't (honest about the unconfirmed AI attribution)
6. Practical takeaway

**Headline options:**

1. **Seven Banks Breached. Core Banking Was Never Touched.** — *RECOMMENDED*
   Hook: surprising result. It is the best-corroborated fact in the whole story and it is also the article's actual argument, so the headline and the payoff are the same thing.

2. **Your Partner Portal Is Your Weakest Product. Nobody Owns It.**
   Hook: contrarian claim — challenges the belief that breach exposure tracks with product importance.

3. **Which Of Your Surfaces Could A Stranger Enumerate Today?**
   Hook: a sharp question most PMs cannot answer confidently about their own product.

---

# Draft

## The attackers skipped the front door

The people who took customer data from at least seven South Korean financial firms over the last two weeks never touched core banking.

No consumer app. No payment rails. They walked in through [a web service built for loan brokers](https://www.americanbanker.com/news/ai-linked-hacks-hit-korean-banks-through-loan-agent-sites) — the portal that Shinhan Bank's outside loan solicitors use to check on applications.

Roughly 25,000 Shinhan customers had names, phone numbers, annual income and [calculated loan limits exposed](https://www.khan.co.kr/en/article/202610011825017/). Shinhan's own account is that an external party reached the service "by an abnormal method that bypassed authentication."

Then it spread. KB Kookmin, Hana, BNK Busan, Yegaram Savings Bank, Welcome Savings Bank and Hyundai Capital all reported exposure, and the incidents [concentrated on the same class of system](https://www.digitaltoday.co.kr/en/view/110617/hacking-emergency-spreads-from-banks-to-savings-banks-and-capital-firms-in-south-korea-finance-sector): loan query services, employee mobile support platforms, sales support databases. Not internet banking. Not the mobile app.

South Korea's Financial Services Commission now [puts combined exposure above 68,000 people](https://www.whalesbook.com/news/English/bankingfinance/South-Korea-Launches-Probe-Into-Major-Bank-Data-Breaches/6ac219a65aacb956d08aef7c). President Lee Jae Myung said on October 6 that [AI appears to have been used](https://www.usnews.com/news/world/articles/2026-10-05/south-koreas-lee-says-ai-appears-to-have-been-used-in-bank-hacks) in some of the intrusions.

I want to set the AI part aside for a moment, because it is the least settled thing in the story and it is not what should worry you. What should worry you is the shape of the target.

## What a side door actually looks like

Here is the mechanic, as far as it has been reported. On the broker portal, an attacker [cycled through randomized customer identification numbers](https://mbiz.heraldcorp.com/article/10891096) against a lookup endpoint, collecting customer numbers, then fed those numbers into a second service that returned contact details and dates of birth.

That is not an exploit. There is no memory corruption, no zero-day, no clever chain. It is a query interface doing exactly what it was built to do, called more times than anyone imagined it would be called.

One analysis of the Shinhan incident describes the attackers as having taken advantage of [ordinary cyber hygiene failures rather than complex vulnerabilities](https://www.thehackacademy.com/news/shinhan-bank-data-breach-ai-evidence/). I believe that, and it is the uncomfortable part.

Every element of that failure was specified by somebody writing requirements. Who can log in. What a single lookup returns. Whether the response changes when the ID doesn't exist. Whether anyone counts how many lookups one session performs. Those are product decisions. They were made, or skipped, long before a security team ever saw the thing.

## Nobody owns the partner portal

The detail I keep coming back to: Shinhan's loan recruiters **are not bank employees**. They are an outside channel. And they had been given access to sensitive customer credit data — access that critics in Korea have called [excessive](https://www.khan.co.kr/en/article/202610011825017/).

I have watched that decision get made in a ten-minute meeting. The channel team needs brokers to see income and approval limits, because a broker who can't see them can't sell. Somebody asks whether that's a lot of data to hand a contractor. Somebody else says the portal is behind a login. The ticket gets written.

> The surface you never scoped is still a product decision. You just made it by default.

Now your own org chart. Who is the PM for your reseller dashboard? Your internal admin console? The CSV export support uses? The mobile tool your field staff log into?

Usually the honest answer is nobody, or a PM who inherited it three reorgs ago and has never put it in a roadmap review. No success metric, so no owner, so no threat model — and it reads from the same customer database as the product with twelve dashboards pointed at it.

The reasonable counterargument: these surfaces are low-traffic and low-revenue, so hardening them costs attention that customers aren't paying for. True, and it's exactly why they stay unhardened. The asymmetry is that a breach on a surface with 400 users costs about what one with 400,000 costs, because blast radius is set by what the surface can read, not by how many people use it.

## The friction you keep getting asked to remove

One reported contrast is worth sitting with, with a flag upfront: it is not confirmed, and accounts differ on whether Woori Bank was affected at all.

Woori reportedly requires its loan agents to connect only from [designated tablets, with a separate digital certificate and a biometric check](https://seoulz.com/korea-bank-hack). Some reporting says it was targeted and repelled the attack; other reporting says it was breached. I can't resolve that, and nobody should build a strategy on a disputed fact.

So hold the case aside and look at the design pattern, which holds regardless of how Woori's week went.

A broker who needs a company-issued tablet, a certificate and a fingerprint to see a customer's income has a measurably worse experience than one who needs a password. That's friction. It costs channel partners, slows onboarding, and generates a trickle of complaints that reach a PM as "the broker portal is painful."

That friction is the control. Not a WAF, not a monitoring dashboard — a device binding and a second factor, which is to say a product requirement someone had to defend against the people whose numbers it hurt.

The tradeoff is yours: channel velocity against exposure, priced in a currency nobody dashboards. I won't pretend the answer is always "add friction." I'm saying the price of that friction currently gets argued in rooms where nobody has quantified the other side of the ledger.

## What's new here, and what isn't

Now the AI part, carefully.

Investigators [found traces of a Chinese-language open-source AI penetration-testing tool](https://therecord.media/south-korean-bank-hacks-ai-agents) on a server linked to the attack, and officials suspect agents probed for weaknesses. But no published logs, command history or forensic finding shows that tool executed any part of the intrusion. [Bloomberg](https://www.bloomberg.com/news/articles/2026-10-02/ai-tools-suspected-in-korea-s-shinhan-bank-hack-yonhap-says) says attackers "probably" used AI agents. Credential stuffing remains an alternative. Attribution is genuinely open.

The uncertainty doesn't let you off the hook. Enumeration has always been limited by effort — somebody had to find the obscure portal, read its responses, write the loop. Capable agents plausibly lower that cost, which makes obscurity worth less than it was. That's a reasonable expectation, not a proven fact, and I'd rather say so than dress it up.

Either way the defensive move is identical. Rate limits, scoped responses and device binding on a forgotten portal are worth building whether the thing hammering it is a contractor's script or an agent.

The regulatory consequence is already concrete. Korean authorities ordered firms to check internet-facing systems, tighten authentication and access controls, and [block outside access](https://en.sedaily.com/finance/2026/10/04/korea-orders-financial-firms-to-block-outside-access-after) pending review. All 79 savings banks have completed self-checks, with sector-wide remediation of basic IT controls [running through November](https://startupfortune.com/south-korea-orders-financial-sector-security-checks-after-bank-data-breaches-spread/).

## Practical takeaway

Four things, in order, and the first one is a week of work at most:

**1. List every surface that reads your customer database.** Not every product — every surface. Partner portals, admin consoles, internal support tools, exports, legacy dashboards, that mobile app for field staff. Put a named PM next to each. The ones you can't name an owner for are your finding.

**2. For each one, answer: what does a single lookup return?** If a broker queries one application and the response includes income and credit limits, you have specified the blast radius of a leaked session. Trim the response payload to what the job needs. This is usually a small change and it is the highest-leverage one.

**3. Check whether anyone counts.** Pick your least-loved internal surface and ask what happens when one session makes 10,000 sequential lookups with incrementing IDs. If the answer is "it works," you've found the Shinhan pattern in your own product. Rate limiting and non-enumerable identifiers are the fix.

**4. Price the friction you're defending.** Before the next review where someone asks you to drop the second factor on the partner login, have a number for what the data behind it is worth. Without one you'll lose that argument, and you should — unquantified caution loses to quantified velocity every time.

None of this is novel security advice, and that's the point. The Korean banks weren't beaten by sophistication. They were beaten on surfaces no product process was watching. The fix isn't a better defense; it's extending the ownership you already apply to your main product to the four or five side doors you forgot you shipped.

Go find out who owns your partner portal. If that takes more than a day, that's the finding.

**Word count: 1,390**

---

# Hero image

**I could not verify any image for this article, and I am not going to present a link I haven't confirmed.**

This session's network egress policy blocked every image source: `unsplash.com`, `www.pexels.com` and Openverse all returned egress-proxy denials, as did every news domain I tried to open. I could run web searches (which execute server-side) but could not load a single page to confirm that an image exists, that its URL resolves, or that its license permits commercial use.

Search results did surface candidate Unsplash pages, but I am listing them as **unverified leads to check manually**, not as usable images:

- `unsplash.com/s/photos/backdoor` — a search results page, reported to contain closed/service-style door photos
- `unsplash.com/photos/a-building-with-two-doors-and-a-clock-on-it-fKWvILqMvqQ` — reported as an illuminated entrance under the Unsplash License

Before using either, open the photo page, confirm it loads, confirm the license line reads "Unsplash License," and copy the photographer's name from that page. Unsplash License does not require attribution, but crediting the photographer is good practice; if you land on a CC BY image instead, attribution is mandatory and must name the creator, the license and link both.

**Fallback cover image description (use this brief if you're sourcing manually):**

A tight, slightly off-centre shot of an unremarkable service door on the side of a modern office building — plain steel or painted metal, a keypad or card reader beside it, no signage, no people. Shoot or select it in flat, overcast daylight so it reads as mundane rather than ominous. The main entrance should be absent from frame entirely, or visible only as a blurred suggestion of glass at the extreme edge. Muted palette: grey concrete, desaturated paint, one small accent of colour from the reader's LED. The image should feel administratively boring, because that is the argument — this is the entrance nobody photographs, nobody maintains, and nobody put on the floor plan. Avoid: robots, androids, glowing blue circuitry, hooded figures, padlock icons, binary rain. Any of those will undercut a piece whose whole point is that the attack was ordinary.

---

# Metadata

**Tags:** Product Management, Artificial Intelligence, Cybersecurity, Fintech, Product Strategy

---

## Unverified claims

**Process limitation, stated upfront:** This session's network egress policy blocked direct page fetches to every source domain I attempted (`therecord.media`, `americanbanker.com`, `nbcnews.com`, `reuters.com`, `khan.co.kr`, `mbiz.heraldcorp.com`, `en.sedaily.com`, `techtimes.com`, `qz.com`, `thestar.com.my`, `en.wikipedia.org`, `unsplash.com`, `pexels.com`). Web search itself worked, so **every claim and date below rests on search-result summaries rather than on a publication date I read on the source page.** The brief asks for page-level date verification; I could not perform it. Treat the dates as reported-by-search, not confirmed.

Specific claims I could not confirm against a primary source:

- **The Woori Bank contrast** (designated tablets, digital certificate, biometric check; attack repelled). Reporting conflicts — some outlets say Woori repelled the attack with no data loss, at least one says Woori was breached. Flagged as disputed in the body, and deliberately not used as the article's load-bearing claim or headline. The *design pattern* argument stands independently; the *specific outcome* does not.
- **AI/agent attribution.** Officials suspect AI involvement and President Lee said AI "appears to have been used," but no published forensic finding ties a specific tool to execution. Credential stuffing remains an alternative explanation. The article states this uncertainty rather than resolving it.
- **The enumeration mechanics** (cycling randomized customer ID numbers, two-step chain through a second lookup service). Attributed to Herald Business reporting via search summary; the method is officially still under investigation and Shinhan and regulators have not confirmed the attack route.
- **Combined exposure above 68,000.** Attributed to an FSC figure cited by AFP via search summary. Outlet totals range from ~65,000 to ~68,000 and the per-firm numbers I found do not reconcile to either total. Per-bank figures also vary by outlet (KB Kookmin reported as both 99 and 119 customers; Shinhan as 25,000 and 25,727).
- **"At least seven" firms.** Counts and the specific list vary across outlets; Hyundai Capital is tied to this wave by some reporting and described as a separate earlier incident by others.
- **"All 79 savings banks have completed self-checks"** and **remediation running through November.** Attributed to Newspim via search summary; not independently confirmed.
- **Both candidate hero images.** Existence, URL validity and license could not be confirmed — see the Hero image section. Do not publish either without opening the page.

**Freshness note:** This incident began in late September 2026 and has developed continuously since. The items inside a 48-hour window as of 2026-10-08 are President Lee's October 6 statement on AI involvement, the sector-wide self-check results, and the FSC's updated exposure figure. The originating Shinhan disclosure (circa October 1) and the October 2–4 regulatory orders are older than 48 hours and are included as necessary background, not as fresh news.
