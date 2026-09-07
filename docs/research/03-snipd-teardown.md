# 03 — Snipd teardown: what it ships, its weak spots, and whether the market is saturated

Research date: **2026-09-07**. Ticket: `issues/03-snipd-teardown.md`.

Every claim below is tagged **[VERIFIED]** (read directly from a primary source today, quoted)
or **[INFERRED]** (my reasoning from the evidence). Where evidence does not exist, this file
says so explicitly rather than estimating.

## Methodological caveat — read this first

> **Update 2026-09-07 (pass 03b, issue #11): the Reddit gap has been partly closed.** A follow-up
> pass ran via the **Arctic Shift archive** (`arctic-shift.photon-reddit.com`), the route proven
> in `04-demand-evidence.md`. Direct Reddit access was retried first and is **still blocked** —
> see the route table in §4.10. The pass recovered the r/ObsidianMD, r/Overcast and r/podcasts
> material that this section originally reported as unreachable. **It did not overturn the
> saturation verdict, but it did surface one new complaint theme (§4.10) and one materially
> adverse competitive development (§5.1) that this document did not previously contemplate.**
> New material is confined to **§4.10**, **§5.1**, and the restated verdict in **§6**; the
> original text below is left as written, including its own claims about what was unavailable.

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

### 4.10 Reddit evidence (pass 03b, 2026-09-07) — route, coverage, and what it added

This section closes the gap the caveat at the top of this file declared. It is placed inside the
taxonomy, not appended as a loose section, because its content belongs to themes 4.1, 4.6, 4.7
and 4.9 — plus **one theme that was previously missing entirely** (offline dependency).

**Route, retried in this order.** Recorded per the ticket's requirement.

| Route | Result 2026-09-07 |
|---|---|
| `api.reddit.com` (search) | **403** |
| `reddit.com/search.json`, `old.reddit.com/.../search.json` | **403** / 302 to bot-wall |
| Redlib mirrors: `catsarch.com`, `perennialte.ch`, `privacyredirect.com`, `l.opnxng.com` | **403** (opnxng redirects to catsarch, which 403s) |
| `safereddit.com` | HTTP **200** but serves an Anubis *"Verifying your browser…"* JS challenge — no content |
| PullPush (`api.pullpush.io`) | **429**; body states scraping is now a paid service |
| **Arctic Shift** (`arctic-shift.photon-reddit.com`) | **WORKS** — the only route that returned data |

So: **direct Reddit access has not recovered.** Every Reddit quote below came from Arctic Shift.

**Two archive quirks that matter for reading the numbers honestly**, because both can manufacture
false negatives and I hit both:

1. Comment body search **requires a subreddit scope** (`body=` alone is rejected). There is no
   global term search on this route.
2. Rare terms in large subreddits **time out server-side**, and the API returns
   `{"data": null, "error": "Timeout..."}` — an HTTP 200 that a naive parser reads as *zero hits*.
   My own first pass made exactly this mistake. Every count below comes from a response that was
   checked for the error field; windows that never resolved are listed as unresolved, **not** as
   empty. Additionally the archive emits raw control characters and invalid backslash escapes in
   comment bodies, which breaks strict JSON parsing — silently dropping real results unless
   repaired. **Treat any prior "no Reddit hits" claim made without these two checks as void.**

#### What it added to the existing themes

**Theme 4.1 (capture boundary accuracy) — corroborated, and dated back to 2021.** Two PKM users
independently describe the post-processing tax at launch:

> "Snipd provides transcripts by default. There's a default number of seconds of capture time.
> It's not (and can't be) an exact highlight of the phrase or idea you want to capture, so you
> need to add a post-processing cleanup step."

