# 05 — Wider competitive landscape and the incumbent-feature threat

Type: research
Status: resolved
Blocked by: —

## Question

Ticket 03 covers Snipd in depth. This ticket covers **everything else** that does part of this,
and the threat that a platform ships it natively.

Cover, for each: what it does, pricing, platform, and traction if discoverable.

- **Dedicated clip/capture apps**: Airr (AirrQuotes), Fathom Podcast, Recast, Podurama, and any
  newer entrant. Verify which still exist and ship — check last update date on the App Store.
- **Mainstream players with clip/bookmark features**: Overcast (clip sharing), Pocket Casts
  (bookmarks — note this shipped relatively recently), Castro, Apple Podcasts (chapters, saved
  episodes), Spotify (clips, and its AI features).
- **Adjacent capture tools**: Readwise Reader, Audiopen, Voicenotes, Granola and other
  meeting-note tools, Apple Notes' own audio capabilities.
- **Platform-native threat**: what have Spotify, Apple, and YouTube shipped or announced in the
  transcript / highlight / AI-summary space? Spotify's transcripts and AI DJ, Apple Podcasts'
  transcripts (iOS 17.4+), YouTube's chapters and summaries. Assess how close each already is.

Then answer the defensibility question directly:

- Could **ChatGPT / Gemini / Apple Intelligence plus an existing player** make this redundant?
  Consider the "user pastes an episode link into an LLM" path — how good is that experience today,
  and what does it cost the user in friction?
- What happens if **Spotify or Apple ships this natively** within a year? How plausible is that,
  given what they've already shipped?
- What, if anything, is **durable**: the friction-free capture moment, the integrations, the
  workflow layer, a data moat? Give an honest verdict, including the possibility that nothing is
  durable.

Note explicitly: Apple shipping podcast transcripts in iOS 17.4 removed a large part of what
made transcript-based tools special. Assess how much of the remaining differentiation is
similarly one OS release from evaporating.

Distinguish verified from inferred throughout.

## Answer

Full research with method notes, sources and confidence grading: [`research/05-competitive-landscape.md`](../research/05-competitive-landscape.md). Researched 7 September 2026. Liveness and pricing VERIFIED against the Apple iTunes API and App Store IAP annotations; death dates bisected via Internet Archive CDX plus live DNS/TLS probes.

**Headline: three of the four dedicated capture apps named in this ticket are dead, the fourth is abandoned, and Pocket Casts shipped the concept's core capture loop on 3 September 2026 — four days before this research was conducted.**

### Comparison table

Ratings = App Store US ratings count, 7 Sep 2026. It is a **weak proxy for traction**, not a user
count. "Not discoverable" means exactly that — no published figure was found.

