# 03 — Snipd teardown: what it does, its weak spots, and whether the market is saturated

Type: research
Status: resolved
Blocked by: —

## Question

Snipd is the closest incumbent and does approximately the proposed concept: AI-generated podcast
highlights, one-tap capture, and export to Readwise / Obsidian / Notion. The developer has **not**
used it and doesn't know it. This ticket exists to answer whether the idea is already built.

Answer specifically:

- **What Snipd actually ships today**: the capture interaction (how many taps, which surfaces,
  headphone-button support or not), what a "snip" contains (audio / transcript / AI summary),
  the AI features, and the export integrations. Be concrete about the capture *moment* — that's
  the proposed app's claimed wedge.
- **Pricing**: current tiers, what's free, what's paid, and the paid price point.
- **Platform coverage** and whether it plays Spotify-exclusive or YouTube content.
- **Traction, if discoverable**: App Store rating count and rating, funding, team size, any public
  user or revenue numbers, Reddit/HN mention volume over time. Say plainly if traction is not
  discoverable rather than guessing.
- **Weak spots — the core of this ticket.** Read App Store reviews (US and other stores), the
  Snipd subreddit if one exists, r/podcasts, r/ObsidianMD, r/PKM, and HN threads. Extract
  recurring complaints **verbatim with attribution**. Look specifically for: transcription
  accuracy, capture friction, sync reliability, price resistance, export fidelity, library
  migration pain, and whether users churn back to their old player.
- **Is the market saturated?** Assess whether the complaint pattern suggests (a) an unmet need a
  new entrant could serve, (b) a category users try and abandon because the underlying need is
  weaker than it looks, or (c) a solved problem with a satisfied user base. These have very
  different implications and the distinction matters more than any single feature gap.

Also cover, more briefly, whether **Airr**, **Fathom Podcast**, **Recast**, and **Podurama** still
exist and ship — several may be dead, and a graveyard of similar attempts is itself strong
evidence about demand.

Distinguish verified from inferred throughout. Quote users rather than paraphrasing them.

## Answer

Full research with inline sources: [`research/03-snipd-teardown.md`](../research/03-snipd-teardown.md)

**Headline: the brief's core premise is falsified. The capture moment is already solved, five ways,
free, by a live and actively-shipping incumbent.**

### Capture interaction (VERIFIED)

