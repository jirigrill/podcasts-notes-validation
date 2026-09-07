# 03 — Snipd teardown: what it ships, its weak spots, and whether the market is saturated

Research date: **2026-09-07**. Ticket: `issues/03-snipd-teardown.md`.

Every claim below is tagged **[VERIFIED]** (read directly from a primary source today, quoted)
or **[INFERRED]** (my reasoning from the evidence). Where evidence does not exist, this file
says so explicitly rather than estimating.

## Methodological caveat — read this first

Reddit was **not accessible** during this research. `reddit.com`, `old.reddit.com`,
`api.reddit.com`, every Redlib/Libreddit mirror tried, and the PullPush archive API all
returned 403 / 429 / bot-walls. General web search (Google, Bing, DuckDuckGo, Brave, Startpage,
Ecosia, Mojeek, ~10 SearXNG instances) was also blocked or returned unrelated results.

Consequence: **the ticket's request for r/podcasts, r/ObsidianMD, r/PKM and r/Zettelkasten
quotes could not be fulfilled.** I have not substituted paraphrase or invention for those
quotes. What I did get instead — and it is arguably better evidence — is:

- Apple App Store reviews, verbatim, from the US and AU storefronts (29 AU reviews retrieved
  via the iTunes RSS feed; 4 US reviews visible on the store page).
- **26 GitHub issues on Snipd's own official Obsidian plugin**, which are power-user PKM
  complaints written in the exact voice the ticket wanted, with names and permalinks.
- Hacker News comment corpus (65 hits mentioning Snipd), full-text, with permalinks.
- Product Hunt reviews (16 total, 4.7 average).
- Snipd's own pricing/feature pages, plus Wayback snapshots to check price drift.

Also note: **US App Store review counts are a hard ceiling on quote volume.** Snipd has 1,142
US ratings but Apple exposes only a handful of review bodies publicly, and the RSS review feed
is deprecated for most storefronts (US/GB/CA/DE all returned empty feeds; only AU, BR and JP
still served data). So the negative-review sample is small — roughly 30 usable reviews — and
skews positive because Apple surfaces "most helpful" first. **Do not read the absence of
complaints as absence of problems; read it as a thin sample.**

---

## 1. What Snipd actually ships today

