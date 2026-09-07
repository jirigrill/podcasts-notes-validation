# Map: Podcast idea-capture app — go/no-go

Label: `wayfinder:map`

## Destination

A **go/no-go decision** the developer will act on: build / build-narrower / don't build the
iOS podcast idea-capture app, with the reasoning, the surviving concept variant (if any), and
the explicit MRR arithmetic behind it. The decision is the deliverable — not a spec, not code.

## Notes

- **Domain**: consumer iOS productivity / PKM tooling; podcast ecosystem; indie subscription apps.
- **Skills every session should consult**: `/grilling`, `/domain-modeling`. Research tickets use
  the `/research` subagent.
- **Standing preferences for this effort**:
  - The developer asked explicitly for **rigour, not encouragement**. Counter-validate. The
    original brief was written in the app's own marketing voice and asserted false premises
    (e.g. "today the only options are stopping to type or losing the idea" — Snipd, Airr and
    Overcast clips exist). Do not inherit that framing.
  - **Distinguish verified from inferred** in every answer. Where evidence is absent, say so
    rather than producing a plausible-sounding number.
  - **Success bar is $2–5k MRR** — the developer's own stated bar, not a floor.
  - Developer is **solo with no audience**: no newsletter, no social following, no existing app
    with users, no PKM-community presence. All funnel arithmetic must assume cold start.
  - Legal compliance is a **constraint to discover, not to route around**. The question is what
    is permissible under actual developer terms, not what is technically achievable.
  - Research findings are written to `.scratch/podcast-capture-app/research/<name>.md` and
    linked from the ticket. Not a git repo, so no research branches.

## Decisions so far

<!-- one line per resolved ticket: gist + link -->

- [01 — What audio access is legally permissible](issues/01-audio-access-legality.md) — The
  "connects to your existing podcast accounts" premise is **dead**. No PCM access on Spotify
  (remote-control SDK only), no YouTube Music SDK, no Apple Podcasts SDK. Only surviving
  architecture is *be the player, over open RSS*. Hardest blocker is App Store Guideline 5.2.3
  (no saving media from third-party sources without authorization) — a gate, not just contract
  risk. Legal safety and product value are inversely correlated across the four mechanisms.
- [02 — Is friction-free capture achievable on iOS?](issues/02-ios-capture-surfaces.md) —
  **Near-zero-friction claim does not survive.** Best surface is `ControlWidgetButton` +
  `AppIntent` (`.background`) — one impl covers Control Center, Lock Screen and Action Button,
  fires without launching or Face ID — but real friction is 2–3 actions, phone out, ~2–4s. The
  killer isn't the button: no iOS API captures another app's audio, so the app must *be* the
  player. AirPods are a dead end (no third-party gesture API). Two good findings: `bookmarkCommand`
  is a documented intended-use fit (but its iOS 26 rendering is undocumented — cheapest
  high-value experiment available), and background execution is **not** a blocker.
- [03 — Snipd teardown](issues/03-snipd-teardown.md) — **The idea is already built, and the capture
  moment is free.** Snipd ships headphone triple-tap, steering-wheel button, lock-screen widget,
  Shortcuts, Watch/CarPlay + Notion/Readwise/Obsidian export at $0. Pricing $11.90/mo, $83.90/yr,
  flat 20 months. 4.7★/1,142; users churn *into* it from Overcast and stay; one logged 8,582 snips
  in a year. Not price resistance — the reverse (*"would pay double, maybe triple"*). Saturation
  verdict: predominantly **(c) solved**, with material **(b)** — Airr, Fathom, Recast all dead, and
  a 2022 HN post proposing near-exactly this map's narrow variant got 5 points, zero replies, and
  nobody built it in four years. Real soft spots are **boundary accuracy** (adjusting start/end
  defeats the no-open-the-app premise), dynamic-ad-insertion drift, corpus quota tax, export
  fidelity, and **no web/desktop** — but web/desktop and boundary detection are both already
  ruled out of this map's scope.
- [04 — Demand evidence](issues/04-demand-evidence.md)
- [05 — Wider competitive landscape and the incumbent-feature threat](issues/05-competitive-landscape.md)
  — **Nothing durable.** Decisive: **Pocket Casts shipped the concept's core loop on 3 Sep 2026** —
  "Smart Bookmarks: save the words, not the timestamp", with deliberate look-back windowing, free
  tier to $39.99/yr, ~14x Snipd's ratings, Automattic-backed. Apple Podcasts already ships
  share-a-moment-from-transcript free on 2.07M ratings. **3 of 4 dedicated competitors are dead**
  (Airr delisted, Fathom Mar 2025, Recast late 2024). Of nine candidate differentiators, five have
  already evaporated, two are one API call away, one is occupied; only PKM export is structurally
  safe — and its flagship has 578 ratings after five years. Adjacent categories that *worked*
  (Granola, Voicenotes, AudioPen) all capture speech you **produce**, not speech you consume. — Pain is **real but tiny in volume**. Best
  ever "does an app do this?" post in r/podcasts: 7 upvotes. Acute segment is PKM/Obsidian users
  (students and language learners produced *zero* evidence). Counter-evidence is serious: the
  target segment itself reports **~10% of captures ever revisited** and concludes capture was
  never the bottleneck; **Airr is dead** (App Store 404) and nobody noticed; WTP points at
  Readwise as the paid destination with the podcast app as unpaid feeder. No TAM produced — three
  funnel fractions have no source, so it was declined rather than invented.
- [06 — Transcription and hosting unit economics](issues/06-unit-economics.md) — Cost is **not** a
  blocker: clip-only transcription (~$0.002/user/mo, ~100% GM) works at every price point, and
  clip-only is what saves the economics rather than on-device. Whole-episode + OpenAI Whisper is
  unviable (typical user loses money at $5/mo). At the $2–5k MRR bar total COGS is under $12/mo.

## Not yet specified

- **Which concept variant to price and spec**, if the legal path forces a retreat to RSS-only,
  transcript-only, or bookmark-and-re-fetch. Can't sharpen until 01 lands. The variants likely
  differ enough in cost and audience that each may need its own arithmetic.
- **Whether a non-podcast adjacent wedge is stronger** — e.g. the same capture moment applied to
  audiobooks, lectures, YouTube, or meetings. Only worth charting if the podcast verdict is
  marginal rather than clearly negative.
- **Distribution strategy**, if the verdict is build. Deliberately downstream of the go/no-go:
  charting it now would presume the answer.
- **What the developer's alternative use of the time is.** Named as a gap: a "don't build"
  verdict is only meaningful against an alternative, and that alternative hasn't been surfaced.
  Likely a grilling ticket once the arithmetic is visible.

## Out of scope

- **Android, web, and desktop clients.** The destination is an iOS decision.
- **Building any part of the app.** This map produces a decision; execution is a separate effort.
- **The "smart boundaries" roadmap** (last paragraph / last exchange / last topic). A v2 feature
  premised on v1 demand that hasn't been established. Ruled out of this effort's scope.
