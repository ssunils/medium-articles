# Design

**Subtitle:** Anthropic's S-1 shows a vendor locked into compute it must pay for either way, selling to customers who can walk. That gap is about to become your negotiation.

**Target reader:** A B2B SaaS PM at a 50–500 person company who owns the cost line on a shipped AI feature and is heading into a vendor renewal or a 2027 commitment conversation.

**Key takeaway:** Your model vendor has non-cancelable costs and cancelable revenue, so your ability to reduce usage or leave is a real asset — decide now whether to sell it for a committed-spend discount or hold it, because the vendor's filing says it needs you to sell it.

**Section outline:**
1. Hook: two sentences sitting next to each other in a risk-factors section
2. What the filing actually says on each side of the ledger
3. Why an asymmetry like this does not stay where it is
4. You are the uncommitted revenue
5. What your optionality is plausibly worth
6. The honest case for committing anyway
7. What a public vendor gives you that a private one didn't
8. Practical takeaway
9. What the filing does not establish

**Headline options:**

1. **Your AI Vendor Owes $750 Billion. You Can Leave Anytime.** — *RECOMMENDED*. Hook type: specific number plus stakes framing. It sets up the exact asymmetry the article is about, and the filing's own take-or-pay language and customer-termination language pay it off directly. No overstatement: both halves are in the document.
2. **The Flexibility You Never Priced Is Your Best Leverage Right Now** — Hook type: contrarian claim challenging a common PM belief (that month-to-month usage is just a default, not an asset).
3. **What Would Two Years of Committed Token Spend Buy You?** — Hook type: sharp question most PMs cannot answer confidently, since almost nobody has priced their own optionality.

---

# Draft

## Your AI Vendor Owes $750 Billion. You Can Leave Anytime.