Snipd ships **five zero-look capture surfaces**, all in the **free** tier: headphone/AirPods
triple-tap; car steering-wheel back button; a **lock-screen widget** ("two buttons: one to create a
snip and one to view your snips library"); **Apple Shortcuts** (voice/automation); and native Apple
Watch / CarPlay / Android Auto. Post-tap: *"The podcast keeps playing, and your note gets saved in
the background"*, capturing *"typically the last 60 seconds you heard."* A snip = **audio +
transcript + AI summary**. Exports to Notion, Readwise, Obsidian, Glasp, Bear, Logseq, Markdown —
**also free**. RSS-only, so **no Spotify exclusives**; YouTube/audiobook **import** is Premium.
v4.1.21, updated 2026-08-24, shipping weekly. ASR is **in-house**, not a wrapped API.

### Pricing (VERIFIED today, 2026-09-07)

Free $0 (unlimited listening + headphone capture + watch/CarPlay + full PKM export; AI capped at
**2 episodes/week**). Premium headline **$6.99/mo** — but that is the annual rate: App Store IAPs
are **$11.90 monthly / $83.90 annual**, plus 900 min/month AI processing. Flat at $6.99 for
~20 months; trial *shortened* 2 weeks → 1 week; `Special Offer` SKUs at $42/$59.90 suggest
discount-to-close.

### Real weak spots (verbatim — full set in the research file)

1. **Boundary accuracy, not tap friction** — the most important finding.
   > *"Every time I take a snip, I have to adjust the start/end points a little bit anyways, so it
   > doesn't make sense for it to override a crucial AirPods feature when I most likely am going to
   > have to open the app anyway to adjust the snip."* — **whitneyelsworth**, US App Store
   > *"the snips don't always accurately capture the section you want"* — **Met Samuel**, Product Hunt
2. **Dynamic ad insertion breaks snip timing.** Conceded by the co-founder in 2022 (*"still a
   challenge for us... haven't found the time to tackle it yet"*) and **still being patched in
   v4.1.20/4.1.21, Aug 2026**.
3. **Corpus coverage tax** — unprocessed episodes burn the user's quota:
   > *"Every single podcast is not processed so you have to use your paid hours to process, which is
   > TWICE the price as whisper AI... Don't waste your time here because I have wasted mine to test.
   > Twice."* — **Sponge9999**, 1★
4. **Export/PKM fidelity** — richest vein, 15 open issues on Snipd's own Obsidian plugin, e.g.
   timestamps+playback links **regressed away** (**adamajane**, #16), AI Notes parity missing vs the
   Readwise path (**jaxley**, #13), silent zero-percent syncs (**aarontimo**, #7).
5. **Sync/data loss** — the only two 1★ reviews are reliability incidents: *"I have lost all my
   data, podcast queues and other info"* (**St. John 01**). Cross-device progress sync only shipped
   Feb 2026 — Snipd's own note: *"You can finally use Snipd across all your devices!"*
6. **No web/desktop** — most-repeated request, 5 independent sources 2022–2026.
7. **Not price resistance — the opposite.** *"Would be willing to pay double, maybe triple, for
   unlimited minutes."* (**cali_guy_0024**) and, from the free tier, *"I can't believe this is free...
   Please stay free forever 😅"* (**Owen Wallbridge**).

**Churn direction is against a new entrant**: users switch *into* Snipd from Overcast/Pocket Casts
and stay (swyx after 9 years on Overcast; Blake Robbins "fully converted"). The one churned-from app
is the dead predecessor: *"Snipd is everything I wanted AirrQuote to be."* (**BillSwag420**).

### Competitor liveness — a genuine graveyard (VERIFIED)

| | Status | Evidence |
|---|---|---|
| **Airr** | **DEAD** | App Store listing gone from all storefronts; page 404 by 2025-09; no Wayback capture after Nov 2023; site 504s |
| **Fathom** (`fathom.fm`) | **DEAD** | Domain **NXDOMAIN**; 404 from 2025-03 onward |
| **Recast** (`recast.fm`) | **EFFECTIVELY DEAD** | HTTPS times out; last (empty) capture 2025-08; `recast.app` now a payments company |
| **Podurama** | **ALIVE** but v7.0.1 (2026-07-07), 4.3★/397 — a *general* free player with bookmarks, **not** an AI-capture rival |

Also: Podwise alive but 80 ratings; Onda 13 months stale, 0 ratings; Anycast+, Steadcast, Scribbler,
PodText.ai all **0 HN points**. And a 2022 HN post proposing **almost exactly this map's narrow
companion-capture concept** (*"I don't want a whole new podcast player. I just want a better way to
take podcast notes"*) got **5 points and zero replies**; nobody built it in four years.

### Traction — and what is NOT discoverable

**VERIFIED:** 4.7★ / **1,142** US ratings; **$700k pre-seed** (Wingman Ventures, Acequia Capital,
2022); **team of five** in 2022; Zurich; Obsidian plugin **72,132** installs (vs Readwise 242,765);
Product Hunt 4.7/16 reviews.

**NOT DISCOVERABLE — stated plainly, not estimated:** revenue/MRR, paying-subscriber count,
conversion, churn, real user count (only unaudited *"hundreds of thousands"* marketing copy), any
post-2022 funding, current team size.

### Saturation verdict: predominantly (c), material (b), and (a) only where this map has ruled it out of scope

- **(c) Solved problem, satisfied base — dominant.** 4.7★; only two 1★ reviews, both reliability
  incidents not concept failures; complainants are **power users asking for more** (one logged
  **8,582 snips across 358 episodes** in 2025) — retention, not churn; price flat 20 months with
  weekly shipping; and the proposed wedge is free.
- **(b) Category users try and abandon — real, and it caps the market.** Three direct competitors
  dead in ~30 months. After 4.5 years the winner has **1,142 US ratings vs Overcast's 47,692 (~2.4%)**.
  As a user put it: *"most people listen to podcasts for fun and entertainment so it's unlikely
  they'll want to clip, get transcripts etc."* (lawtalkinghuman, HN). The niche is
  knowledge-listeners ∩ active-PKM — a subset of a subset, and Snipd has most of it.
- **(a) Unmet need — exists, but not reachable here.** The three durable gaps are **web/desktop**
  and **snip-boundary accuracy** — *both explicitly out of scope in `map.md`* — plus export
  templating, which is a backlog rather than a market.

**Implication for the go/no-go:** the claimed wedge does not exist; the only capture-adjacent wedge
that does (boundary detection) is the one the map ruled out, which is worth escalating. There is no
price umbrella (free covers capture+export; heavy users want to pay *more*). At $83.90/yr, $3k MRR
≈ **~430 paying subscribers** — not absurd arithmetically, but the funded five-person category
leader with Ali Abdaal and swyx endorsements has 1,142 total US ratings after 4.5 years, and its
revenue is unknowable from outside. **Leaning strongly negative — but flagging honestly that the
funnel is unquantifiable from public evidence, and that Reddit was inaccessible, so the one thing
that could move this verdict (a cohort of churned-out ex-Snipd users) has not been checked.**