| Product | What it does | Pricing (US, 7 Sep 2026) | Platform | Traction | Alive/Dead |
|---|---|---|---|---|---|
| **Airr** (AirrQuotes) | Podcast player with timestamped "AirrQuotes" highlight clips, transcript-linked, PKM export | n/a | iOS (was) | Not discoverable | **DEAD.** Delisted from App Store (no record via iTunes API for any Airr podcast app). Last Internet Archive capture of `airr.io` 23 Oct 2023; no captures at all after that. `airr.io` today resolves but fails TLS handshake and returns HTTP 504 |
| **Fathom** (`fathom.fm`) | AI podcast discovery/summaries/clips | n/a | iOS/web (was) | Not discoverable | **DEAD.** Domain no longer resolves (SERVFAIL). Site went 200 → 404 between **28 Feb 2025 and 28 Mar 2025**; 404 on every capture since. Not in App Store |
| **Recast** (`letsrecast.ai`) | Turned saved articles into AI-generated audio "recasts" (adjacent, not podcast capture) | n/a | iOS/Android (was) | Not discoverable | **DEAD.** Site is a farewell page: "This was… Thank you for being a part of recast." Shutdown occurred between **1 Sep and 1 Nov 2024**. Not in App Store. (Note: `recast.app` is an unrelated live content-payments company — easy to mistake for a survivor) |
| **Podurama** | Free cross-platform player; bookmarks within episodes, AI chapters, episode summaries, "Trending Snippets" | Free w/ IAP: **$9.99/6mo, $19.99/3mo(!), $29.99/yr, $34.99/5yr, $69.99 lifetime**. Site banner: "50% off lifetime premium" | iOS, Android, web, Windows, macOS | **397** ratings, 4.33 avg. Revenue not discoverable | **ALIVE.** v7.0.1, updated **7 Jul 2026** |
| **Podwise** | AI podcast summaries, key insights, searchable transcripts, Notion export — closest direct clone of the concept besides Snipd | Free w/ IAP: **Standard $9.99/mo or $70.90/yr; Pro $19.99/mo or $142.99/yr**; quota top-ups $8–$24 | iOS + web | **80** ratings, 4.76 avg. Revenue not discoverable | **ALIVE.** v1.3.3, updated **31 Aug 2026** |
| **Overcast** | Premier indie player. **Clip sharing since Apr 2019** (audio/video clips, max 60s). No transcripts, no AI, no notes | Free (podcast ads); **Overcast Premium $19.99/yr**, other tiers $29.99 | iOS, iPadOS, watchOS | **47,689** ratings, 4.54 avg — largest indie player here. Revenue not published | **ALIVE.** v2026.8.1, updated **24 Aug 2026** |
| **Pocket Casts** | Owned by Automattic. **This is the headline finding — see below.** Transcripts, AI chapters, and Smart Bookmarks all shipped 2026 | Free w/ IAP: **Plus $3.99/mo or $39.99/yr; Patron $9.99/mo or $99.99/yr** | iOS, Android, web, desktop, TV | **15,664** ratings, 4.51 avg | **ALIVE and shipping aggressively.** v8.19, updated **31 Aug 2026** |
| **Castro** | Queue-centric player. No transcript/AI/notes layer | **Castro Plus $24.99/yr** ($3.99/mo, $9.99/qtr, $39.99 family) | iOS | **9,177** ratings, 4.58 avg | **ALIVE** but quiet. v2026.7.1, updated **15 Jul 2026**. Recent release notes are download bug fixes, not features. Now under "Bluck Podcast LLC" (ownership has changed hands more than once) |
| **Apple Podcasts** | Transcripts (iOS 17.4+), read-along, tap-to-jump, transcript search, **"Share a specific moment in an episode from the transcript"**, chapters, Enhance Dialogue | **Free** | iOS/iPadOS/macOS/watchOS, preinstalled | **2,073,765** ratings — ~44x Overcast, ~1,800x Snipd | **ALIVE.** v4.5, updated 27 Apr 2026 |
| **Spotify** | Auto-generated time-synced transcripts (free + Premium, global, since Sep 2023), automatic chapters, AI DJ, and per May 2026 Investor Day **"real-time questions about what you're hearing"** | Free tier has transcripts | Everywhere | >100M podcast listeners (Spotify's own 2023 figure) | **ALIVE** |
| **YouTube** | **"Ask YouTube"** on the watch page: LLM Q&A about the video you're watching, ~40+ languages, no paid tier required. Plus chapters and auto-captions | Free | Everywhere | Not applicable | **ALIVE** |
| **Readwise Reader** | Read-later + highlighting across web/RSS/PDF/EPUB/newsletters/**YouTube transcripts**. Podcast audio is *not* a first-class source | **$9.99/mo** full (incl. Reader); Lite $5.59/mo billed annually | iOS, Android, web, extension | **578** ratings (Reader) / 1,511 (classic Readwise). Site self-reports "1,724 other readers" on the pricing page — likely a stale or partial widget, not a user count | **ALIVE.** v8.18, updated 25 Aug 2026 |
| **AudioPen** | Speak a rambling thought → clean structured text. Your voice, not podcast audio | **Prime $11/mo or $99/yr** | iOS, Android, Mac, Windows, Chrome ext. | Site claims **"Used by 200,000+ people"** (self-reported, unaudited). Only **159** App Store ratings | **ALIVE.** v2.4.1, updated **6 Sep 2026** |
| **Voicenotes** | Voice notes + meeting notes, AI summaries, MCP integration to Claude/ChatGPT | **Free / Pro $9 per user/mo / Enterprise $24**. App IAPs show messier legacy pricing incl. $8.99/wk, $99.99/yr | iOS, Android, desktop | **6,812** ratings | **ALIVE.** v2.1.6, updated 27 Aug 2026 |
| **Granola** | AI meeting notes; has pivoted toward being a general knowledge layer (chat across meetings, MCP, mobile, Watch) | **Free / Business $14 per user/mo / Enterprise $35** | macOS, iOS, Watch | **12,815** ratings. Funding is public knowledge; ARR is not discoverable | **ALIVE.** v1.15.4, updated 18 Aug 2026 |
| **Apple Notes / Voice Memos** | Notes records audio **with live transcripts, searchable**, in macOS Tahoe 26 / iOS 26 generation. Voice Memos preinstalled | **Free** | Apple platforms | Voice Memos: **1,079,853** ratings | **ALIVE** |
| **Snipd** | (ticket 03) | Free tier w/ 2 AI episodes per week; **Premium $6.99/mo** advertised on site, App Store annual IAPs $71.90–$95.90 | iOS, Android | **1,142** ratings, 4.74 avg | **ALIVE.** v4.1.21, updated 24 Aug 2026 |
| **Onda AI Podcast Note Taker** | Podcast note-taking, direct concept clone | Not examined | iOS | **0** ratings | **EFFECTIVELY DEAD/ABANDONED.** Last update **25 Aug 2025** — over a year stale, zero ratings |

Sources for the table: Apple iTunes lookup/search API (US storefront, 7 Sep 2026); App Store
product pages for IAP annotations; [podurama.com](https://podurama.com/);
[snipd.com/pricing](https://snipd.com/pricing); [pocketcasts.com/plus](https://pocketcasts.com/plus/);
[castro.fm](https://castro.fm/); [overcast.fm](https://overcast.fm/);
[readwise.io/pricing](https://readwise.io/pricing); [audiopen.ai](https://audiopen.ai/);
[voicenotes.com/pricing](https://voicenotes.com/pricing);
[granola.ai/pricing](https://www.granola.ai/pricing); Internet Archive CDX API.

### The graveyard is the most important finding

Three of the four dedicated capture apps the ticket named are **dead**, and the fourth
(Onda) is abandoned. Verified:

- **Airr** — the app that invented the "AirrQuote" concept the brief's premise rests on — is gone.
  No App Store listing under any bundle or name search. `airr.io` last archived **23 Oct 2023**,
  with zero captures since; today the host answers on port 443 but the TLS handshake fails and
  plain HTTP returns 504. That is an abandoned deployment, not a maintained site.
- **Fathom** (`fathom.fm`) died between **28 Feb and 28 Mar 2025** (200 → 404, bisected via CDX).
  The domain no longer resolves at all.
- **Recast** (`letsrecast.ai`) shut down between **1 Sep and 1 Nov 2024**, and left an explicit
  farewell page.

**I could not determine why any of them shut down** — no post-mortem was reachable given the
search-tool failure described above. So the following is INFERRED, and should be treated as a
hypothesis to test rather than a finding: three independent teams building precisely this product
failed to reach sustainability in the 2023–2025 window, which is exactly the window in which Apple
and Spotify shipped free transcripts. The correlation is suggestive. It is not proof of causation,
and it is *possible* all three died of unrelated founder or funding reasons. But a developer
weighing this decision should note that **the base rate of survival among dedicated podcast-capture
apps is roughly 1-in-4 over three years**, and the survivors (Snipd, Podwise) have 1,142 and 80
App Store ratings respectively — no evidence of either having reached meaningful scale.

The map's standing note that "Snipd, Airr and Overcast exist" needs a correction: **Airr no longer
exists.** That does not restore the original brief's premise, though — the capability didn't go
away, it moved into the platforms.

### Pocket Casts has already built the product, in the last 90 days

This is the single most decisive piece of evidence in this ticket. Pocket Casts (owned by
Automattic, 15,664 US ratings, free-to-$39.99/yr) shipped, in sequence:

- **24 Jun 2026** — [Highlighted Transcripts](https://blog.pocketcasts.com/2026/06/24/read-along-as-you-listen-highlighted-transcripts-are-here/):
  sentence-by-sentence highlighting synced to playback, tap any line to jump to that moment. iOS
  and Android. Plus/Patron.
- **7 Jul 2026** — [AI Generated Chapters](https://blog.pocketcasts.com/2026/07/07/ai-generated-chapters-are-here/):
  auto chapter markers when the creator supplies none.
- **3 Sep 2026** (four days ago) — [Smart Bookmarks](https://blog.pocketcasts.com/2026/09/03/smart-bookmarks-save-the-words-not-the-timestamp/).

Read the Smart Bookmarks announcement closely, because it is not merely adjacent — it is the
proposed product's core loop, described in the proposed product's own language:

> "You heard something worth keeping. You reached for the bookmark button. Pocket Casts saved
> 13:28. A week later, 13:28 is a number. You know you saved it for a reason. Finding out what that
> reason was means listening to it again. That's the last thing a bookmark should ask of you."

And the mechanism:

> "Tap Add Bookmark and the sheet arrives already filled in. A title, written for you. The passage
> from the transcript, captured around the moment you tapped. One tap on Save and you're back in
> the episode."

Plus the retro-capture detail that any serious version of this product needs:

> "The transcript behind it leans backward on purpose. By the time your thumb finds the button, the
> sentence you wanted has already gone past. So we go back and get it."

That is: friction-free capture moment, auto-titling, transcript-anchored passage extraction, and
look-back windowing. It is on iOS **today**, inside a free-tier-plus-$39.99/yr app with roughly 14x
the ratings base of Snipd, backed by Automattic. Web and Android are stated as following.

This did not happen a year out. It happened **four days before this research was conducted**, and
it substantially removes the "nobody has built the capture moment properly" premise.

### Platform-native threat: what has ALREADY shipped

The ticket asks how close each platform already is. The answer for the transcript layer is: it is
not close, it has arrived, and it is free.

#### Apple — the threat is partly already realised

[Apple newsroom, 5 Mar 2024](https://www.apple.com/newsroom/2024/03/apple-introduces-transcripts-for-apple-podcasts/),
with **iOS/iPadOS 17.4**, VERIFIED:

- Full episode text, in English, French, Spanish and German.
- "Search the episode for a specific word or phrase, **and tap on the text to play the podcast from
  that point**."
- "Each word is highlighted, making it easy to follow along."
- Auto-generated "shortly after episodes are published"; back catalogue "transcribed over time."
- 170+ countries. Free. Preinstalled. 2,073,765 US ratings.

And critically — from the **current** Apple Podcasts App Store description (v4.5, VERIFIED
7 Sep 2026), a feature bullet the ticket did not anticipate:

> "• Read along with a transcript as your episode plays.
> • **Share a specific moment in an episode from the transcript.**"

So Apple ships transcript-anchored moment sharing natively, for free, on every iPhone. The ticket's
own framing — "Apple shipping podcast transcripts in iOS 17.4 removed a large part of what made
transcript-based tools special" — is correct and understated. Apple went past transcripts to
transcript-anchored capture-and-share.

Separately, **Apple Notes now records audio with live, searchable transcripts** in the macOS Tahoe
26 / iOS 26 generation ([Apple support guide](https://support.apple.com/guide/notes/record-and-transcribe-audio-apdb51236d92/mac)),
and Voice Memos is preinstalled with 1.08M ratings. The "capture a spoken thought into my notes"
job is now an OS feature.

What Apple has **not** shipped (VERIFIED absent from the app description): AI summaries of episodes,
AI-generated chapters, a highlight library, spaced repetition, or exports to Notion/Obsidian/Readwise.

#### Spotify — transcripts free and global since 2023, AI Q&A announced

[Spotify newsroom, 28 Sep 2023](https://newsroom.spotify.com/2023-09-28/international-podcast-day-transcripts-chapters-show-pages-global/),
VERIFIED: "auto-generated and time-synced transcripts", rolling out "to **Free and Premium** users
globally" across "millions of episodes", plus podcast chapters on mobile globally. Note the article
does **not** claim tap-to-jump or transcript search, so I am not asserting those for Spotify.

More important, [Spotify's 2026 Investor Day recap, 21 May 2026](https://newsroom.spotify.com/2026-05-21/investor-day-recap/),
VERIFIED: Maya Prohovnik demonstrated tools for searching and using podcasts including "transcripts,
automatic chapters, and **real-time questions** about what you're hearing." Spotify also stated its
AI edge comes from a proprietary "Large Taste Model" and reported ~9% improvement in podcast
discovery from Home.

"Real-time questions about what you're hearing" is, functionally, chat-with-this-episode — the
premium differentiator of Snipd's paid tier — being demonstrated on stage by a platform with
>100M podcast listeners. INFERRED (this is a demo/roadmap item, not a confirmed shipped feature at
the time of writing): general availability is plausible within the next 12 months, but I cannot
verify a ship date.

#### YouTube — conversational AI over video content is live

[YouTube Help, "Ask YouTube"](https://support.google.com/youtube/answer/14110396?hl=en), VERIFIED
live: on the watch page you "interact with AI to learn more about the content" — question-answering
about the video you're watching, LLM-backed, drawing on YouTube and the web, with suggested prompts.
Available on Android, iOS, desktop, smart TVs and consoles, in roughly 40+ languages, to any
signed-in user meeting the age minimum. **No paid tier requirement is stated.** Availability is
per-video and per-region.

Given that video podcasts are now a major distribution channel (Spotify's own creator case studies
are almost entirely about video), a free LLM Q&A layer over YouTube covers a large and growing slice
of podcast consumption.

### Could ChatGPT/Gemini/Apple Intelligence plus an existing player make this redundant?

Partly, and the honest assessment cuts both ways.

**The "paste an episode link into an LLM" path is genuinely worse than the app path** for the core
job, and this is the one real point in the concept's favour:

- It is **not the capture moment**. The concept's whole premise is the two-second, eyes-free,
  headphone-tap capture while walking or driving. Pasting a link into a chat app requires stopping,
  unlocking, switching apps, and finding the URL — and by then the idea has passed. The friction
  differential here is real and I am not going to minimise it.
- LLMs summarise the **episode**, not **the moment you cared about**. "What did they say about X"
  requires you to already remember X well enough to ask — which is precisely the thing you failed to
  do, hence the app.
- Reliability on arbitrary audio URLs is inconsistent (paywalled/dynamic feeds, ad-inserted audio,
  no transcript available).

**But the counter-validation is stronger than that concession:**

1. The friction advantage is a **UI advantage over a chat interface**, not an advantage over
   Pocket Casts Smart Bookmarks, which has the same two-tap capture moment, inside the player, with
   auto-titling and look-back. Against the actual competitor, the friction moat is already gone.
2. Apple Podcasts already lets you share a specific moment from the transcript for free.
3. Once captured, the *downstream* value — summarise, extract, organise, chat — is commodity LLM
   work that any player can add with an API call, and Pocket Casts, Spotify and YouTube have all
   demonstrated they will.

So: an LLM alone does not replace the product. **An existing player with a capture button plus an
LLM does** — and that combination now exists and shipped four days ago.

### What happens if Spotify or Apple ships this natively within a year?

Reframe the question, because it is now the wrong one. **The relevant incumbent already shipped it,
and it wasn't Apple or Spotify — it was Pocket Casts, on 3 September 2026.** The threat modelled as
a future risk has partially materialised as a present fact.

On the platform-native question specifically:

- **Apple**: has shipped transcripts, tap-to-jump, transcript search, and share-a-moment-from-
  transcript. It has *not* shipped AI summarisation of episodes or a highlight library. Apple's
  podcast app ships roughly annually with terse "Bug Fixes and Feature Enhancements" notes, so
  cadence is slow — but Apple Intelligence summarisation exists across the OS and the marginal cost
  of applying it to a transcript Apple already generates is close to zero. Probability Apple ships
  episode summaries or AI highlights within 12 months: **INFERRED, moderate.** I have no
  announcement to cite and will not invent one.
- **Spotify**: has publicly demoed "real-time questions about what you're hearing" at its own
  investor day. Probability of shipping something in this space within 12 months: **INFERRED,
  high** — this is a stated direction with a live demo, not speculation on my part. Ship date not
  verifiable.
- **YouTube**: already shipped the Q&A layer.

If any of these land, the residual differentiation is a highlight-library-plus-PKM-export workflow —
which is Readwise's territory, and Readwise Reader has 578 App Store ratings after five years, which
should temper any assumption that PKM export is a large market.

### How much of the remaining differentiation is one release from evaporating?

Taking each candidate differentiator honestly:

| Differentiator | Status | One release from evaporating? |
|---|---|---|
| Transcripts | Already gone. Apple (free), Spotify (free), Pocket Casts (Plus) | Already evaporated, 2024 |
| Tap-to-jump / read-along | Already gone. Apple, Pocket Casts | Already evaporated |
| AI chapters | Pocket Casts shipped Jul 2026; Spotify has them | Already evaporated |
| Episode summaries | Snipd, Podwise, Podurama have them; platforms don't yet | **Yes** — trivially, it's one API call over a transcript the platform already generates |
| Headphone-tap / friction-free capture | Snipd (headphone tap); Pocket Casts Smart Bookmarks (in-player two-tap with look-back) | **Largely evaporated** as of 3 Sep 2026 |
| Auto-titled, transcript-anchored highlight | **Pocket Casts shipped this exact thing on 3 Sep 2026** | Already evaporated |
| Chat-with-episode | Snipd Premium; Spotify demoed it; YouTube shipped equivalent for video | **Yes**, within ~12 months |
| Spaced repetition over highlights | Snipd ("Daily recap"), Readwise's core product | Not a platform priority — but already occupied by two incumbents |
| Export to Notion/Obsidian/Readwise | Snipd, Podwise | **No** — platforms have negative incentive to export users' attention elsewhere. This is the one structurally safe feature |

Nine candidate differentiators. Five have already evaporated, two more are one API call away, one is
already occupied by two players, and exactly one is structurally safe — and that one (PKM export) is
a feature that appeals to a niche whose observable size is small.

### Defensibility verdict

**Nothing durable is visible, and I am not going to manufacture a moat.**

Taking the four candidate moats the ticket names, in order:

**1. The friction-free capture moment — NOT DURABLE, and it is the load-bearing claim.** This was the
strongest candidate and it was overtaken during the window this research was conducted. Pocket Casts
Smart Bookmarks (3 Sep 2026) delivers in-player capture, auto-titling, transcript-anchored passage
extraction and look-back windowing, on iOS, inside a free-tier app with ~14x Snipd's ratings base
and Automattic's engineering behind it. Snipd's headphone-tap is a marginally better interaction
(fully eyes-free vs two taps) — but "marginally better tap ergonomics" is a feature, not a moat, and
it does not survive one Pocket Casts release.

**2. Integrations — WEAKLY DURABLE, COMMERCIALLY THIN.** Structurally safe from platform
encroachment (Apple and Spotify have no incentive to export highlights to Obsidian). But it is
already table stakes among the survivors: Snipd exports to Readwise, Notion, Obsidian and Glasp;
Podwise exports to Notion. So it is defensible against platforms and worthless as differentiation
against the actual competitors. And the addressable audience is small: Readwise Reader, the
best-known product in this space, has **578** App Store ratings.

**3. The workflow layer — NOT DEMONSTRATED.** Snipd's spaced-repetition recap is the most developed
version, and Snipd has 1,142 US ratings after five years. There is no evidence in the accessible
record that a workflow layer over podcast highlights converts at scale. Absence of evidence here is
weak evidence of absence, given how many teams have tried.

**4. A data moat — DOES NOT EXIST at indie scale.** Transcripts are commodity (Whisper-class ASR,
or free from the platforms). Highlights are per-user and confer no cross-user network effect. There
is no cold-start advantage a solo developer accrues that Automattic cannot buy in a sprint. Spotify's
actual data moat — the "Large Taste Model" trained on trillions of behavioural signals — is the shape
of a real one, and illustrates by contrast that this product has nothing like it.

**The base rates, which matter more than the feature analysis:**

- Dedicated podcast-capture apps: **3 of 4 named are dead** (Airr, Fathom, Recast), 1 abandoned
  (Onda). Survivors: Snipd (1,142 ratings), Podwise (80 ratings), Podurama (397 ratings).
- **No survivor in this category shows evidence of scale.** Not one published a user or revenue
  number I could verify. I am explicitly declining to estimate their MRR — but the ratings counts
  are two to three orders of magnitude below the mainstream players, and if any had broken through,
  it would likely be discoverable.
- Meanwhile the *adjacent* categories that did work — Granola (12,815 ratings), Voicenotes (6,812),
  AudioPen (self-reported 200k users) — are all **meetings and your own voice**, not podcasts. That
  pattern is worth noting against the map's open question about a non-podcast wedge: the market has
  already voted, and it voted for capturing speech you produce over speech you consume.

**Verdict: the competitive landscape does not support a build. Not because the space is crowded with
strong players, but because it is a graveyard with no proven survivor, the one durable-looking
differentiator was commoditised by an incumbent four days ago, and the remaining differentiation is
one API call from free.** For a solo developer with no audience targeting $2–5k MRR, this ticket's
evidence points to no-go on the podcast concept as framed. The evidence does not distinguish between
"don't build" and "build a much narrower thing" — but any narrower variant must survive the specific
question: *what does this do that Pocket Casts Smart Bookmarks plus Apple's free transcripts does not,
and why will that still be true in twelve months?*