**[VERIFIED]** App: [Snipd | AI Podcast Player](https://apps.apple.com/us/app/snipd-ai-podcast-player/id1557206126),
seller **Snipd AG** (Zurich). Version **4.1.21**, last updated **2026-08-24**. iOS 15+,
201 MB, Productivity category, English only, 13+. Also ships watchOS (10.4+) and visionOS
builds. Rating **4.7 from 1,142 US ratings**.

Shipping cadence is healthy: from the version history on the store page, roughly **weekly to
biweekly releases** through 2026 (4.1.3 in Mar → 4.1.21 in Aug). This is not a coasting product.

### The capture moment — the proposed app's claimed wedge

This is where the ticket's premise is most directly at risk, so it is worth being precise.
**[VERIFIED]** from [snipd.com](https://www.snipd.com/) and
[the how-to-take-notes post](https://www.snipd.com/blog/how-to-take-notes-from-podcasts-with-snipd):

Snipd ships **five** separate zero-look capture surfaces:

| Surface | Trigger | Source |
|---|---|---|
| Headphones / AirPods | **Triple-tap** | "Triple-tap your headphones to save key moments with transcript and summary." ([homepage](https://www.snipd.com/)) |
| Car | Steering-wheel back button | "you triple-tap your headphones or press your steering wheel's back button" ([blog](https://www.snipd.com/blog/how-to-take-notes-from-podcasts-with-snipd)) |
| Lock screen | Widget button | "a small widget appears on your lockscreen with two buttons: one to create a snip and one to view your snips library" ([blog](https://www.snipd.com/blog/skip-intro-outro-lockscreen-widget-apple-shortcuts-release)) |
| Siri / automation | Apple Shortcuts | Snipd "now integrates with Apple's Shortcuts app, enabling voice commands and custom automations" ([same post](https://www.snipd.com/blog/skip-intro-outro-lockscreen-widget-apple-shortcuts-release)) |
| Apple Watch / CarPlay / Android Auto | Native app | Listed as a **free-tier** feature in the [pricing comparison table](https://www.snipd.com/pricing) |

Post-tap behaviour, **[VERIFIED]** quoting the blog: "The app automatically captures the audio
clip and transcript of that moment (a 'snip')." — "The podcast keeps playing, and your note gets
saved in the background." The captured window is retrospective: "typically the last 60 seconds
you heard."

A snip contains three things, **[VERIFIED]** from the homepage: "Our AI creates a snip for you
with **audio, transcript, and summary**."

**[INFERRED] — and this is the single most important finding for the go/no-go:** the capture
interaction the proposed app names as its wedge is **already shipped, on five surfaces, and is
free**. "One tap, no looking at the phone" is not a gap. It is table stakes in the incumbent's
free tier. Any wedge claim must be built on something other than the existence of low-friction
capture.

### AI features **[VERIFIED]** (homepage feature list)

Transcripts with speaker identification; AI auto-chapters; custom AI prompts ("Customize how AI
captures your insights with tailored prompts and durations"); mentioned-books extraction; guest
bios and cross-appearance discovery; shareable quote cards; **26-language** AI support; "Chat
with Podcasts" ("Like ChatGPT for your podcasts"); pre-play Mini Summaries; and an "AI DJ"
(added v4.1.4, Mar 2026) that per [the release post](https://www.snipd.com/blog/ai-dj-listen-to-best-parts-of-any-podcast)
plays "the best parts of any podcast in 25% of the time."

Notably **[VERIFIED]** the transcription is in-house, not a wrapped API. Co-founder Ferdinand on
HN in 2022: *"We don't use any paid APIs for the AI. Everything is in-house ;)"*
— [ferdinand_snipd, HN](https://news.ycombinator.com/item?id=30454639)

### Export integrations **[VERIFIED]**

"Notion, Readwise, Obsidian, Glasp, Bear, Logseq, or export as Markdown" (homepage). Sync/export
is a **free-tier** feature per the pricing table, as is the spaced-repetition "Daily recap."
An **official first-party Obsidian plugin** exists: [snipd-app/snipd-obsidian](https://github.com/snipd-app/snipd-obsidian)
(created 2025-10-16, 52 stars, last pushed 2026-05-14).

### Platform coverage **[VERIFIED]**

RSS-based. Co-founder Kevin Smith, addressing copyright on HN: *"Just like all other podcast
apps, we are relying on the RSS feed system and are not streaming any audio from our own
servers. The podcasts are streamed directly from the podcast hosters via the URLs provided by
podcasters in their RSS feeds."* — [KevinBenSmith, HN](https://news.ycombinator.com/item?id=30454639)

- **Spotify exclusives: NO.** Not supported and not claimed anywhere. RSS-only architecture
  precludes it. **[INFERRED from the RSS architecture — Snipd never addresses Spotify directly.]**
- **YouTube: YES, but as import, not playback.** "Import YouTube Videos" is a **Premium-only**
  feature.
- **Audiobooks: YES** — Libro.fm import (v3.6.84) plus arbitrary audio-file upload (Premium).
- **Private/Patreon RSS feeds: still a gap as of the last evidence I have.** Requested on HN in
  2022 by *agentdrtran* ("any word on snipping coming to private RSS feeds? all of my most
  listened to pods are private"); Kevin replied "We don't have a clear date yet." An AU reviewer
  still wanted it: *"The only feature I would request is the ability to have transcripts from
  private podcasts — then this would be perfect."* (Cael Mitchell, 5★, v2.0.18).
  **[Not verified as still missing in 4.1.21 — I could not test the app.]**

---

## 2. Pricing — current as of 2026-09-07

**[VERIFIED]** from [snipd.com/pricing](https://www.snipd.com/pricing) fetched today, cross-checked
against the App Store IAP list.

**Free — $0/month.** The page's own boast: *"More features than most premium apps."*
- Unlimited listening to all podcasts; unlimited core features
- **Create snips with headphones** — free
- **CarPlay, Android Auto & Apple Watch** — free
- **Export & sync snips to Readwise, Notion, Obsidian, Glasp & more** — free
- Auto/smart downloads; spaced-repetition Daily recap — free
- AI features capped at **2 episodes per week** (AI snips, transcript w/ speakers, chapters,
  episode summary, mentioned books, shareable quotes)

**Premium — $6.99/month equivalent**, "Most Popular", "Includes 1 week free trial."
- Unlimited AI features across "1M+ processed episodes"
- Chat with episode; import audio files & YouTube; custom AI prompts
- **AI processing quota: 900 min/month** for episodes not already in the processed corpus

**Actual charged amounts [VERIFIED]** from the App Store in-app-purchase list:
**$11.90 monthly** and **$83.90 annual**. $83.90 ÷ 12 = **$6.99/mo** — so the headline $6.99 is
the *annual-billed* rate, and month-to-month is $11.90. A Jan-2025 Wayback snapshot of the
pricing page stated this explicitly: *"Billed annually at $83.90"*
([archived 2025-01-15](https://web.archive.org/web/20250115093931/https://www.snipd.com/pricing)).
The live 2026 page has **dropped** that disclosure, showing only "$6.99/month".

Also present in the IAP list: `Snipd Premium (Special Offer)` at **$42.00** and **$59.90**, and a
`$95.90` tier. **[INFERRED]** the $42 SKUs are discounted/win-back annual offers — Snipd is
discounting to close, which is a mild price-resistance signal.

**Price stability [VERIFIED]:** $6.99/month appears in Wayback snapshots from Jan 2025 through
Aug 2026. **The price has not moved in ~20 months.** The free trial did shorten from
**2 weeks → 1 week** between the Jan-2025 snapshot and today. **[INFERRED]** shortening a trial
is usually a conversion-optimisation or cost-control move, not a sign of pricing power.

Caveat the page states itself: *"Prices may vary by country. For exact pricing, please check the
App Store in your region."* A student discount FAQ entry exists but its answer did not render.

**Extra AI minutes are now purchasable** — version 4.1.13 (May 2026) release note: *"Allow to
purchase extra AI minutes."* **[INFERRED]** the 900-minute cap was binding often enough that
Snipd built a paid escape valve for it, ~4 years in.

---

## 3. Traction — what is and is not discoverable

### VERIFIED

| Metric | Value | Source |
|---|---|---|
| US App Store rating | **4.7** from **1,142 ratings** | [App Store](https://apps.apple.com/us/app/snipd-ai-podcast-player/id1557206126) (embedded JSON-LD `aggregateRating`) |
| Funding | **$700,000 pre-seed**, "over-subscribed" | [TechCrunch, 2022-08-16](https://techcrunch.com/2022/08/16/how-snipd-is-using-ai-to-unlock-knowledge-in-podcasts/) |
| Investors | **Wingman Ventures**, **Acequia Capital** | same |
| Team size (2022) | **"a team of five, including three co-founders and two employees"** | same |
| HQ | Zurich, Switzerland (Snipd AG) | App Store seller record + TechCrunch |
| Obsidian plugin installs | **72,132** for `snipd-official` | [community-plugin-stats.json](https://github.com/obsidianmd/obsidian-releases/blob/master/community-plugin-stats.json) |
| Product Hunt | 4.7 from **16 reviews**; 3 launches (Feb 2022, Oct 2022, Jun 2023), both 2022 launches "#4 of the day" | [Product Hunt](https://www.producthunt.com/products/snipd) |
| Founder-stated scale | *"Loved by hundreds of thousands of podcast listeners"* | [snipd.com/pricing](https://www.snipd.com/pricing) — **marketing copy, unaudited** |

**One useful scale anchor [VERIFIED]:** the Snipd Obsidian plugin has **72,132 installs**; the
Readwise official Obsidian plugin has **242,765**. So Snipd's Obsidian-using cohort is roughly
**30% the size of Readwise's** in the same ecosystem. For further context, the top Obsidian
plugins are in the millions (Excalidraw 7.8M, Templater 5.5M). **[INFERRED]** Snipd is a real but
niche product within PKM — visible, not dominant.

Also note the marketing-copy drift **[VERIFIED]**: the Jan-2025 pricing page said *"Loved by
thousands of podcast listeners"*; today's says *"hundreds of thousands."* Growth or looser
copywriting — unresolvable from outside.

### NOT DISCOVERABLE — stated plainly

I could not find, and am **not** estimating:

- **MRR, ARR, or revenue of any kind.** No number exists publicly.
- **Paid-subscriber count or free→paid conversion rate.** Nothing.
- **Total user count.** The only figure is Snipd's own unaudited "hundreds of thousands," which
  is almost certainly *registered accounts / downloads*, not paying subscribers, and should not
  be used in any arithmetic.
- **Any funding after the 2022 $700k pre-seed.** TechCrunch said a seed was planned "in the
  not-too-distant future"; I found no announcement of one in four years. This is **absence of
  evidence, not evidence of absence** — but for a 2022 pre-seed AI company in a hot category, no
  publicly visible seed round in four years is at least worth noting.
- **Current team size.** The only figure is "five" from 2022.
- **Churn / retention.** Nothing.
- **Reddit/HN mention volume over time.** The HN Algolia year-bucketed count queries failed, and
  Reddit was inaccessible. What I can say **[VERIFIED]** from the 65-hit HN comment corpus is
  qualitative: Snipd mentions cluster in **2022–2024** and are notably **sparse in 2025–2026**
  (only ~4 substantive mentions in the last 20 months). **[INFERRED]** this is consistent with a
  product past its novelty-buzz peak, but the sample is far too small to call it a trend.

---

## 4. Weak spots — verbatim, with attribution

The complaints cluster into seven themes. I have ordered them by how load-bearing they are for
the proposed app's thesis.

### 4.1 Capture accuracy — snips grab the wrong window

This matters most, because it is a defect **in the exact interaction the proposed app claims as
its wedge**. Note carefully: the complaint is *not* "capture is too much friction." It is
"one-tap capture fires fine but selects the wrong audio, so I have to open the app and fix it" —
which reintroduces the friction from the other end.

> "the snips don't always accurately capture the section you want"

— **Met Samuel**, Product Hunt review, ~1 year ago
([producthunt.com/products/snipd/reviews](https://www.producthunt.com/products/snipd/reviews)).
He adds that out-of-sync transcripts make it worse, that adjusting start/end points is tedious,
that automatic snips create clutter for deliberate listeners, and that a web version is badly
needed.

The most valuable quote in this entire teardown, because it names the failure mode precisely:

> "Every time I take a snip, I have to adjust the start/end points a little bit anyways, so it
> doesn't make sense for it to override a crucial AirPods feature when I most likely am going to
> have to open the app anyway to adjust the snip."

— **whitneyelsworth**, US App Store, 03/21/2022
([App Store](https://apps.apple.com/us/app/snipd-ai-podcast-player/id1557206126))

Read that again. A user reports that the one-tap capture is followed, *every time*, by opening
the app to fix the boundaries. **[INFERRED]** If that is representative, the real unsolved problem
is not the tap — it is **boundary detection**. And note the map explicitly rules "smart
boundaries" out of scope for this effort as a v2 feature. This evidence suggests boundaries may
be the *only* defensible v1 wedge, which would force the map's scope to be revisited.

Related, from the same reviewer — headphone-gesture collision, a real cost of the
triple-tap design:

> "the fact that the normal skip-back, triple-click behavior on AirPods has been overridden with
> the snip feature and with no option to change it is a complete deal breaker for me. I simply
> cannot go without the ability to replay the last 15 seconds of a podcast from my headphones."

— **whitneyelsworth**, same review. (Snipd fixed this; she later prepended *"Update: They just
released an update that fixed all of the issues I had with with it. It's now the best podcast app
in the market."* — so treat it as a **solved** problem, and as evidence the team is responsive.)

A subtler capture complaint — the AI-suggested boundaries actively disorient:

> "Also, the highlighted snip is a little disorienting. Would really just like to highlight the
> current sentence I'm in and set the start/end markers myself."

— **_brontus**, 5★, AU App Store, v2.2.48

### 4.2 Dynamic ad insertion breaks snip timing

**[VERIFIED]** as a real, acknowledged, still-live problem.

> "A few podcasts use dynamic ads and it messes up the snipping but I've really only found one I
> listen to regularly that does that - On Purpose with Jay Shetty."

— **Kate Que**, 5★, US App Store, 03/24/2024

Snipd conceded it four years ago. Co-founder Kevin Smith on HN, asked about dynamic ad insertion
shifting all timestamps per-user:

> "Dynamic ad insertion is also still a challenge for us. We'd like to develop a technical
> solution for it but haven't found the time to tackle it yet."

— [KevinBenSmith, HN, 2022-02-24](https://news.ycombinator.com/item?id=30454639)

They have since worked on it — the blog claims a method that "syncs transcripts to the audio even
when podcasts insert dynamic ads", and v4.1.20 (Aug 2026) fixes "snip manual edit start & end not
correct in episode with dynamic content", and v4.1.21 fixes false "Transcript might be out of
sync" warnings. **[INFERRED]** they are still shipping fixes for it in the most recent release,
i.e. **not fully solved after four years**. This is a genuinely hard technical moat problem, and
it is a *harder* problem for a new entrant with less corpus and no in-house ASR.

Third-party corroboration that this is Snipd's distinctive technical asset — a HN commenter
recommending Snipd's approach be studied:

> "slightly tangential but the podcast app Snipd has a lot of text to speach re-sync alignment to
> recover from inserted advertisements so it might be worth exploring if they have published any
> details"

— [jimmySixDOF, HN, 2026-08-31](https://news.ycombinator.com/item?id=49507782)

### 4.3 Corpus coverage — the "unprocessed episode" tax

This is the most structurally interesting complaint, because it is a **consequence of the
business model** rather than a bug, and it would hit a new entrant *far harder*.

Snipd's AI works instantly only on its pre-processed corpus ("1M+ processed episodes"). Anything
outside it burns the user's 900-minute monthly quota. The pricing page admits the selection
criterion: *"We automatically process the most popular shows on Snipd."*

> "And a few have not been run for AI so you have to use the allotted number of minutes per month
> they give you to run AI on an episode you want to snip. But again, only one podcast I've
> encountered that I listen to regularly on that issue - The Trent Shelton Podcast. Snip'd! - run
> AI on all the Trent Shelton's podcast episodes, please!"

— **Kate Que**, 5★, US App Store, 03/24/2024

The harshest review found anywhere, and it attacks exactly this — plus the unit economics:

> "Back to the AI feature and the community curated snips: they are nearly unusable. Every single
> podcast is not processed so you have to use your paid hours to process, which is TWICE the price
> as whisper AI if you know how to invoke it from API. The taste of so called groups are just so
> philistine that you won't want to listen to their snips if you value your time and brain so
> much that you use AI to process more knowledge. Don't waste your time here because I have wasted
> mine to test. Twice."

— **Sponge9999**, 1★, "Totally garbage and deceive the users", US App Store, 09/03/2023

**[INFERRED]** — and this is a cost warning, not an opportunity: Snipd has a four-year head start
on corpus pre-processing and runs **in-house** ASR (per Ferdinand's HN comment), and users *still*
hit unprocessed episodes and *still* complain the per-minute price is above raw Whisper API cost.
A solo developer paying retail ASR API rates with a cold-start corpus of zero would face
materially worse economics on the same complaint. The corpus is Snipd's moat, and it is expensive.

### 4.4 Quota resistance — but note who is complaining and how

The 900-minute cap binds on heavy users. But read the framing carefully:

> "However, if you are a heavy podcast listener, 900 minutes (15 hours) a month of AI processing
> credits is not enough, but you can request more in app (for free, for now). I re-up my AI
> minutes a few times a month. **Would be willing to pay double, maybe triple, for unlimited
> minutes.**"

— **cali_guy_0024**, US App Store, Mar 11 (2026)

**[INFERRED]** This is *willingness-to-pay* evidence, not price resistance. A user volunteering
to pay $170–250/yr says the heavy-user segment is under-monetised, and that a competitor cannot
win this cohort on price. Contrast the only actual price complaint found:

> "Awesome product! Have been using since day 1."

— **Tom Etminan**, Product Hunt, ~2 years ago. His only gripe is that he'd like a lower
subscription price.

And, from the free tier, the opposite pressure:

> "I can't believe this is free. It integrates straight with Notion too, perfect for second brain.
> No need for a readwise subscription. Please stay free forever 😅."

— **Owen Wallbridge**, 5★, AU App Store, v2.2.48

**[INFERRED]** Snipd's free tier — which includes headphone capture, watch/CarPlay, *and* full
PKM export — has anchored a chunk of the audience at $0. This is the single most hostile fact in
this document for a paid new entrant: **the incumbent gives away exactly the feature set the
proposed app would charge for.**

### 4.5 Sync reliability and data loss

The clearest churn-causing defect class. Total data loss:

> "Enjoyed using the app. I have lost all my data, podcast queues and other info after the app
> decided to ask for my logins twice. Second time without a way to re-connect"

— **St. John 01**, 1★, "Great app - Extremely buggy", AU App Store, v3.6.96

That the *only* two 1-star reviews in my whole sample are (a) data loss and (b) account-deletion
mishandling is a signal about what actually drives users out.

Cross-device sync was broken for years and is only recently fixed:

> "The play queue should sync between devices. As far as I can tell, it doesn't or doesn't work.
> Maybe this only affects a small number of users who move between devices, but as someone who
> needs a separate work device, the experience of trying to match them up is tedious."

— **mocksa**, 3★-in-substance (rated 4★), "Cool AI but unfortunately lacking on some basics",
AU App Store, v3.2.0. His framing is worth quoting too: *"I wanted to like this, and I do, but not
as my main player. The AI features are really neat, but basic issues detailed below have never
been ironed out, even though this app is now a few years old."*

**[VERIFIED]** Snipd shipped "player progress sync across multiple devices" only in **v3.6.96
(Feb 2026)** — release note: *"You can finally use Snipd across all your devices!"* The word
"finally" is theirs. And v4.1.20 (Aug 2026) still fixes *"user getting logged out due to some
network issues."*

Account deletion / data-rights failure, from the 1★ review:

> "I sent an email to request to delete the account. As a result, the product team replied that
> there was no such function; the person in charge of operating account deletion went on vacation
> and you have to wait for half a month! ... But after at least one year ... I was logged in to
> the old account that should have been deleted more than a year ago!"

— **Sponge9999**, 1★, US App Store, 09/03/2023

To Snipd's credit, the co-founder replied publicly and by name **[VERIFIED]**: *"Hi Sponge, I am
very very sorry for this mistake! ... you can delete your account very easily inside the app's
settings ... You can also export your subscriptions in OPML format, if you decide to move to a
different podcast app. ... Kevin (co-founder of Snipd)"* (Developer Response, 06/21/2024).
**[INFERRED]** the ~10-month gap between review and reply is itself a small support-capacity
signal for a five-person team.

### 4.6 Export fidelity and PKM-pipeline friction — the richest vein

Snipd's official Obsidian plugin issue tracker is where the *paying PKM power users* complain in
detail. 26 issues, 15 still open, from Nov 2025 to Jun 2026. These are exactly the ticket's target
demographic and they are all verbatim and attributable.

**Export regressed and lost timestamps/playback links** — a fidelity regression, i.e. the new
first-party plugin is *worse* than the older Readwise path:

> "Previously, when you exported/synced snips, the Obsidian note included the exact segment of the
> podcast from which a snip originates, with a playback link and timestamps... This information is
> not currently included by the Obsidian plugin. Would it be possible to add this back, or expose
> it as an optional setting?"

— **adamajane**, [issue #16](https://github.com/snipd-app/snipd-obsidian/issues/16), 2026-01-11 (still open)

**Feature parity gap between export paths:**

> "Currently, the Readwise Snipd integration allows you to sync the Episode AI Notes summaries. The
> official plugin does not appear to support that."

— **jaxley**, [issue #13](https://github.com/snipd-app/snipd-obsidian/issues/13), 2025-12-15

**No transcript export into the vault:**

> "Would love to be able to import full transcripts or transcripts for Snips into Obsidian so
> they're searchable"

— **hamezuccino**, [issue #22](https://github.com/snipd-app/snipd-obsidian/issues/22), 2026-03-01 (open)

**Migration pain — the exact "library migration" concern the ticket asked about:**

> "I've been use Snipd for many years and have lots of exported files(every month). Recently I try
> this plugin and want to switch old exported files to new format with this plugin. After comparing
> two format markdown files, I found some template varibles are missing"

— **bgzo**, [issue #23](https://github.com/snipd-app/snipd-obsidian/issues/23), 2026-03-08 (open)

**Silent sync failure:**

> "when I try to sync, the progress doesn't move off zero percent. I did a test sync, and that
> worked correctly. When I do a proper sync, the folders in the base file are added, but there's
> just no content."

— **aarontimo**, [issue #7](https://github.com/snipd-app/snipd-obsidian/issues/7), 2025-12-01 (open)

**Filename/OS-compatibility breakage** — mundane but the kind of thing that quietly kills trust:

> "The episode title is often incompatible with the file naming conventions of Linux and Windows,
> causing unpredictable errors - for example, when synchronizing files."

— **mcmilupa**, [issue #3](https://github.com/snipd-app/snipd-obsidian/issues/3), 2025-11-21 (open)

Also: `episode_title` unset when a title starts with `#` ([#21](https://github.com/snipd-app/snipd-obsidian/issues/21),
**Toubi01**); frontmatter not customisable ([#10](https://github.com/snipd-app/snipd-obsidian/issues/10),
**jaxley**); confusion about which template controls what — *"I'm in the template, deleting and
changing the fields, but it keeps doing the same default Frontmatter... Just all around confused."*
(**bloominburges**, [#6](https://github.com/snipd-app/snipd-obsidian/issues/6)); the plugin
breaking unrelated Obsidian UI — *"Something in this plugin interferes with the appearance of all
menus on mobile while in portrait."* (**bea-hemm**, [#8](https://github.com/snipd-app/snipd-obsidian/issues/8));
Google auth failing outright (**meagerfindings**, [#5](https://github.com/snipd-app/snipd-obsidian/issues/5));
and the plugin briefly not being findable in the community directory at all
(**RemkoPape**, [#24](https://github.com/snipd-app/snipd-obsidian/issues/24)).

**[INFERRED]** This is the genuine soft spot: **export/PKM-pipeline polish**, not capture. The
plugin is 10 months old, 15 of 26 issues are open, and the complaints are from committed users who
want *more* Snipd, not less. But note the strategic implication is unfavourable: these users are
**retained and invested**, not churning. Fixing their complaints is a feature-request backlog for
Snipd, not an opening for a new player — a new entrant cannot serve them without first replicating
capture, ASR, corpus, and player.

**Export-clutter, which cuts against auto-AI-snipping:**

> "Please add a 'delete all snips option' as far as I can see right now the only way I can delete
> all snips within an episode is to go into the highlights and delete them one by one. The problem
> with this is if I want to export things to my Readwise account, I will now get a mix of snips
> that I want to keep and random AI generated snips from podcasts that aren't worth highlighting."

— **Naroshkabov**, 4★, AU App Store, v3.5.9

### 4.7 No web/desktop client — the most-repeated single request

Four independent sources, across four years:

> "There are a couple of bigger, harder, development improvements I wish could take place
> (web/desktop access)"

— **cali_guy_0024**, US App Store, Mar 11 (2026)

> "Snipd makes consuming and learning from podcast content easier than any other podcasting app for
> iOS." — his one complaint being the missing desktop app for note-taking at work.

— **Skyler Reeves**, Product Hunt, ~3 years ago

> "Love this app and I would love either a iPad or desktop version. As I have one hand that works
> properly because of a disability - having it just iPhone is tiring sometimes"

— **LibraryGeekGirl**, 5★, AU App Store, v3.3.8

> "I either want pocketcast to get a snippet type feature on snipd/overcast to have a web client.
> One or the other isn't too much to ask I think."

— [hackeraccount, HN, 2022-10-23](https://news.ycombinator.com/item?id=33307127)

> "nice, I've been looking for a free alternative to snipd with ability to use on desktop."

— [idbnstra, HN, 2026-04-10](https://news.ycombinator.com/item?id=47722834)

**[INFERRED]** A real, durable, four-year-unserved gap — but it points **away** from the proposed
concept. The demand is for a *desktop/web* surface, and the map puts "Android, web, and desktop
clients" explicitly **out of scope**. This gap is therefore unaddressable within this effort's
destination.

### 4.8 Other recurring complaints (briefly, all VERIFIED)

- **Battery drain**: *"the impact on battery is egregious (~1% per 2min playback on newest
  hardware). This makes it a bit like a luxury roadster with hexagonal wheels: awesome, unless
  it's moving."* — **GroomedMonkey**, 3★, AU, v3.0.49
- **Non-English languages**: *"I do need more language options, especially Chinese like Mandarin
  and Cantonese. Would have subscribed in a heartbeat if these languages are included and done
  well."* — **Chan Pui-Kwan**, 4★, AU, v3.6.5. Echoed on HN by a competing developer:
  *"1. It does not support Chinese transcription 2. It is more like a note-taking software rather
  than a podcast software. Therefore, I still developed this app."* —
  [kindjeff, HN, 2024-08-12](https://news.ycombinator.com/item?id=41222633). (Snipd now claims 26
  languages, so this may be resolved.)
- **Player fundamentals lag dedicated players**: *"the library management isn't as smooth as pocket
  casts, with some simple options notably missing. For example: play all episodes in a filter, or
  auto download by filter."* — **Tom McCleery**, 5★, AU, v3.6.12. And on missing silence-trim and
  widgets: **bebankzt**, 5★, AU, v3.4.34.
- **Watch/CarPlay were absent or poor for years**: *"car app is useless and watch app missing...
  Its an app for productivity, but you ll have to bring the phone out everytime you want to use
  the snip feature."* — **OK.786**, AU, v3.0.69. (Both now ship; v4.1.20 still fixes "Apple Watch
  performance issues" and CarPlay crashes.)
- **Discovery quality**: *"Discover page only shows Rogan-Hibernian-core…"* — **hodgea56**, 4★, AU, v3.4.17
- **Cold-start / onboarding**: *"it feels unintuitive as someone moving from Spotify"* —
  **Kamil Szafraniak**, Product Hunt, ~3 years ago; he still defaults to Spotify.

### 4.9 Do users churn back to their old player? — the switching evidence

The ticket asks this specifically. The evidence points **the wrong way for a new entrant**:
users churn **into** Snipd from mainstream players and stay.

**[VERIFIED]** switching-in testimonials:

> "after ~9 years on @OvercastFM, i have finally made the big move to @snipd_app by @KevinBenSmith.
> its the first AI native podcast app for power podcast consumers. not perfect by any means, but the
> synced transcripts are much better for multimodal browsing"

— **swyx**, [x.com/swyx, 2024-07-18](https://x.com/swyx/status/1813745200524915176) (quoted on Snipd's pricing page)

> "fully converted from Overcast to Snipd for podcasts"

— **Blake Robbins**, [x.com/blakeir, 2024-03-08](https://x.com/blakeir/status/1766086331300561049)

> "Tried nearly all podcast apps. This is one of the bests. Used Pocket Casts for two years."

— **bebankzt**, 5★, AU App Store, v3.4.34

> "I was on and off for a lot of the year but finally went all in with an annual subscription!"

— **Isaac_andy97**, 5★, AU App Store, v3.6.75

The only churn-*out* cases in my sample are the two 1★ reviews (data loss; account deletion) and
**mocksa**, who keeps Snipd but "not as my main player" because of queue-sync and download basics.

**[VERIFIED]** the displaced-competitor testimonial that most directly undercuts a new entrant —
a user describing Snipd as the successor to a *previous* podcast-highlighting app:

> "I was a huge fan of the AirrQuote app before this, but the interface was too buggy and it had
> very minimal features. Snipd is everything I wanted AirrQuote to be. Not only is the interface
> clean and responsive, but it implements every feature that AirrQuote was lacking. Even down to
> the ability to customise actions with your headphones (i prefer setting fast-forward to 'take
> snip'). Readwise integration was also a must for me. Ease of sharing snips is also incredibly
> smooth. All this on top of AI driven smart snipping and transcripts makes this app almost
> perfect."

— **BillSwag420**, 5★, AU App Store, v2.0.38

**[INFERRED]** This is the market's verdict in one review: the previous entrant in this exact
category (Airr) lost, Snipd won, and the winner is described as "almost perfect."

---

## 5. Competitor liveness — the graveyard

The ticket asked whether Airr, Fathom, Recast and Podurama still exist. **This is the strongest
single body of evidence in the teardown.** Checked today via Apple's iTunes Lookup API, DNS, live
HTTP, and Wayback CDX.

| Product | Status | Evidence |
|---|---|---|
| **Airr** (`airr.io`, App Store id **1355926315**) | **DEAD** | App Store lookup returns **zero results** in US/GB/CA/AU/DE — the listing is gone. Wayback shows its App Store page returning **404 as of 2025-09-23** (last 200 was 2023-06-12). `airr.io` DNS still resolves (35.241.62.204) but HTTP returns **504 Gateway Timeout** / TLS failure. Last Wayback capture of the site: **2023-10-23**; **no captures at all after Nov 2023**. |
| **Fathom** (`fathom.fm`) | **DEAD** | Domain **does not resolve** — NXDOMAIN. Wayback: last HTTP 200 **2025-02-28**; **404 from 2025-03-28 onward** (confirmed again 2025-07 and 2026-05). Died ~March 2025. (Note: "Fathom AI Note Taker", id 6746237515, is an unrelated *meeting*-notes app.) |
| **Recast** (`recast.fm`) | **EFFECTIVELY DEAD** | Domain registered until 2027 and DNS resolves (208.91.197.27 — a parking-range IP), but HTTPS **times out** with no response. Last Wayback capture: **2025-08-16**, and that snapshot's body renders as **empty**. No iOS app findable under any "Recast podcast" search. `recast.app` now redirects to `recastpay.com` — an unrelated payments company. |
| **Podurama** | **ALIVE** | [AI Podcast Player: Podurama](https://apps.apple.com/us/app/id1497491520), Podurama Ltd, v**7.0.1**, updated **2026-07-07**, **4.3★ / 397 ratings**, released 2020-05-21. `podurama.com` serves 200. But note: it is a *general* podcast player ("the best free Podcast player for mobile, tablet and web with no ads") with bookmarks — **not** an AI-capture competitor. Its own reviews are about playlists and resume-position bugs, not highlighting. |

**Adjacent entrants found while researching, for completeness [VERIFIED]:**

- **Podwise** (id 6499190232, PODWISE PTY LTD): v1.3.3, updated 2026-08-31, **4.8★ but only 80
  ratings**. Alive, tiny.
- **Onda AI Podcast Note Taker** (id 6743153167): v1.2.1, last updated **2025-08-25** — **13 months
  stale, 0 ratings**. Effectively abandoned.
- **Anycast+** — [Show HN, Aug 2024](https://news.ycombinator.com/item?id=41222633) — got **0
  points**. Its developer's stated reason for building was Chinese transcription, not capture.
- **Steadcast** — free Mac podcast player, [Show HN twice in April 2026](https://news.ycombinator.com/item?id=47783496),
  **0 points both times**. Its developer volunteered: *"Snipd was definitely in my head when I was
  building the Memories feature, though I went less highlight-share-y and more private-notebook."*
- **Scribbler**, **PodText.ai** — 2023 Show HNs in this space, both **0 points**, both gone.

**[INFERRED] Read the graveyard carefully, because it cuts two ways and the second way matters
more.** The naive reading is "competitors died, so there's room." The correct reading is:

1. **Three direct competitors died within ~30 months of each other** (Airr ~late 2023, Fathom
   ~Mar 2025, Recast ~Aug 2025). Airr was the *category originator* — it had press coverage,
   an [HN writeup in 2020](https://news.ycombinator.com/item?id=24006107), and users who loved it
   enough to still name it in 2026 reviews. It still lost.
2. **The one survivor is the one that vertically integrated** — in-house ASR, a pre-processed
   million-episode corpus, its own player, five capture surfaces, and seven PKM integrations. That
   is a large surface area for a solo developer to match.
3. **Every lightweight entrant that tried the narrow "just the capture" wedge got zero traction.**
   Steadcast, Anycast+, Scribbler, PodText.ai, Onda: 0 HN points, 0 ratings, or abandoned. And
   note the 2022 HN post [Screenshot Lock Screen to Take Podcast Note](https://news.ycombinator.com/item?id=33345268)
   proposed **almost exactly the narrow companion-capture concept** in this map — *"I don't want a
   whole new podcast player. I just want a better way to take podcast notes and organize them"* —
   and it received **5 points and zero replies**. Four years later, nobody has built it.

A graveyard where the deaths cluster and the survivor is the most-integrated player is evidence of
a **market that does not support narrow entrants**, not evidence of an opening.

---

## 6. Is the market saturated? The three-way verdict

The ticket asks whether the complaint pattern indicates **(a)** an unmet need a new entrant could
serve, **(b)** a category users try and abandon because the need is weaker than it looks, or
**(c)** a solved problem with a satisfied base.

### Verdict: predominantly (c), with a material (b) component, and (a) only in places this effort has ruled out of scope.

**The case for (c) — solved problem, satisfied base. This is the dominant reading.**

- **[VERIFIED]** 4.7★ / 1,142 US ratings. In a ~30-review qualitative sample, exactly **two 1★
  reviews**, both about *reliability incidents* (data loss, account deletion) rather than the
  product concept.
- **[VERIFIED]** Users describe it in terms normally reserved for solved problems: *"This is easily
  the #1 app I cant live without. Period."* (**Lennox S**, AU, v3.6.100); *"Excellent execution of
  an excellent idea. I was constantly taking notes while listening to podcasts but not possible
  while driving, which is when I mostly listen. **This solves that.** Great app, use it every
  day."* (**bnorry**, AU, v3.0.61); *"If I need only two apps on my phone / One is Readwise, the
  other is Snipd."* (**Phantom889**, AU, v3.6.5).
- **[VERIFIED]** The people who *do* complain are **power users asking for more**, not people
  leaving. The Obsidian-plugin complainants include a user with **8,582 snips across 358 episodes
  in 2025** ([thiagoghisi, issue #20](https://github.com/snipd-app/snipd-obsidian/issues/20), who
  [blogged](https://thiagoghisi.substack.com/p/my-top-25-podcast-episodes-and-interviews) that it
  is *"a game-changer"* and *"Say goodbye to taking screenshots or opening the notes app while you
  are on the gym"*). That is retention, not churn.
- **[VERIFIED]** Willingness-to-pay is *above* the current price for heavy users
  (*"Would be willing to pay double, maybe triple"* — cali_guy_0024), so there is no price umbrella
  for an undercutter either.
- **[VERIFIED]** Price has been flat at $6.99/mo for ~20 months with weekly shipping — a stable,
  actively-maintained incumbent, not a stagnating one.
- **[VERIFIED]** The specific interaction the proposed app names as its wedge — one-tap,
  no-look capture — ships on **five surfaces and is FREE**.

**The case for (b) — a category users try and abandon. Real, and it constrains the market size.**

The strongest evidence for (b) is not complaint content, it is the **graveyard plus the ceiling**:

- **[VERIFIED]** Three direct competitors dead in ~30 months (Airr, Fathom, Recast). Airr had first-
  mover advantage and named advocates, and still died.
- **[VERIFIED]** After **4.5 years**, the surviving category leader has **1,142 US App Store
  ratings**. For scale from the same API today: Overcast 47,692; Pocket Casts 15,664; Podbean
  53,920; Apple Podcasts 2,073,765. Snipd has roughly **2.4% of Overcast's rating count**.
- **[VERIFIED]** Snipd's Obsidian plugin: 72k installs vs Readwise's 243k in the same ecosystem.
- The most incisive statement of the demand ceiling comes from a user, not from me:

> "I think most people listen to podcasts for fun and entertainment so it's unlikely they'll want
> to clip, get transcripts etc. But the small number of podcasts doing deep dives on scholarly,
> technical or professional matters? It's potentially quite useful to be able to get
> transcripts/excerpts with highlights and audio clips to add to personal notes for future
> reference."

— [lawtalkinghuman, HN, 2022-10-24](https://news.ycombinator.com/item?id=33316379)

And self-identification of the segment as unusual, from a user who rigged a smartwatch to trigger
Snipd snips:

> "In other words, I am apparently exactly the kind of weirdo who would use the heck out of
> something like this!"

— [smeej, HN, 2025-12-09](https://news.ycombinator.com/item?id=46211684)

**[INFERRED]** The "capture ideas from podcasts into a PKM" behaviour is a **genuine but narrow
niche** — a subset of a subset (knowledge-podcast listeners ∩ active PKM users). Snipd appears to
have won most of it. The graveyard is what a small TAM looks like from the outside: not enough room
for several players, and the survivor took it.

**Where (a) — unmet need — genuinely exists, and why it doesn't help here:**

Three real, durable, four-year-unserved gaps emerged. Each is a problem for this effort:

1. **Web/desktop client.** The most-repeated request in the corpus (5 independent sources, 2022–
   2026). **Explicitly out of scope** per `map.md` ("Android, web, and desktop clients").
2. **Snip boundary accuracy.** The one defect *inside* the capture moment — *"Every time I take a
   snip, I have to adjust the start/end points a little bit anyways"* (whitneyelsworth);
   *"the snips don't always accurately capture the section you want"* (Met Samuel). Also
   **explicitly out of scope** per `map.md` ("The 'smart boundaries' roadmap... Ruled out of this
   effort's scope"). **This is the finding most worth escalating**: the ticket asked for the wedge,
   and the evidence says the only capture-adjacent wedge is the one the map ruled out.
3. **PKM export fidelity/templating.** Real (15 open issues) but it is a *backlog*, not a market —
   a new entrant cannot serve those users without first rebuilding capture, ASR, corpus and player.

**What this means for the go/no-go — counter-validating, per the map's standing preference:**

- The brief's premise that capture friction is unsolved is **falsified**. It is solved, five ways,
  free, by a live and actively-shipping incumbent.
- The remaining defensible wedges are the two the map has ruled out of scope (boundaries; desktop).
- There is **no price umbrella**: free covers capture + export; heavy users want to pay *more*.
- **The $2–5k MRR bar in context.** At Snipd's $83.90/yr, $3k MRR ≈ **~430 paying annual
  subscribers**. That number is not absurd on its face. But: the category leader — funded ($700k),
  five people, four-and-a-half years, in-house ASR, weekly releases, Ali Abdaal and swyx
  endorsements — has accumulated 1,142 US ratings total, and its *revenue is not publicly known*.
  A solo developer with **no audience, no newsletter, no PKM presence** (per `map.md`) would be
  competing for a slice of that same narrow niche, against a free tier that already does the
  headline feature. **[INFERRED]** I would not represent 430 cold-start subscribers in this category
  as a likely outcome, and I want to be explicit that **I have no revenue data on which to model it
  either way** — the honest statement is that the funnel is unquantifiable from public evidence and
  the qualitative signals are unfavourable.

**Explicit statement of what would change this verdict.** I would revise toward (a) if: Reddit
evidence (inaccessible here) showed a large cohort of *ex-Snipd* users describing why they left; or
if Snipd's rating count were shown to be falling / the app to have stopped shipping; or if the
map's scope were widened to include boundary detection or a desktop surface. None of those is
established by the evidence I could reach.

---

## 7. Confidence and gaps

**High confidence [VERIFIED, primary sources read today]:** Snipd's feature set, the five capture
surfaces, current pricing ($0 / $11.90 mo / $83.90 yr), free-vs-paid split, App Store rating and
version cadence, funding ($700k pre-seed, Wingman + Acequia), 2022 team size (five), the Obsidian
plugin install count, and the liveness/death status of Airr, Fathom, Recast and Podurama.

**Medium confidence:** the complaint *taxonomy*. The themes recur across independent sources
(App Store, Product Hunt, GitHub, HN), which is reassuring, but the negative-review sample is
~30 reviews and Apple's surfacing is biased positive.

**Low confidence / explicitly unknown — not estimated:**
- Snipd's revenue, MRR, paying-subscriber count, conversion rate, churn. **No public data exists.**
- Snipd's true user count. Only unaudited marketing copy ("hundreds of thousands").
- Whether Snipd raised after 2022. No announcement found; absence of evidence only.
- Current team size (last figure is 2022's "five").
- **Reddit sentiment entirely** — r/podcasts, r/ObsidianMD, r/PKM, r/Zettelkasten were all
  inaccessible. **A follow-up pass with working Reddit access is the highest-value remaining
  research action**, specifically hunting for churned-out users, which is the one thing that could
  move the verdict.
- Whether private/Patreon RSS snipping now works in 4.1.21.
- Snipd's Android footprint (Google Play was not checked; the map scopes the decision to iOS).