— **u/SkydiveMike**, r/ObsidianMD, 2021-11-02,
[hizfbna](https://reddit.com/r/ObsidianMD/comments/qkk8fm/we_at_snipd_just_released_an_obsidian_integration/hizfbna/)
(Arctic Shift)

And Snipd's own reply concedes the design limit, which is the strongest available confirmation
that boundary detection is intrinsic rather than a passing bug:

> "By default, the 'snipping' highlights the entire chapter which is currently playing... You can
> then change the start & end of your highlight by using the transcript."

— **u/snipd_app**, r/ObsidianMD, 2021-11-02,
[hizsp2l](https://reddit.com/r/ObsidianMD/comments/qkk8fm/we_at_snipd_just_released_an_obsidian_integration/hizsp2l/)
(Arctic Shift)

**[INFERRED]** §4.1 said boundary accuracy might be the only capture-adjacent wedge. This pass
makes that finding **older and better attested** — the complaint is present on day one of the
Obsidian integration in 2021 and still present in 2026 App Store reviews. It does **not** make it
a bigger commercial opportunity; see §6.

**Theme 4.6 (export fidelity) — the pattern is five years old, not a 2026 plugin regression.**
§4.6 read the missing timestamps/headings as a regression introduced by the first-party plugin.
Reddit shows the same complaint in 2023, against the older export path:

> "The Obsidian export format is beautiful in the reading mode, but I take Obsidian notes to work
> on them... 1.a. The headings were not exported... 1.b. The time signatures were not exported...
> 1.c. The formatting was just standing in my way, I found myself with lots of parasite code in an
> infinite one-column text. I needed to manually clean the code... 2. The selected snip was a bit
> over 10 minutes, but the exported text stopped after around 6 or 7 minutes."

— **u/archAndrew**, r/ObsidianMD, 2023-04,
[jgo1fae](https://reddit.com/r/ObsidianMD/comments/qkk8fm/we_at_snipd_just_released_an_obsidian_integration/jgo1fae/)
(Arctic Shift)

**[INFERRED]** This slightly *weakens* the "the new plugin is worse than the old Readwise path"
reading in §4.6: export fidelity has been a persistent weak point across both paths, so it looks
structural to turning chapter-length audio into clean notes, not a specific regression.

**Theme 4.7 (no desktop client) — extended back to 2021.**

> "My main issue is that I mostly listen on the desktop, and these new apps with annotation
> features are unfortunately mobile-only. The desktop is the only place where I am ready to take
> notes actively, and on mobile (= on the go), it would just inconvenience me."

— **u/LordDeath86**, r/ObsidianMD, 2021-11-01,
[hiy2zye](https://reddit.com/r/ObsidianMD/comments/qkk8fm/we_at_snipd_just_released_an_obsidian_integration/hiy2zye/)
(Arctic Shift)

The request is thus **five years unserved**, not four. Still out of scope per `map.md`.

**Theme 4.9 (churn) — a second independent account that Airr lost on execution.** §4.9 rested on
one App Store review (BillSwag420). Reddit supplies a year-long Airr beta tester:

> "**Airr** — The transcripts are reliably quite good. But at the moment, you can no longer
> request more than a single episode transcript per day... Airr appears to work best on faster
> devices... Newer updates still remain non-functional (crashes regularly but especially whenever
> I make highlights..). Without Readwise, exporting is a pain if you take lots of highlights with
> transcripts. **Snipd** — Switched over to Snipd as soon as I saw this post. And I'm absolutely
> in love."

— **u/doyouhavesauce**, r/ObsidianMD, 2021-11-03,
[hj5sw3z](https://reddit.com/r/ObsidianMD/comments/qkk8fm/we_at_snipd_just_released_an_obsidian_integration/hj5sw3z/)
(Arctic Shift)

**[VERIFIED]** The demand statement the ticket most wanted — a non-listener converted *into* the
category by the capture feature:

> "I usually don't listen to podcasts because it is impractical to pause and take notes. And it's
> an absolute nightmare to remember you heard something in some podcast... End result is that I
> don't really learn anything that I can use or reuse. This is a good enough reason to try snipd
> in particular and retry podcasts again."

— **u/Psychsatani**, r/ObsidianMD, 2021-11-01, 17 points,
[hiwxdgj](https://reddit.com/r/ObsidianMD/comments/qkk8fm/we_at_snipd_just_released_an_obsidian_integration/hiwxdgj/)
(Arctic Shift)

#### NEW theme — offline / cloud dependency (not in the original seven)

This is the one substantive complaint the original taxonomy missed, and the closest thing to a
churn-out post the pass found. An entire r/podcasts thread titled **"Snipd Dealbreaker"**:

> "Love the 'Snips' feature but the major downer of this App is that you need a reasonably good
> network connection for it to work. It was dead in the water on a flight to LA. And even when
> driving around will hang while trying to download favorites (never had either of these issues
> with Overcast)"

— **u/BartSmithsonn**, r/podcasts, 2026-04-29,
[1tqrud4](https://reddit.com/r/podcasts/comments/1tqrud4/snipd_dealbreaker/) (Arctic Shift)

**Honest limits on this one.** It is **single-source**: I searched the full App Store review
corpus (AU/BR/JP RSS feeds, the only storefronts still serving) for
`offline|network|connect|download|flight|plane|wifi|signal` and found **no** corroborating
complaint. The thread's only reply was **later removed** and promoted a product, so I am not
citing it. So: a real, verbatim, on-point dealbreaker post from a user comparing unfavourably
against Overcast — but **one** of them. Recorded as a theme because it is structural (a cloud-ASR
architecture genuinely cannot work on a plane), flagged as thin because it is n=1.

#### r/PKMS — the richest Snipd-specific vein found (added on second parse)

r/PKMS was the highest-yield subreddit in this pass (37 hit rows). It contains a dedicated
**"Snipd vs Airr for podcast note-taking"** thread
([xodrk7](https://reddit.com/r/PKMS/comments/xodrk7/snipd_vs_airr_for_podcast_notetaking/), 2022-09)
that runs to 2024 — a longitudinal record of exactly the ticket's target demographic choosing
between the two, then living with the choice. All Arctic Shift.

**Why Airr lost, from users who chose against it in real time** — this triangulates §4.9's
single-review conclusion with three more independent voices:

> "I use snipd because back when I used Airr it often didn't remember where I was in a podcast the
> last time I listened so it started over. The Airr app overall is just really glitchy."

— **u/oskernaut**, 2022-09-26,
[ipzlqq6](https://reddit.com/r/PKMS/comments/xodrk7/snipd_vs_airr_for_podcast_notetaking/ipzlqq6/)

> "I eliminated Airr because of a lack of company Twitter traffic (putting doubt in if the company
> is really still alive and moving forward?), and negative feedback on Twitter"

— **u/thepolymathelder**, 2022-09-26, 5 points,
[ipzdtk6](https://reddit.com/r/PKMS/comments/xodrk7/snipd_vs_airr_for_podcast_notetaking/ipzdtk6/)

**[VERIFIED]** The most important line in this thread for sizing the category, from a user who
adopted Snipd and kept using it:

> "But yeah...podcast note taking is a surprisingly **dry space** at the moment."

— **u/Remixer96**, 2022-09-26, 6 points,
[ipydl25](https://reddit.com/r/PKMS/comments/xodrk7/snipd_vs_airr_for_podcast_notetaking/ipydl25/)

**[VERIFIED]** And the closest thing to a stability-based churn signal the pass found, from that
same user five months later:

> "Sadly no, and **Snipd hadn't been the most technically stable app either.**"

— **u/Remixer96**, 2023-03-04,
[javjdiz](https://reddit.com/r/PKMS/comments/xodrk7/snipd_vs_airr_for_podcast_notetaking/javjdiz/)

**[INFERRED]** Note the past tense ("hadn't been"), which reads as a user who has stopped or
reduced use. This is the second churn-adjacent data point (with §4.10's dealbreaker post), and it
corroborates **§4.5 (sync reliability and data loss)** from an independent source. Still not a
cohort — two users, different reasons — but §4.5's confidence rises.

**Export friction, quantified by a user who counted the taps** — the sharpest version of §4.6:

> "Yikes! **Seven screens and nine taps.** So, yes, manual and crazy long process...I hope I'm
> missing something."

— **u/thepolymathelder**, 2022-09-27,
[iq3m7bz](https://reddit.com/r/PKMS/comments/xodrk7/snipd_vs_airr_for_podcast_notetaking/iq3m7bz/)

**Transcription accuracy — a complaint theme under-weighted in the original taxonomy.** §4.1 covers
snip *boundaries*; these users complain about ASR *accuracy*, which is distinct:

> "I really like Snipd but the transcription is often times wrong lol."

— **u/oskernaut**, 2022-09-26, 3 points,
[ipzouv0](https://reddit.com/r/PKMS/comments/xodrk7/snipd_vs_airr_for_podcast_notetaking/ipzouv0/)

> "I agree that the Snipd transcription is far from perfect."

— **u/thepolymathelder**, 2022-09-26,
[ipzweeu](https://reddit.com/r/PKMS/comments/xodrk7/snipd_vs_airr_for_podcast_notetaking/ipzweeu/)

**[INFERRED]** This is a *cost* warning for a new entrant, like §4.3: Snipd runs in-house ASR and
users still call it "far from perfect." A solo developer paying retail ASR rates would not
obviously beat it.

**Price resistance at the free→paid transition** — relevant to §6's "no price umbrella" claim,
and mildly against it:

> "I used the previous free version once or twice a week to export podcast transcripts to my
> Obsidian vault. However, now that they've moved most of that functionality to the premium paid
> version, I'm not sure I'll keep using it... I think they **overpriced** and the new features
> aren't that much better than before IMO."

— **u/redmelon42**, r/ObsidianMD, 2023-09-10, 8 points,
[16enxj3](https://reddit.com/r/ObsidianMD/comments/16enxj3/what_do_you_think_of_snipd_premium/)

> "Great catch - didn't know about Snipd. But, darn, paid subscription."

— **u/Barycenter0**, r/PKMS, 2024-05-10,
[l3h8mfg](https://reddit.com/r/PKMS/comments/1cnzs5d/timestamping_videos_with_just_press_of_a_button/l3h8mfg/)

**[INFERRED]** §6 argues there is "no price umbrella" because heavy users would pay *more*. That
remains true at the top of the market, but these two show a **lower** segment that balks at
Snipd's paywall. This is the strongest pro-(a) evidence the pass produced. I am not upgrading it
further because both users describe *reducing use*, not *paying someone else* — no revealed
willingness to pay a competitor is demonstrated.

**Low switching cost, stated explicitly** — a warning about defensibility in both directions:

> "genious! I would use it and easily **ditch snipd**."

— **u/Legal-Judgment-908**, r/PKMS, 2024-06-19, 5 points, replying to someone launching a podcast
second-brain tool,
[l9atze0](https://reddit.com/r/PKMS/comments/1djhvrz/i_built_a_second_brain_tool_for_podcasts_as_a/l9atze0/)

**[INFERRED]** Cuts both ways and is worth stating plainly: users are willing to leave Snipd for
something better, which is mildly pro-(a) — but the same non-existent switching cost applies to
anything a new entrant builds. Note also that the tool being praised here launched in 2024; I did
not find it still operating.

**Still-open gaps confirmed in 2026** — the most recent substantive post found, which reads as a
checklist of unfixed §4.6/§4.7 issues from an active researcher:

> "I like how I can 'snip' sections as I listen and import into Obsidian... But I'm not too happy
> with a few things like: Lack of desktop player / Sometimes convoluted player / Difficult to find
> the episodes I'm interested in / **Doesn't give me a source link, just the Snipd link**, which if
> I reference others can't play without also having the app... The snip template is a bit tricky to
> get right... In sum, it's a great resource but **seems like there should be a better tool for this
> purpose.** Any suggestions on alternatives?"

— **u/Hour_Papaya_5583**, r/ObsidianMD, 2026-08-08, 5 points,
[1viie03](https://reddit.com/r/ObsidianMD/comments/1viie03/podcasts_as_source/)

**[INFERRED]** This is the single most encouraging quote in the pass for the proposal — a 2026
power user explicitly asking for alternatives. Weigh it against §5.1 and §6 before treating it as
a green light: the gaps named are desktop (out of scope), citation/source links (a
citation-management feature, not capture), and template control (§4.6's backlog).

**A skeptical note on the "Discover/highlights feed" premise, from someone building in the space:**

> "I keep seeing tools (Snipd being the main one) that auto-extract highlights... But I talk to a
> lot of Obsidian users who say the same thing: **highlights feeds feel useful for 3 days and then
> they stop opening it.** The stuff that actually ends up in their vault came from moments they
> were actively listening and chose to capture."

— **u/Remote-Positive-8951**, r/ObsidianMD, 2026-03-08,
[1rokpmq](https://reddit.com/r/ObsidianMD/comments/1rokpmq/does_a_podcast_highlights_feed_actually_help_you/)

**[INFERRED]** Treat as a competitor's hypothesis, not as evidence — the author is soliciting
validation for their own product. But it aligns with §4.1's *deliberate-listener* complaint about
automatic snips creating clutter, and it supports the narrower reading that **user-initiated
capture is the durable behaviour and AI-surfaced discovery is not.**

#### r/Zettelkasten — the "capturing notes from audio while driving" thread

**[VERIFIED]** r/Zettelkasten contains a thread on exactly this effort's use case
([zboiem](https://reddit.com/r/Zettelkasten/comments/zboiem/capturing_notes_from_audio_while_driving/),
2022-12, "Capturing notes from audio while driving"). Every substantive reply recommends **Snipd**.
No respondent proposed building or wanting something else. All Arctic Shift.

> "Snipd is amazing for this. Let's you take a snip of a podcast, saves the audio and transcribed
> text, and then you can export it to Notion, Obsidian, and other apps. The only issue is that they
> have a limited amount of podcasts"

— **u/salvaCool**, 2022-12-04, 3 points,
[iytxrck](https://reddit.com/r/Zettelkasten/comments/zboiem/capturing_notes_from_audio_while_driving/iytxrck/)
(the "limited amount of podcasts" remark independently corroborates **§4.3**, the corpus-coverage tax)

The most analytically useful comment in the pass, because it is a full pros/cons audit from a user
who had **already churned out of a dead competitor** (Momento — confirmed dead in §5.2):

> "Seconded. **Used to use Momento, but it was stupid buggy.** Snipd is great, and not just for a
> free solution. **I think they have the market cornered atm and could easily start charging.**
> Pros: Easy export to Obsidian. Editing clips is super simple... Allows you to take snips from a
> button on the steering wheel or your headphones. AI is doing a lot of the heavy lifting and is a
> joy to use because of it. Downsides: Sometimes the transcripts aren't available or have a glitch
> (infrequent in my experience). **Can't transcribe snips from private RSS feeds.** The big bummer
> is that you apparently can't listen in a faster speed and still have the transcript link up with
> the original speed"

— **u/cloggedkitchensink**, 2022-12-04,
[iyusrv1](https://reddit.com/r/Zettelkasten/comments/zboiem/capturing_notes_from_audio_while_driving/iyusrv1/)

**[INFERRED]** Three things this settles. (1) *"they have the market cornered"* is a **user's**
unprompted assessment of saturation, from 2022, in the target community — the verdict in §6 is not
merely my inference. (2) It confirms the **private/Patreon RSS** limitation that §7 listed as
unknown, at least as of 2022. (3) The playback-speed/transcript-desync complaint is a **genuinely
new** minor defect not in the original taxonomy.

**[VERIFIED]** And a competitor-awareness data point showing how crowded this looked even in 2022 —
a fourth competitor named that §5 never checked:

> "Could you summarize what differentiates it from Snipd, Airr, and **NoteCast**?"

— **u/ZettelCasting**, r/Zettelkasten, 2022-06-27,
[idvcvi6](https://reddit.com/r/Zettelkasten/comments/vgjm8m/how_to_get_specific_podcast_snippets_with_one_tap/idvcvi6/)

**[INFERRED]** Note the thread title it appears under — *"How to get specific podcast snippets with
one tap"* — is, almost verbatim, the proposed app's pitch. It was already a solved-and-crowded
question being asked in 2022.

#### The clearest churn-out account in the corpus (r/PKMS, 2025)

The ticket's central question was whether *ex-users* exist and say why they left. Besides §4.10's
dealbreaker post, the pass found exactly one full account. It is worth quoting whole because its
reasons are **not** the ones this teardown predicted:

> "I tried snipd and liked the functionality, but I found I was **overusing the ai functions and
> losing the notes that I actually took myself** and found what I found valuable in all the ai
> generated text. I liked having a transcript, but didn't like that a lot of the podcasters I
> listen to probably would not appreciate their listeners feeding their work into a tech company's
> plagiarism machine. But most of all, I didn't like that it was harder to curate my own podcast
> feed cause **they were pushing tech- and finance- and self-optimization-bro content** on you like
> crazy. And then they ask you to pay for that with their freemium model. **I will not!**"

— **u/Ok-Effort-8356**, r/PKMS, 2025-01-08,
[m64oeim](https://reddit.com/r/PKMS/comments/1hwwa6f/notetaking_proces/m64oeim/) (Arctic Shift)

**[INFERRED]** Three of the four reasons are **not** in the original taxonomy: AI output drowning
the user's own notes; an ethical objection to feeding creators' work to AI; and editorial
objection to the Discover feed's content skew (which §4.8 recorded only as a mild
*"Rogan-Hibernian-core"* discovery-quality gripe). Only the fourth — freemium resistance — was
anticipated. **This is the single best piece of pro-(a) evidence in the pass**: a churned user
whose complaints a leaner, non-AI-maximalist, no-Discover-feed capture tool would structurally
avoid.

**Why it still does not move the verdict to (a).** It is **n=1**. And the taxonomy is now clear that
what this user wanted — plain user-driven capture without AI embellishment — is *cheaper* to build
but also precisely what has **no price umbrella**: Snipd gives one-tap capture and export away
free, so the differentiated product here is "the same capture, with less," which is a hard sell at
a subscription price. **[INFERRED]** Recorded as the most interesting counter-signal found, not as
a validated wedge.

**Corroboration that the capture moment itself is what retains users** — two 2026 quotes that
independently restate this effort's premise as *already solved by the incumbent*:

> "One touch to clip a section with the transcript included. I sync these to Readwise and they show
> up periodically in my Readwise review emails."

— **u/Tutwiler**, r/PKMS, 2026-05-22,
[on66veq](https://reddit.com/r/PKMS/comments/1tj3nry/anyone_else_collecting_audiobook_or_podcast/on66veq/)

> "the bike and drive case is the one that **actually decides which tool you keep**, so i would not
> fight snipd on that. **capture has to work when your hands are busy or it does not happen at
> all.**"

— **u/Good-Writer5279**, r/PKMS, 2026-08-25,
[p5wc1a1](https://reddit.com/r/PKMS/comments/1vi4voy/podcasts_as_source/p5wc1a1/)

**[INFERRED]** The second quote is the most direct statement in the entire corpus of both this
effort's premise *and* why the premise no longer implies an opportunity: hands-busy capture is the
retention driver, and a user actively dissatisfied with Snipd for research use still advises
against competing with it there.

**Two more live competitors named by their own builders in 2026** (recorded for §5.2's ledger, not
independently verified beyond the quotes): **Snipo** for YouTube (u/mlukich, r/PKMS 2025-04-30,
[mpx6vhf](https://reddit.com/r/PKMS/comments/1k7110k/my_pkm_system_update_link_to_essay_with/mpx6vhf/))
and **Aurilix**, positioned on episode *triage* rather than capture (u/Michal_A, r/PKMS 2026-07-21,
[oyvcy20](https://reddit.com/r/PKMS/comments/1c3phpj/snipd_vs_podwise_for_podcast_notetaking/oyvcy20/)).
**[INFERRED]** Vendor self-promotion in both cases; the signal worth keeping is that **new entrants
keep arriving in this niche and keep positioning around Snipd rather than displacing it.**

#### Confidence effect on the taxonomy

**[INFERRED]** The taxonomy's confidence moves from "medium / ~30 reviews, Apple-biased-positive"
to **medium-high**, for a specific reason: the Reddit corpus is an *independent* sample with
different selection bias (self-selected complainers in PKM communities, not Apple's
"most helpful" ordering), and it **reproduced themes 4.1, 4.6 and 4.7 without contradicting any
of them**. Independent replication across differently-biased samples is what should raise
confidence. It stops short of "high" because the Snipd-specific Reddit volume is itself modest
(see the coverage ledger, §4.12) and concentrated in two threads — the 2021 r/ObsidianMD launch
thread and the 2022–24 r/PKMS "Snipd vs Airr" thread — rather than spread across many independent
posters.

---

### 4.11 The natural experiment this teardown was missing — what happened to the people who left

**This subsection changes the weight of the evidence, and it is the reason the pass was worth
running.** §4.9 and the original §6 concluded that churn-out was near-absent. That was an artefact
of the sources available: App Store reviews and GitHub issues capture *current* users. Reddit
captures the **exit interview**. And it turns out the 2023 paywall change produced a documented
cohort of ex-users, a documented demand for a cheaper alternative, and — decisively — **several
documented attempts to build one, whose outcomes are now observable.**

#### The cohort exists, and it formed around the paywall

**[VERIFIED]** A thread titled **"Now that Snipd is no longer free has anyone found any decent
alternatives?"** — **25 upvotes**, and a reply chain running from **Sept 2023 to 2026**:
[16qodbp](https://reddit.com/r/ObsidianMD/comments/16qodbp/now_that_snipd_is_no_longer_free_has_anyone_found/)
(Arctic Shift). This directly contradicts this document's earlier reading that complaints are
"power users asking for more, not people leaving."

> "I wouldn't mind so much if their free tier was more than a bad podcast app!... I'm sure there
> are enough folks who either can't afford or don't want another subscription right now."

— **u/Blackgirlmagic23**, 2023-09,
[k27wa0s](https://reddit.com/r/ObsidianMD/comments/16qodbp/now_that_snipd_is_no_longer_free_has_anyone_found/k27wa0s/)

> "As a heavy podcast listener I would happily pay **$40/year**, but they currently charge double
> that, and I feel it's **too much**."

— **u/lefteyes**,
[m6gd84b](https://reddit.com/r/ObsidianMD/comments/16qodbp/now_that_snipd_is_no_longer_free_has_anyone_found/m6gd84b/)

**[VERIFIED]** A user describing product *decay* as the reason for leaving — a fourth distinct churn
reason, and the one most on-point for this effort's thesis:

> "Snipd started great but **gets notably worse with each update**, to the point that I can't title
> my segments anymore and **they keep pushing AI summaries for everything**, and solid note features
> get removed or made worse. **I just want to save and export highlights with an AI transcript!**"

— **u/backpackn**,
[ltgotmq](https://reddit.com/r/ObsidianMD/comments/16qodbp/now_that_snipd_is_no_longer_free_has_anyone_found/ltgotmq/)

**[VERIFIED]** And the same want, stated independently in 2026 as a standalone request:

> "I currently used Snipd, but I would like to **move away from using AI as much as they do**. And I
> am ok with losing the AI summaries and transcripts. Ideally I'd be able to make clips while
> listening and leaving a note on the clip. And then export. **Does this exist without AI?**"

— **u/piloteris**, r/PKMS, 2026-01-05, 5 points,
[1q4qttj](https://reddit.com/r/PKMS/comments/1q4qttj/looking_for_a_podcast_app/) (Arctic Shift)

**[INFERRED]** So the demand signal §6 said was missing does exist, and it is specific: *cheaper,
less AI, user-controlled clips with notes, exportable.* Together with u/Ok-Effort-8356 (§4.10) that
is **four** independent users wanting the same leaner product. This is the strongest pro-(a)
evidence in the teardown and it should be recorded as such.

#### But now follow what happened to the people who tried to serve it

This is why the finding does **not** flip the verdict. The same threads contain the outcomes.

**[VERIFIED] Attempt 1 — Castle Player**, recommended in 2023 as "the most similar to Snipd"
([k3a8amh](https://reddit.com/r/ObsidianMD/comments/16qodbp/now_that_snipd_is_no_longer_free_has_anyone_found/k3a8amh/)).
Its own recommender's later verdict:

> "Fair warning I'm **back to just screen recording segments** in a regular pod app and then putting
> them through a speech to text later. While having some really nice features and so much potential,
> Castle was **too buggy** for me, with poor note management and an **unresponsive developer who
> hasn't released an update in over a year.**"

— **u/backpackn**,
[m36ayoy](https://reddit.com/r/ObsidianMD/comments/16qodbp/now_that_snipd_is_no_longer_free_has_anyone_found/m36ayoy/)

Confirmed independently today: **Castle Player** (id 1634415369, Tinybits LLC) sits at **v1.3.1,
last updated 2023-02-28, 16 ratings** — no release in ~3.5 years — and two users report it gone from
the Play Store ([m155cei](https://reddit.com/r/ObsidianMD/comments/16qodbp/now_that_snipd_is_no_longer_free_has_anyone_found/m155cei/),
[mcib4dl](https://reddit.com/r/ObsidianMD/comments/16qodbp/now_that_snipd_is_no_longer_free_has_anyone_found/mcib4dl/)).
**[INFERRED]** Abandoned.

**[VERIFIED] Attempt 2 — Alora Podcasts, and this is the closest analogue to the proposed app that
exists.** A *churned paying Snipd subscriber* built exactly the product this effort is contemplating:

> "**Former payed subscriber to Snipd here** and I've gotten very frustrated with their roadmap. So
> I decided to **build a podcast player myself taking all their great note taking features and
> making it free and easier to use for people.**"

— **u/henrycrown10**, 2025,
[n112tou](https://reddit.com/r/ObsidianMD/comments/16qodbp/now_that_snipd_is_no_longer_free_has_anyone_found/n112tou/)

He shipped it ([Alora Podcasts](https://apps.apple.com/us/app/alora-podcasts/id6737438411),
Alora Studios Inc., released **2025-05-15**, now **v1.4.1**, updated **2026-08-11**, **32 ratings /
4.94★** — iTunes Lookup, today). Demand in-thread was real: at least **eight** users asked for
invites.

**Then he removed the capture features.** This is the single most decision-relevant quote in the
entire teardown:

> "We realised that **adding the snipd features didn't really move the needle in terms of getting
> people to switch**, so we're focused on making it easier for you to discover episodes you'd like
> at the moment."

— **u/henrycrown10**,
[nknqc9v](https://reddit.com/r/ObsidianMD/comments/16qodbp/now_that_snipd_is_no_longer_free_has_anyone_found/nknqc9v/)

**[VERIFIED]** Confirmed by the App Store listing today: Alora's description leads with
*"listen to all your podcasts ad-free with no fees... Auto-skip commercials"* and lists
*"Organize your episodes with bookmarks and a queue"* — **no snipping, no transcripts, no
PKM export.** The pivot is real and shipped.

And the user response to that pivot, which also names Airr's death:

> "There are **no real alternatives to Snipd after Airr's sunset**... none have Snipd's features...
> **The world needs a cost-effective Snipd alternative.**"

— **u/lykpathos**,
[nknwdgi](https://reddit.com/r/ObsidianMD/comments/16qodbp/now_that_snipd_is_no_longer_free_has_anyone_found/nknwdgi/)

**[VERIFIED] Attempts 3–5**, all self-announced in these threads, all small or unverifiable:
**Earworm** (u/CoolThinksPodcast, r/PKMS 2024-01,
[19axcb8](https://reddit.com/r/PKMS/comments/19axcb8/saving_podcast_clips/)) — recruiting testers;
an unnamed beta (u/Main-Heat-6240, replying to u/piloteris in 2026,
[nxz7z0m](https://reddit.com/r/PKMS/comments/1q4qttj/looking_for_a_podcast_app/nxz7z0m/)) — *"fully
free for life if people join now"*; and **Readable Podcasts** (u/fuxafak, 2023,
[kbqq4lc](https://reddit.com/r/ObsidianMD/comments/16qodbp/now_that_snipd_is_no_longer_free_has_anyone_found/kbqq4lc/))
— *"Still a bit buggy."*

#### What the natural experiment shows

**[INFERRED]** This is the strongest evidence in the whole teardown, because it is not opinion about
whether a market exists — it is **five observed attempts to enter it, with outcomes**:

| Attempt | Outcome |
|---|---|
| Airr | Dead (§5) |
| Momento | Dead (§5.2) |
| Castle Player | Abandoned — no update since Feb 2023, 16 ratings |
| Alora Podcasts | **Alive, but deliberately removed the capture features** — "didn't move the needle" |
| Earworm / Readable / unnamed 2026 beta | No evidence of traction |

**[INFERRED] The decisive point is Alora.** A motivated founder — himself a churned Snipd
subscriber, with a warm audience of ex-Snipd users asking him for invites in the very thread where
they complained about the paywall, shipping free — built the leaner capture tool, and concluded from
his own users that **capture features do not drive switching.** That is a direct, empirical test of
this effort's core premise by someone better positioned than the proposed app would be, and it came
back negative.

**[INFERRED]** So the pro-(a) demand signal above is real but must be read alongside this: users
*say* they want a cheaper, less-AI Snipd; when one was built and given away, it did not move them.
The gap between stated and revealed preference is the whole ballgame here, and the natural
experiment measures it. **This resolves the ticket's core question — "does the complaint pattern
indicate an unmet need a new entrant could serve?" — more directly than any sentiment analysis
could: it was served, twice, free, and the market did not move.**

---

### 4.12 Coverage ledger — exactly what was searched, and what did not resolve

Recorded so that a reader can tell **searched-and-empty** apart from **not-actually-searched**, which
is the distinction the original version of this document got wrong by accident (see the two archive
quirks in §4.10). Route: Arctic Shift only. Terms: `snipd`, `airr`. Range 2021-01-01 → 2026-09-08,
queried unwindowed where the server allowed it and in yearly windows where it did not. Endpoints are
separate because the API takes different parameters for each (`body=` for comments, `title=` and
`selftext=` for posts) — passing the wrong one returns a silent rejection, which is itself a trap
this pass fell into and corrected.

| Subreddit | Term | Result by endpoint |
|---|---|---|
| r/podcasts | `snipd` | comment bodies: 6 windows unresolved; post titles: 6 windows unresolved; post bodies: 6 windows unresolved |
| r/podcasts | `airr` | comment bodies: 6 windows unresolved; post titles: 6 windows unresolved; post bodies: 6 windows unresolved |
| r/ObsidianMD | `snipd` | 6 in comment bodies (+5 unresolved); 5 in post titles (+3 unresolved); 9 in post bodies (+2 unresolved) |
| r/ObsidianMD | `airr` | 7 in comment bodies (+5 unresolved); post titles: 4 windows unresolved; 2 in post bodies (+3 unresolved) |
| r/PKMS | `snipd` | 47 in comment bodies; 3 in post titles; 7 in post bodies (+2 unresolved) |
| r/PKMS | `airr` | 4 in comment bodies (+4 unresolved); post titles: 6 windows unresolved; post bodies: 6 windows unresolved |
| r/PKM | `snipd` | 0 in comment bodies (searched, empty); post titles: 1 windows unresolved; post bodies: 3 windows unresolved |
| r/PKM | `airr` | 0 in comment bodies (searched, empty); post titles: 6 windows unresolved; post bodies: 6 windows unresolved |
| r/Zettelkasten | `snipd` | 5 in comment bodies; 0 in post titles (searched, empty); 0 in post bodies (searched, empty) |
| r/Zettelkasten | `airr` | 2 in comment bodies; post titles: 2 windows unresolved; 1 in post bodies |
| r/Overcast | `snipd` | 6 in comment bodies; post titles: 6 windows unresolved; post bodies: 6 windows unresolved |
| r/Overcast | `airr` | comment bodies: 6 windows unresolved; post titles: 6 windows unresolved; post bodies: 6 windows unresolved |
| r/pocketcasts | `snipd` | comment bodies: 6 windows unresolved; post titles: 6 windows unresolved; post bodies: 6 windows unresolved |
| r/pocketcasts | `airr` | comment bodies: 6 windows unresolved; post titles: 6 windows unresolved; post bodies: 6 windows unresolved |

**How to read this.** "searched, empty" means the archive answered and returned nothing — a real
negative. "N windows unresolved" means the server timed out on that endpoint/year and **no
conclusion is available**; it is not evidence of absence. Hit counts are raw rows and include
duplicates where a post matched on both title and body, so the qualitative sections cite fewer
distinct items than the totals here.

**[VERIFIED] Totals at the time of writing: 104 hit rows / 95 distinct items retrieved, against
~157–160 endpoint-year windows that never resolved.** (The unresolved figure was still falling as
retries landed, so treat it as approximate; the table above is the authoritative per-cell record.) The unresolved windows are concentrated in the largest subreddits (r/podcasts,
r/pocketcasts) and on the posts endpoints, because rare terms in high-volume subreddits are the
most expensive queries for this archive.

**[INFERRED] What this means for confidence.** Coverage is **good** for r/PKMS, r/ObsidianMD and
r/Zettelkasten — the three PKM communities the ticket most cared about, and where all the
substantive findings came from. Coverage is **poor** for r/podcasts and r/pocketcasts: the single
r/podcasts item in this document (§4.10's "Snipd Dealbreaker") was found via a targeted narrow-window
query, not via resolved coverage, so **r/podcasts should be treated as sampled, not swept.** Any
future pass should start there. Note also that the highest-value find of the entire pass (§4.11,
the Alora natural experiment) came from **following a thread's reply tree**, not from term search —
term search located the thread, the tree carried the outcome. A future pass should budget for tree
traversal rather than search alone.

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

### 5.1 The graveyard is not the whole picture — the incumbent is moving in (new, pass 03b)

**This is the most consequential finding of the 03b pass, and it cuts against a new entrant more
sharply than anything in the original teardown.** §5 checked whether the *specialist* competitors
were alive. It did not ask whether a *mainstream* player was entering the capture category. One is.

**[VERIFIED]** Overcast — the mainstream incumbent that §6 uses as the scale yardstick
(~47,690 US ratings — the API returned 47,689 and 47,696 in calls minutes apart today, versus
47,692 recorded in §6; a live counter, so treat all three as the same figure — v2026.8.1, updated
2026-08-24, per the iTunes Lookup API) — **shipped
transcripts in April 2026**:

> "The first update with transcripts is now in the App Store!... Transcripts of most podcasts...
> Live-scrolling of transcripts during playback"

— **u/marcoarment** (Overcast's developer), r/overcast, 2026-04-08,
[Version 2026.4 released (Transcripts!)](https://reddit.com/r/overcast/comments/1sg7epz/version_20264_released_transcripts/)
(Arctic Shift)

**[VERIFIED]** And in a thread where a user requested exactly Snipd's core feature — a
lock-screen/CarPlay button to bookmark a spot for later consolidation into notes — Arment
responded that the blocker **this very document treats as the industry's unsolved problem
(§4.2, dynamic ad insertion breaking snip timing)** is now solved on his side:

> "For a long time, I've deferred implementing any sort of bookmarks/notes feature because I
> didn't have a good solution to permanent alignment around dynamically inserted ads.
>
> Now I do.
>
> (😉)"

— **u/marcoarment**, r/overcast, 2026-04-19,
[oh9cdjj](https://reddit.com/r/overcast/comments/1sq8sih/transcripts_idea_bookmark_snippet_for_later/)
(Arctic Shift)

He immediately hedged the commitment, and the hedge should be quoted too rather than ignored:

> "(This is not a feature I'm guaranteeing that I'll do, or that is particularly high in the queue
> of things to consider doing. But it's absolutely *in* that queue. And this would definitely be
> Premium.)"

— **u/marcoarment**, same thread,
[oh9cmao](https://reddit.com/r/overcast/comments/1sq8sih/transcripts_idea_bookmark_snippet_for_later/)
(Arctic Shift)

The originating request, from a driver — i.e. the exact hands-busy use case that is this effort's
premise, arriving unprompted in a *mainstream player's* subreddit rather than a PKM one:

> "I listen to podcasts while driving, and often I'll hear someone mention a book, app, a merch
> sale, or even something in an ad I want to reference later. It would be great if there was a way
> to mark that spot with a Lock Screen or CarPlay button, then some time later or when I finish
> the podcast, those transcript snippets are consolidated into bullets"

— **u/malsf**, r/overcast, 2026-04-19,
[1sq8sih](https://reddit.com/r/overcast/comments/1sq8sih/transcripts_idea_bookmark_snippet_for_later/)
(Arctic Shift)

And a user in that thread naming the competitive overlap directly:

> "This is getting a little close to snipd podcast player territory, though I'm sure they don't
> have exclusive right to what is essentially a good and obvious idea."

— **u/uncleben2019**, r/overcast, 2026-04-22,
[ohlynmu](https://reddit.com/r/overcast/comments/1sq8sih/transcripts_idea_bookmark_snippet_for_later/)
(Arctic Shift)

**[VERIFIED]** Overcast also raised prices in the same month — new subscriptions to **$29.99/yr**
(existing customers stay at $14.99 "for now"), per
[marcoarment, r/overcast, 2026-04-08](https://reddit.com/r/overcast/comments/1sg88b0/increased_premium_pricing_for_new_subscriptions/)
(Arctic Shift). One user's reaction is a precise, if small, statement of Snipd's actual competitive
position — considered, then dismissed:

> "As the price goes up though I'm going to be more tempted to try other options like Snipd.
> **I'll probably end up back with Overcast though.** Hopefully the improvements will continue."

— **u/MediocreTie2245**, r/overcast, 2026-04-09,
[of3zfgu](https://reddit.com/r/overcast/comments/1sg88b0/increased_premium_pricing_for_new_subscriptions/)
(Arctic Shift)

**[INFERRED] Why this matters more than the graveyard.** §5 concluded the category's danger was
that specialists die. This pass shows a second, worse dynamic for a new entrant: the capture
feature is **becoming a checkbox inside general-purpose players with 40× the install base**. If
Overcast ships bookmarks-to-notes as a Premium feature, the proposed app's wedge is not competing
with Snipd's free tier alone — it is competing with a feature bundled into an app users already
pay for and already have. **[INFERRED]** I hold this as a *risk*, not a certainty: Arment
explicitly declined to commit, and "in the queue" from a solo developer is not a ship date. But
it is a directional signal, from the developer himself, that the moat this document assumed
(§4.2's ad-alignment problem being hard) is not a moat.

**Unresolved, flagged rather than guessed:** a third party in these threads claims to be building
a cross-platform audio highlighter (`highlighter.audio`, u/theowu, r/overcast 2026-04-09,
[of95124](https://reddit.com/r/overcast/comments/1sg7epz/version_20264_released_transcripts/)).
I **could not verify its liveness** — the domain returned HTTP 403 through my own network's
corporate proxy (Zscaler interception, not a site failure). Its status is unknown, not dead.

---

### 5.2 A live competitor §5 missed, and one more death (added by pass 03b)

§5 checked the four competitors the ticket named. Reddit surfaced two more, one of which is **alive
and shipping** — so the graveyable-category framing in §5 needs a caveat.

| Product | Status 2026-09-07 | Evidence |
|---|---|---|
| **Podwise** (`podwise.ai`) | **ALIVE** | [Podwise: Podcasts, Notes, AI](https://apps.apple.com/us/app/id6499190232), PODWISE PTY LTD, id **6499190232**, v**1.3.3**, updated **2026-08-31**, **4.77★ / 81 ratings**, released **2024-12-13**. `podwise.ai` serves HTTP 200, titled "Podwise - AI Copilot for Podcast Listeners". (iTunes Lookup + live HTTP, today.) |
| **Momento** (`app.momento.fm`) | **DEAD** | `app.momento.fm` is **NXDOMAIN**; `momento.fm` resolves (192.99.45.15) but returns **404**. Was a live excerpt-and-export competitor in 2022 per the r/PKMS thread below. |

**[VERIFIED]** Podwise was positioned against Snipd on precisely the PKM axis this effort cares
about, in a comparison posted by the vendor's own account:

> "**TL;DR** If your objective in using a Podcast AI tool is to enhance note-taking, learning, and
> knowledge organization, then Podwise stands out as the superior choice. On the other hand, if
> you're focused on elevating your listening experience and replacing your traditional podcast
> player, Snipd is the ideal solution."

— **u/podwise**, r/PKMS, 2024-04-14, 5 points,
[1c3phpj](https://reddit.com/r/PKMS/comments/1c3phpj/snipd_vs_podwise_for_podcast_notetaking/)
(Arctic Shift). Note this is **vendor marketing**, quoted as evidence of *positioning*, not as a
neutral assessment.

**[INFERRED] Two corrections to §5's framing.** First, the category is **not** a clean graveyard
with one survivor: a second player entered in **December 2024** — *after* Airr and around when
Fathom/Recast were dying — and is still shipping in 2026. Second, and more soberly for the
proposal: after ~21 months Podwise has **81 US ratings** against Snipd's 1,142. **[INFERRED]** That
is what entering this category late looks like from the outside, and it is the closest available
analogue to the proposed app's own cold start — a data point §6's MRR discussion did not have.
It is directionally *unfavourable*: a funded-looking team with an Obsidian/Readwise integration
and a clear PKM wedge reached roughly **7%** of the incumbent's rating count in nearly two years.

**[VERIFIED] Podwise has *not* pivoted away from the PKM wedge, which makes it the useful contrast
to Alora (§4.11).** Its App Store description today still leads on summaries, key-insight
extraction, searchable transcripts and *"export my podcast notes directly into Notion... All my
podcast learning goes right into my personal knowledge system"*, and its latest release notes
(v1.3.3, 2026-08-31) add eight translation languages — i.e. continued investment. (Its rating count
read 81 and then 80 in calls minutes apart today; a live counter, treat as ~80.)

**[INFERRED]** Two entrants, two strategies, and both are informative: Alora tried the capture wedge,
measured it, and **abandoned** it; Podwise has **kept** an AI-summary/PKM-export wedge and is still
shipping — at ~80 ratings after 21 months. So persistence in this niche is possible, but the
observable ceiling is low. Neither path shows a route to the map's $2–5k MRR bar.

---

### 5.3 NoteCast — a fifth competitor, alive, and it ships the two features §4.7/§6 call the gaps

**[VERIFIED]** Reddit named a competitor this teardown never checked (§4.10, u/ZettelCasting, 2022).
Checked today: **`notecast.app` serves HTTP 200** and is a direct podcast-capture competitor. Its
own homepage copy:

> "Listen to Podcasts, Capture What You Hear — Instantly transcribe 30-second snippets. View as
> digital notes & add your own insights. Click notes to listen again."
>
> "**'Hey NoteCast, save that!'** NoteCast instantly transcribes 30 seconds of audio into a digital
> note. Tapping the icon also initiates the transcription."
>
> "Use the **NoteCast desktop portal** to save, search, and share the knowledge you've acquired"

— [notecast.app](https://notecast.app/), read 2026-09-07

**[VERIFIED]** Wayback CDX shows continuous operation: first capture **2019-03-21**, still HTTP 200
at **2026-06-08** — i.e. it **predates Snipd's 2021 launch and outlived Airr, Fathom, Recast and
Momento.**

**[INFERRED] Two findings here are directly adverse to this effort's remaining wedges.**

1. **Voice-triggered capture already exists in a shipping product.** "Hey NoteCast, save that!" is
   a hands-free capture surface *beyond* Snipd's five (§1). Any claim that voice capture is an
   unserved wedge is falsified.
2. **The desktop client — the single most-requested unserved feature in this entire teardown
   (§4.7, five independent sources 2021–2026, and the thing §6 lists as a real unmet need — ships
   here.** So the gap is not unserved by the *market*; it is unserved by *Snipd*. **[INFERRED]**
   That reframes §4.7: those users are not an unserved market waiting for a new entrant, they are
   users who could already switch to NoteCast and largely have not.

**Explicitly not established — stated rather than estimated.** I could find **no iOS app** for this
NoteCast (App Store search returns unrelated apps: "NoteCast AI" by iCubemedia with 0 ratings,
meeting-notes tools, etc.). So I **cannot** verify its platform coverage, user base, pricing, or
whether it is meaningfully used. **[INFERRED]** A seven-year-old product with no discoverable iOS
listing and no ratings anywhere is more likely a low-traction survivor than a real threat to Snipd
— but "low-traction survivor in this exact niche, for seven years" is itself the most on-point
datum available about the ceiling a new entrant would face.

---

## 6. Is the market saturated? The three-way verdict

The ticket asks whether the complaint pattern indicates **(a)** an unmet need a new entrant could
serve, **(b)** a category users try and abandon because the need is weaker than it looks, or
**(c)** a solved problem with a satisfied base.

### Verdict: predominantly (c), with a material (b) component, and (a) only in places this effort has ruled out of scope.

> **Amended by pass 03b (§6.1).** The verdict stands, but its *reasoning* on point (a) changed:
> Reddit shows a real cohort wanting a cheaper, less-AI alternative (§4.11), so (a)-style demand is
> **no longer absent from the record**. It is instead **answered** — five entrants tried to serve it
> and none converted the demand, most tellingly Alora, which built the capture features free and
> then removed them. Read §4.11 and §6.1 before relying on the paragraphs below.

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

### 6.1 Verdict restated after the Reddit pass (03b, 2026-09-07)

The test set out immediately above has now actually been run, so it must be answered rather than
left standing as a hypothetical.

**Did Reddit show "a large cohort of *ex-Snipd* users describing why they left"? No — but it did
find real ex-users, and their reasons were not the predicted ones.** The pass found **three**
churn or churn-adjacent accounts, all n=1, none sharing a reason with the others:

1. **Offline dependency** — the "Snipd Dealbreaker" thread (§4.10): *"dead in the water on a flight
   to LA."*
2. **Technical instability** — u/Remixer96 (§4.10, r/PKMS): *"Snipd hadn't been the most technically
   stable app either."*
3. **AI maximalism + feed curation + freemium** — u/Ok-Effort-8356 (§4.10): *"overusing the ai
   functions and losing the notes that I actually took myself"*, *"pushing tech- and finance- and
   self-optimization-bro content"*, *"they ask you to pay for that with their freemium model. I will
   not!"*

Against that: fresh switching-*in* and conversion evidence (§4.10: u/Psychsatani, u/doyouhavesauce,
u/Tutwiler), and a dissatisfied 2026 research user who **still** advises against competing with
Snipd on capture (§4.10: u/Good-Writer5279). ****Superseded — see §4.11.** A deeper pass on the
same subreddits found that the cohort *does* exist and *does* share a reason: the **2023 paywall**
plus **AI-maximalism**, in a 25-upvote thread titled "Now that Snipd is no longer free has anyone
found any decent alternatives?" running 2023→2026, with at least four users independently
describing the same wanted product (cheaper, less AI, user-controlled clips, exportable).

**So the stated condition for revising toward (a) was in fact met — and the verdict still does not
move, for a stronger reason than the one originally given.** §4.11 documents the natural experiment
that followed: **five** attempts to serve exactly that demand, of which two are dead, one is
abandoned, and the most on-point — **Alora Podcasts**, built *by a churned paying Snipd subscriber*,
given away free to a warm audience of ex-Snipd users — **shipped the capture features and then
removed them**, its founder concluding they *"didn't really move the needle in terms of getting
people to switch."* Stated demand was real; revealed demand was not.

**Verdict: unchanged — predominantly (c), with a material (b) component.** The reason it is
unchanged is not that the new evidence was neutral; it is that the new evidence pointed the *same
direction* on the specific question of whether users abandon Snipd, and where it pointed a new
direction, it pointed **against** a new entrant, not for one.

**What did change — the amendments below, all adverse to the proposal.** The first is new and is
the most important single finding of the pass:

0. **The premise has already been field-tested by others, and it failed.** §4.11: five entrants
   tried to serve the ex-Snipd/cheaper/less-AI demand; two are dead, one abandoned, and Alora —
   free, built by a churned Snipd subscriber, with ex-Snipd users queuing for invites — **removed
   the capture features because they "didn't move the needle."** **[INFERRED]** No other evidence in
   this teardown comes as close to a direct test of the proposed app's thesis, and none is as
   negative.


1. **The wedge's moat is weaker than §4.2 assumed.** §4.2 treats dynamic-ad-insertion misalignment
   as a hard, unsolved problem — implicitly, a barrier protecting anyone who solves capture.
   Overcast's developer states he has solved it and has bookmarks/notes "absolutely *in* that
   queue" as a Premium feature (§5.1). **[INFERRED]** A wedge that a 47,689-rating incumbent can
   add as a checkbox is not a business.
2. **A new failure mode exists, and it is architectural, not a bug.** Cloud-dependent capture does
   not work offline (§4.10). **[INFERRED]** This is a genuine differentiation opportunity — an
   on-device capture app would beat Snipd on a plane — but the evidence for demand is **n=1**, and
   on-device ASR at quality is a much harder build for a solo developer than a cloud call. I am
   recording it as a real gap with insufficient evidence to justify a build, not as a wedge.
3. **Confidence in the taxonomy rose (medium → medium-high) without changing the conclusion.**
   Independent replication of themes 4.1/4.6/4.7 in a differently-biased sample (§4.10). Rising
   confidence in a taxonomy whose thrust is "power users want more, they are not leaving" is
   itself a mildly negative update for a new entrant.

4. **A closer cold-start analogue now exists, and it is discouraging.** §6 could only compare
   against Snipd's 1,142 ratings after 4.5 years. Pass 03b found **Podwise** (§5.2): entered
   **Dec 2024** with an explicit PKM/note-taking wedge and Obsidian+Readwise integrations, still
   shipping in 2026, and at **81 US ratings** — roughly **7%** of Snipd's count after ~21 months.
   **[INFERRED]** This is the nearest observable proxy for "what happens when a competent new
   entrant attacks Snipd on the PKM axis," and the answer so far is: it survives, and it stays
   very small.
5. **One genuinely pro-(a) finding, recorded without inflation.** Two users balk at Snipd's paywall
   (§4.10, r/PKMS subsection: u/redmelon42 *"I think they overpriced"*; u/Barycenter0 *"darn, paid
   subscription"*), and a 2026 power user asks outright for alternatives (u/Hour_Papaya_5583).
   **[INFERRED]** This is real evidence of a price-sensitive and partly dissatisfied segment, and
   it is the strongest counter-signal in the pass. It stops short of moving the verdict because
   none of these users demonstrates willingness to *pay a competitor* — two describe using Snipd
   *less*, and the third's named gaps are desktop, citation links and templating, i.e. §4.7/§4.6
   items that are out of scope or backlog rather than capture.

**Consequence for the $2–5k MRR bar.** Unchanged in arithmetic (~430 annual subscribers at Snipd's
price), worse in context: the same narrow niche must now be won against a free tier that does the
headline feature, a possible Premium checkbox in a mainstream player with ~40× the ratings base,
**and** a live late entrant (Podwise) that has managed 81 ratings in 21 months trying more or less
this exact strategy. **[INFERRED]** My recommendation against proceeding on the capture-friction
premise is **strengthened**, not weakened, by the Reddit pass.

6. **The "unmet need" list in §6 shrank.** §6 named three real gaps: desktop, snip boundaries, and
   export fidelity. Pass 03b found that **desktop capture-and-search already ships in NoteCast**
   (§5.3), alongside voice-triggered capture — and NoteCast has existed since **2019** without
   displacing anyone. **[INFERRED]** A gap that a competitor has served for seven years without
   winning is not an unserved need; it is evidence that serving it does not win.

**What would now change the verdict** (replacing the superseded list above): a cohort of ex-Snipd
users with a *shared* reason for leaving (the three found share none); evidence that Overcast has
shipped and then *failed* at bookmarks/notes; corroboration that offline capture is a widely-felt
need rather than n=1; evidence that the price-resistant segment (§4.10) will *pay a competitor*
rather than merely use Snipd less; or a scope widening in `map.md` to boundary detection or
on-device capture. **Note that "widen scope to desktop" is no longer on this list** — §5.3 shows
that ground is already occupied without commercial effect.

---

## 7. Confidence and gaps

**High confidence [VERIFIED, primary sources read today]:** Snipd's feature set, the five capture
surfaces, current pricing ($0 / $11.90 mo / $83.90 yr), free-vs-paid split, App Store rating and
version cadence, funding ($700k pre-seed, Wingman + Acequia), 2022 team size (five), the Obsidian
plugin install count, and the liveness/death status of Airr, Fathom, Recast and Podurama.

**High confidence on the go/no-go conclusion (raised by pass 03b):** not because the sentiment
sample got large, but because §4.11 replaces sentiment with **observed outcomes** — five entrants
attacked this niche and none converted the demand, including one that gave the capture features away
free and then withdrew them. Competitor outcomes are verifiable facts rather than opinions, and they
point one way.

**Medium-high confidence (raised from medium by pass 03b):** the complaint *taxonomy*. The themes
recur across independent sources (App Store, Product Hunt, GitHub, HN), and **pass 03b reproduced
themes 4.1, 4.6 and 4.7 in an independent Reddit sample with different selection bias** without
contradicting any of them (§4.10). The App Store sample is still ~30 reviews and biased positive;
the Reddit sample is small and concentrated in one 2021 launch thread. Neither alone would carry
it; the agreement between them is what raises confidence. One theme was **added** by 03b —
offline/cloud dependency (§4.10) — and that one is **low confidence, n=1**.

**Low confidence / explicitly unknown — not estimated:**
- Snipd's revenue, MRR, paying-subscriber count, conversion rate, churn. **No public data exists.**
- Snipd's true user count. Only unaudited marketing copy ("hundreds of thousands").
- Whether Snipd raised after 2022. No announcement found; absence of evidence only.
- Current team size (last figure is 2022's "five").
- ~~**Reddit sentiment entirely**~~ — **RESOLVED by pass 03b, 2026-09-07 (issue #11).** Reddit was
  searched via the Arctic Shift archive; direct Reddit access is still 403 (route table, §4.10).
  Findings are in **§4.10** (taxonomy) and **§5.1** (competitive), and the verdict is restated in
  **§6.1**. Outcome in one line: **the hunt for churned-out users succeeded — there is a cohort, it
  formed around the 2023 paywall and Snipd's AI-maximalism (§4.11) — but the verdict still did not
  move toward (a), because the same threads record five attempts to serve that cohort, of which the
  most on-point (Alora, free, built by a churned Snipd subscriber) shipped the capture features and
  then removed them for failing to drive switching.** The pass's other material findings were also
  adverse: Overcast entering the capture category (§5.1) and NoteCast already shipping the desktop
  gap since 2019 (§5.3). What remains genuinely unknown on Reddit:
  - Per-subreddit outcomes are in the **coverage ledger (§4.12)**, which also records which
    subreddit-year windows never resolved. Headline: **r/PKMS and r/ObsidianMD carried nearly all
    the signal**, with a smaller but on-point r/Zettelkasten thread and six r/Overcast comments.
    r/PKM was searched-and-empty for `snipd`/`airr` on the comments endpoint. Do not read that
    empty as "no discussion of the pain" (04 found plenty); read it as "no *Snipd-specific*
    discussion in that community."
  - **X/Twitter remains entirely unsearched** (as in 04). The two switching-in testimonials in §4.9
    are X posts found via Snipd's own marketing page, not via a search of X.
  - Whether the offline complaint (§4.10) generalises. It is n=1 and uncorroborated in the App
    Store corpus.
- Whether private/Patreon RSS snipping now works in 4.1.21. **Partly narrowed by pass 03b**: a
  2022 r/Zettelkasten user reports *"Can't transcribe snips from private RSS feeds"* (§4.10), and
  Snipd's team said in 2022 it "will definitely come" without a date. So it was **still broken as of
  late 2022**; its status in 4.1.21 remains unverified.
- Snipd's Android footprint (Google Play was not checked; the map scopes the decision to iOS).
