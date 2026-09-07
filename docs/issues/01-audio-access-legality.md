# 01 — What audio access is legally permissible from Spotify, YouTube Music, Apple Podcasts, and open RSS?

Type: research
Status: resolved
Blocked by: —

## Question

This is the make-or-break ticket. The concept requires capturing **the preceding N seconds of
audio** from a podcast the user is already listening to. Establish what is permissible under the
actual developer terms of each source — not what is technically achievable by circumvention.

Answer specifically:

- For **Spotify** (iOS SDK / Web API / Web Playback SDK): does any surface expose the decoded
  audio stream, or PCM buffers, to a third-party app? Quote the Developer Terms of Service and
  SDK documentation clauses that govern recording, caching, downloading, or derivative works.
  Note the known restriction that Spotify's iOS SDK is a *remote-control* SDK requiring the
  Spotify app to be installed, and confirm or refute that.
- For **YouTube Music**: is there any third-party playback SDK at all? Cover the YouTube API
  Services Terms of Service clauses on separating audio from video, downloading, and caching.
- For **Apple Podcasts**: is there a playback SDK or only deep links? Can a third-party app
  observe or capture what Apple Podcasts is playing?
- For **Pocket Casts** and other third-party players: any public API? Any usable integration?
- For **open RSS podcast feeds**: what does direct access to the enclosure audio URL permit? Is
  clipping and storing a 30-second excerpt defensible, and under what theory (fair use /
  fair dealing, ephemeral copy, user-side processing)? Note that this is a legal-risk assessment,
  not legal advice, and flag where a lawyer would be required.
- **Publisher transcripts**: is the podcast `<podcast:transcript>` RSS tag in meaningful use?
  What coverage does it actually have in the top N shows?

Then state clearly: **which of these four capture mechanisms survive** —
(a) full audio clip from the played stream,
(b) re-fetch the public audio file by timestamp and clip locally,
(c) transcript-only capture with no audio,
(d) timestamp bookmark with a deep link back to the source.

Distinguish verified (quoted terms) from inferred throughout.

## Answer

Full findings with verbatim clause quotes and URLs:
[research/01-audio-access-legality.md](../research/01-audio-access-legality.md)

**Not legal advice.** Legal-risk assessment. §8 of the research file lists four questions that
require a lawyer.

### Headline

There is **no legitimate technical surface** on Spotify, YouTube Music, or Apple Podcasts that
hands decoded audio to a third-party app — and even if there were, each platform's terms
independently prohibit capture. The concept's core mechanic (grab the preceding N seconds of what
the user is already listening to) only exists inside **your own player playing open RSS audio**.

### Per source

- **Spotify** — VERIFIED remote-control only. The iOS SDK "offload[s] complexity to the main
  Spotify application such as: playback, authentication, networking, and offline caching" and
  requires the Spotify app installed; the ticket's premise is confirmed. No PCM/audio surface in
  either the iOS SDK or the Web Playback SDK (control + metadata only; web playback runs through
  browser encrypted-media). ToS IV.2.b.iii bars facilitating "stream ripping" or functionality that
  helps users "capture or otherwise make permanent copies"; VI.5 obliges developers to *help
  Spotify pursue* such capture. IV.3.b bars local caching of Spotify Content beyond metadata/cover
  art or Premium-only time-limited offline sync. Developer Policy separately bars any product
  "integrated with streams or content from another service" — INFERRED fatal to a multi-source app.
- **YouTube Music** — NO third-party playback SDK found. Developer Policies III.E.1(a) bars
  "download, import, backup, cache, or store copies"; III.I.7 bars acting to "separate, isolate, or
  modify the audio or video components"; III.I.9 bars background players; III.I.14 bars non-API
  routes to the content. Redundantly dead.
- **Apple Podcasts** — no playback SDK, no now-playing observation. `MPNowPlayingInfoCenter` is
  write-only ("An object for setting the Now Playing information for media that your app plays").
  ReplayKit captures only "audio that originates from the app" and the microphone. Apple
  auto-generates transcripts since iOS 17.4 and ingests the RSS transcript tag, but NO EVIDENCE
  FOUND of any API exposing those to third parties — it's competition, not infrastructure.
- **Pocket Casts / other players** — NO EVIDENCE FOUND of any public API. Not exhaustively
  surveyed; stated as a gap.
- **Open RSS** — no ToS layer at all. The binding constraint is **copyright, and it is
  unresolved**. Fair use (17 U.S.C. §107) is plausible but unsettled: amount favours the developer
  (30s of 60min), market effect favours them, but nature-of-work weighs against and the
  "heart of the work" doctrine bites hard because a capture app *systematically selects for the
  qualitatively substantial moment*. Best theory is user-side private copying, not ephemeral copy.
  UK/EU is weaker ground than the US (private-copying exception note flagged UNVERIFIED).
- **App Store Guideline 5.2.3** is the sharpest operational blade: apps must not "include the
  ability to save, convert, or download media from third-party sources ... without explicit
  authorization from those sources", and "Authorization must be provided upon request." Broad
  enough on its face to reach open-RSS clipping. 2.5.14 additionally forces a visible/audible
  indicator for any rolling capture buffer — which damages the invisible-capture UX.
- **`<podcast:transcript>`** — VERIFIED the tag exists, is spec-locked, and Apple ingests it.
  **Coverage question UNANSWERED**: every Podcast Index stats endpoint returned 403. I did not
  estimate a number. Two structural reasons to expect worse coverage than headline feed
  percentages: Apple's auto-transcripts remove publisher incentive, and the biggest shows are
  disproportionately not in open RSS. A one-afternoon direct measurement (fetch top 100–200 feeds,
  count the tag) should precede pricing mechanism (c).

### Four-mechanism verdict

| | Mechanism | Verdict |
|---|---|---|
| (a) | Full audio clip from the played stream | **Dead** on all three platforms — prohibited by name *and* technically unavailable. Survives only in your own player over open RSS, with live copyright + 5.2.3 exposure. |
| (b) | Re-fetch public audio by timestamp, clip locally | **Survives for open RSS only.** Solves the *platform-terms* problem, NOT the copyright problem — a retained reproduction is a retained reproduction. Unavailable for Spotify/YouTube (no public file); for Apple Podcasts the file is reachable but the playback position is not. |
| (c) | Transcript-only, no audio | **Survives**, best legal posture of the capturing options, sidesteps 5.2.3. But coverage is unmeasured, it still requires being the player to know the position, and the ASR fallback collapses back into (b). |
| (d) | Timestamp bookmark + deep link | **Survives everywhere, zero meaningful exposure.** Spotify's policy actively requires link-backs. Degrades to episode-level on Apple Podcasts (no position available). |

### The uncomfortable structural finding

Legal safety and product value are **inversely correlated** across (a)→(d). (d) is clean precisely
because it captures nothing — the user still has to come back and re-listen, which is the problem
the concept exists to solve. Everything with real value sits in unresolved copyright territory.

And the one architecture that survives — *be the podcast player, over open RSS* — is already
occupied. Snipd (SECONDARY, vendor site) does exactly this: its own player plus YouTube/Libro.fm/
file imports, headphone-tap snip producing "audio, transcript, and summary". It never mentions
Spotify or Apple Podcasts. That is convergent evidence the legal analysis above is correct, and
also that the surviving variant means competing head-on with a funded incumbent rather than
entering an empty space.