On Monday, Anthropic [filed an S-1 with the SEC](https://www.anthropic.com/news) for a proposed public offering. Somewhere in the risk factors, two facts sit near each other that should interest you more than the revenue line.

The first: the company has signed long-term compute agreements with "minimum purchase commitments, take-or-pay provisions" that [obligate it to pay for resources regardless of actual utilization](https://www.thestack.technology/anthropic-s-1-shows-it-is-at-the-hyperscalers-mercy/).

The second: much of its own revenue carries no equivalent commitment, with [contracts that let customers reduce usage or terminate with limited or no notice](https://fortune.com/2026/10/26/anthropics-s-1-makes-clear-its-on-the-hook-for-billions-in-compute-its-customers-can-walk-at-any-time-2/).

Fixed costs. Floating revenue. And you are standing on the floating side.

## The two sides of the ledger

The cost side is large. Reporting on the filing puts cloud compute commitments at roughly $475 billion, rising to [as much as $750 billion once chip-leasing deals are counted](https://dealroom.co/news/164610-anthropics-draft-s-1-reveals-16-3b-revenue-80-7b-loss-and-up-to-750b-com/). One analysis of the contract terms notes the AWS agreement is non-cancelable except on Amazon's uncured material breach, and that a Broadcom lease runs to [about $125 billion in rent over five years on similar terms](https://nodiligence.substack.com/p/anthropic-has-to-pay-its-suppliers).

The revenue side is growing fast and is also, structurally, loose. First-half 2026 revenue came in around [$16.3 billion](https://www.investing.com/news/stock-market-news/anthropic-revenue-hits-163-billion-as-preliminary-s1-outlines-ipo-risks--wsj-4960928), against a first-half net loss of $80.7 billion that at least one analyst attributes largely to a non-cash accounting charge. Reporting on the filing also describes meaningful customer concentration, with [the two largest customers at roughly 20% of first-half revenue](https://seekingalpha.com/news/4654922-anthropics-draft-s-1-filing-shows-revenue-growth-customer-concentration-risks-report).

I want to be careful here, because this is the part that gets overstated. None of that means the company is in trouble. Take-or-pay compute is how you get capacity at all, and a vendor growing at this rate has reasons to buy ahead of demand. The filing is not a distress signal.

It is something more useful to a PM: a description of an incentive.

## Asymmetries like this don't stay put

If your costs are locked and your revenue isn't, you have exactly one structural problem, and you will work on it. Not with a price increase — that pushes customers toward the exit you just disclosed. You work on it by making commitment attractive.

That looks like committed-spend discounts, multi-year agreements with volume floors, credits that expire, enterprise tiers priced below list in exchange for a minimum, reserved throughput. None of it is punitive. Most of it is a genuinely good deal for someone. The point is that the pressure to offer it is now written down in a public document, and it applies to every vendor with the same shape — which, given how compute is bought, is most of them.

So the question in your next renewal is not whether you will be offered a commitment. It is whether you have decided what yours is worth before someone else prices it for you.

## You are the uncommitted revenue

Here is the uncomfortable translation. When the filing says customers can reduce usage or leave with little notice, that is describing your contract. Your month-to-month, consumption-based, no-floor arrangement — the one you probably think of as the absence of a decision — is an asset the vendor's own disclosure identifies as a risk to them.

Most PMs have never priced it. We treat flexibility as free because it arrived by default. It isn't free; it just hasn't been traded yet.

And it's worth more right now than it will be later. Optionality is worth most to a counterparty who has just told the market they need it.

> Your ability to walk away is a line item. You have simply never put a number on it.

## What it's plausibly worth

I can't tell you the discount, and I'd distrust anyone who quotes one — enterprise AI terms aren't public and vary enormously. What I can tell you is how to find your own number, because the inputs are all things you already have.

Start with the spread between what you pay at list and what a committed tier would cost. Then estimate the probability you'd actually want to move within the commitment term. That second number is the one PMs get wrong, usually by assuming they're more mobile than they are. If you've built evaluations against one model family, tuned prompts to its behaviour, and shipped features whose output quality your customers now expect, your real switching window is longer than your contract's.

If you are honestly unlikely to move inside two years, you are holding an option you will never exercise. Sell it.

If you have a live second-vendor plan, a routing layer, or a model-agnostic evaluation harness, your option has teeth. Price it accordingly, and consider holding.

## The case for committing anyway

There's a version of this where the flexible choice is the wrong one, and it deserves saying plainly.

A usage floor you comfortably clear converts a variable cost into a predictable one, which is worth something real if you are trying to quote a gross margin to a board. Commitment also tends to come with things that aren't money: capacity guarantees, rate limits that match your peak, roadmap visibility, a named contact when something breaks at 2am. For a team shipping an AI feature into a growing customer base, predictable capacity can matter more than the discount.

What you should not do is commit to a volume you reached by extrapolating a trend line. Floors are only cheap when you clear them.

## What a public vendor gives you

One underrated consequence of this filing: a vendor subject to SEC disclosure has to keep telling you things. Quarterly results, a risk-factor section that gets updated, a margin trend you can read. Private vendors gave you a pricing page and a sales call.

That's a planning input you didn't have before. If compute cost per dollar of revenue is improving — and reporting on the filing suggests it has improved sharply — you can expect that to eventually reach pricing. If concentration or commitment risk grows, you can expect commercial terms to tighten. You get to see the pressure before it arrives in your renewal email.

Use it. Put the earnings date in the same calendar as your renewal date.

## Practical takeaway

Four things worth doing in the next two weeks:

1. **Find your real switching window.** Not the contract notice period — the engineering estimate. How long to move your highest-volume feature to a second vendor with quality your customers wouldn't notice? That number is your option's maturity.
2. **Price the option.** Get a committed-spend quote at your current volume, even if you have no intention of signing. You cannot evaluate flexibility without knowing what it costs.
3. **Separate your volumes.** Split predictable baseline usage from spiky or experimental usage. Commit the baseline if the discount is real; keep the spiky part flexible. Most teams negotiate one blended number and lose on both halves.
4. **Diarise the disclosure.** Note the vendor's reporting dates and read the risk factors when they change. Terms follow pressure, and now you can see the pressure.

None of this requires a view on whether the IPO is a good investment. It only requires noticing that your vendor just published its incentives, and that you are on the other side of them.

---

# Hero image

**I could not verify any real, free-to-use image for this article.** The environment's network policy denied access to unsplash.com, pexels.com, openverse.org and commons.wikimedia.org, so I was unable to confirm that any candidate image exists, is genuinely free for commercial use, or carries the license I would be claiming. Rather than present an unverified or guessed URL, here is the fallback description.

**Primary candidate: none verified.**
**Backup candidate: none verified.**

**Ideal cover image (fallback description):** A tight, editorial still-life shot of an unbalanced mechanical scale or two-pan balance on a plain desk, photographed from slightly above in cool neutral light — one pan weighted down with something solid and dense, the other holding almost nothing. Shallow depth of field, muted palette of greys and a single warm accent, lots of negative space on the right for Medium's title overlay. It reads as asymmetry and obligation rather than technology, and it avoids the robot-and-android cliché entirely. A workable alternative in the same register: an overhead shot of a long printed contract with one paragraph highlighted, shot at an angle so the text is legible as texture but not readable as content.

To source this once network access allows, search Unsplash or Pexels for "unbalanced scale", "brass balance scale desk", or "contract paperwork overhead" and confirm the license on the image's own page before use.

---

# Metadata

**Medium tags:** Product Management, Artificial Intelligence, SaaS, Vendor Management, Startup Strategy

---

## Unverified claims

Primary-source verification was limited this run: the environment's network policy denied direct page access to sec.gov, fortune.com, cnbc.com, finance.yahoo.com, betanews.com and every image host I tried. Only anthropic.com was reachable. So the filing's existence and date are confirmed against the primary source, but the figures inside it are confirmed only against press summaries, not the document itself.

- **Confirmed against a primary source:** Anthropic filed an S-1 with the SEC for a proposed IPO on October 26, 2026. This appears as a dated post on [anthropic.com/news](https://www.anthropic.com/news), which I retrieved directly.
- **Could not open the S-1 itself.** Every quoted figure and every piece of quoted filing language below comes from press and analyst summaries, not from my own read of the document. sec.gov was blocked by the network policy.
- **Compute commitment totals are inconsistent across sources.** I saw roughly $475 billion for cloud compute, up to $750 billion including chip leases, a separate report of roughly $450 billion over a decade, and another citing about 80% of $518 billion as non-cancelable. These do not reconcile, and I could not determine which reflects the filed document.
- **Customer concentration conflicts.** Coverage puts the two largest customers at roughly 20% of first-half 2026 revenue and 24% of 2025 revenue, while at least one summary reports the filing saying no single customer exceeded 10% of revenue for the nine months ended September 30. I could not resolve this.
- **Draft versus filed document.** Some coverage I relied on describes a *draft* S-1 reported before Monday's public filing. Figures from draft coverage may not match the filed version. I have not verified which is which for every number.
- **The $80.7 billion first-half net loss**, and the characterisation of it as largely a non-cash accounting charge, come from secondary reporting and one analyst's reading. Unverified.
- **The revenue mix** (roughly 80% consumption-based, 20% subscription) appeared in one set of search results and could not be corroborated in a second search; one source suggested the 80% figure may be a conflation with an unrelated 81% decline in compute expense per dollar of revenue. I have therefore kept it out of the article body.
- **Broadcom lease terms** (~$125 billion over five years, non-cancelable except on default) and the AWS non-cancelability clause come from a single Substack analysis. Unverified.
- **"Compute cost per dollar of revenue has improved sharply"** — I reference this directionally in the article. It rests on a single reported figure (an 81% decline from Q1 2025 to Q2 2026) that I could not verify.
- **No image license could be confirmed.** No hero image is presented, by design, for the reasons given above.
- **My forward-looking argument is an argument, not a finding.** The claim that vendors will respond to this asymmetry by pushing commitment terms toward customers is my inference from the disclosed incentive structure. The filing does not say this, and no vendor has announced it.
