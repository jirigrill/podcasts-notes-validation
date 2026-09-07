# 01 — Audio access legality: Spotify, YouTube Music, Apple Podcasts, RSS

Research for ticket `issues/01-audio-access-legality.md`. **Not legal advice.** Legal-risk
assessment from primary sources only. Every line is tagged VERIFIED (read in a primary source,
URL given) or INFERRED (my reasoning from those sources) or NO EVIDENCE FOUND.

## Verdict up front

| Mechanism | Verdict |
|---|---|
| (a) Full audio clip from the played stream | **Dead** on Spotify, YouTube Music, Apple Podcasts. Only survives inside your own player playing open RSS audio. |
| (b) Re-fetch public audio file by timestamp, clip locally | **Survives for open RSS only.** Copyright exposure remains, unresolved by ToS. |
| (c) Transcript-only capture, no audio | **Survives** where a transcript is legitimately obtainable — which is a much narrower set than it sounds. |
| (d) Timestamp bookmark + deep link | **Survives everywhere.** Also the least valuable. |

Strongest blocker: there is **no legitimate technical surface** on any of the three big platforms
that hands decoded audio to a third-party app, and the terms independently prohibit capture even
if one existed. Apple App Review Guideline 5.2.3 makes this an App Store gate, not just a
contractual risk.

## 1. Spotify

### 1a. Technical surface — does anything expose decoded audio?

VERIFIED — the iOS SDK is a remote-control SDK, confirming the ticket's premise. Spotify's iOS
landing page describes it as letting your app "offload complexity to the main Spotify application
such as: playback, authentication, networking, and offline caching", lists "Always-in-sync
Playback (via the Spotify main application)", and states "A physical iOS device is needed to
install the Spotify app". Your app must obtain "the user's permission to control playback remotely
first". Source: https://developer.spotify.com/documentation/ios

VERIFIED (by absence) — that page never mentions raw audio, PCM, sample buffers, or file access.
The documented surface is playback control plus "subscribing to player state changes".

VERIFIED — the Web Playback SDK is likewise control + metadata. It is described as "a client-side
only JavaScript library designed to create a local Spotify Connect device in your browser, stream
and control audio tracks from Spotify inside your website and get metadata about the current
playback." The documented API surface is connect/disconnect/pause/resume/togglePlay/seek/
prev/next/volume/getCurrentState plus events and metadata objects. No API returns decoded audio.
Source: https://developer.spotify.com/documentation/web-playback-sdk

VERIFIED — the same page states the SDK "require iframes to allow encrypted-media and autoplay in
cases of cross origin iframes", i.e. playback runs through browser EME/DRM.

INFERRED — because playback is rendered inside Spotify's own process (iOS) or the browser's EME
pipeline (web), there is no supported path for a third-party app to obtain the PCM buffer. Any
route to audio would be circumvention, which the ticket explicitly excludes from scope.

### 1b. Terms of Service — the clauses that matter

All from https://developer.spotify.com/terms

VERIFIED — anti-ripping clause, IV.2.b.iii, prohibits SDAs that facilitate "stream ripping" or
other functionalities that make it easier for users to "capture or otherwise make permanent
copies" of streamed content. This is the direct, on-point prohibition. Mechanism (a) is barred by
name.

VERIFIED — VI.5 goes further: developers agree to assist Spotify in pursuing violations of "the
prohibition against ripping or other capture of streamed content." A developer is affirmatively
obliged to help police the exact behaviour the concept requires.

VERIFIED — IV.3.a.i: "you may not store, aggregate or create compilations or databases of Spotify
Content, other than as strictly necessary to operate your SDA". Combined with the instruction not
to store Spotify Content indefinitely.

VERIFIED — IV.3.b: "Do not locally cache any Spotify Content, except as strictly necessary to
enhance the performance of your SDA". Permitted caching is limited to metadata and cover art, or
"Conditional Downloads of sound recordings" defined as time-limited offline syncing and restricted
to Premium subscribers. A permanently retained 30-second clip is not time-limited offline syncing.

VERIFIED — IV.2.a.ii bars "modifying, editing, altering, creating derivative works, disassembling,
decompiling, reverse-engineering, or extracting source code".

VERIFIED — IV.2.a.i bars "using the Spotify Platform or any Spotify Content to train a machine
learning or AI model". Relevant if the concept intends to run captured audio through an ASR or
summarisation model. Whether inference-only use counts as "training" is genuinely ambiguous on
the face of the text — **a lawyer would be needed here**, and Spotify's own reading is the one
that matters commercially.

VERIFIED — IX.8.g: on termination you must "delete all Spotify Content (including Spotify Personal
Data)" obtained via the Platform. INFERRED: a user's permanently-kept clip library cannot survive
Spotify revoking your access, which undermines the product promise even if capture were allowed.

VERIFIED — Developer Policy (https://developer.spotify.com/policy):
- "Do not create any product or service which is integrated with streams or content from another
  service." INFERRED: this alone is fatal to the multi-source premise — a single app that unifies
  capture across Spotify plus YouTube plus RSS appears to be precisely what this forbids.
- "Do not synchronize any sound recordings with any visual media".
- "Do not permit any device or system to segue, mix, re-mix, or overlap any Spotify Content with
  any other audio content".
- "there shall be no playback of Spotify Content without showing relevant cover art and metadata
  in your SDA".
- Audio Preview Clips (30-second previews available via the Platform, per ToS II.2) are heavily
  fenced: "You must not offer Audio Preview Clips as a standalone service or product" and they
  "may only be used to promote the underlying content and not for personalization or messaging
  products", and each "must be accompanied by a link back to the applicable content".

INFERRED — the Audio Preview Clip surface is worth naming explicitly because it is the only
Spotify-sanctioned 30-second audio object, and it is *not* usable here: previews are a fixed
promotional excerpt of a track chosen by Spotify, not an arbitrary window of the user's current
listening position, and the standalone-product ban blocks a clip-library app.

**Spotify verdict.** VERIFIED-grounded: (a) prohibited by name and technically unavailable.
(b) not applicable — there is no public audio file URL to re-fetch. (c) NO EVIDENCE FOUND that
Spotify's API exposes podcast transcripts to third parties; I could not locate any Spotify Web API
transcript endpoint in the developer docs. (d) survives: playback position is available via player
state, and deep-linking back to Spotify is the sanctioned pattern.

## 2. YouTube Music

VERIFIED (by absence) — NO EVIDENCE FOUND of any third-party playback SDK for YouTube Music. What
exists is the YouTube IFrame/Player API for *video* embeds and the YouTube Data API for metadata.
I found no YouTube Music developer SDK in Google's developer documentation.

All quotes below from the YouTube API Services Developer Policies,
https://developers.google.com/youtube/terms/developer-policies

VERIFIED — III.E.1(a): API clients must not "download, import, backup, cache, or store copies of
YouTube audiovisual content without YouTube's prior written approval". III.E.1(b) bars making
content "available for offline playback". This kills (a) and (b) outright.

VERIFIED — III.I.7 prohibits acting to "separate, isolate, or modify the audio or video components
of any YouTube audiovisual content" provided through the API services. This is the single most
on-point clause for the whole concept: extracting an audio clip from a YouTube item is separating
the audio component, prohibited whether or not you store it.

VERIFIED — III.I.8 bars promoting the audio or video components "separately".

VERIFIED — III.I.9 bars playing content "from a background player", described as one "not displayed
in the page, tab, or screen that the user is viewing". INFERRED: this is fatal to the ambient
"you're already listening, we're capturing in the background" UX for YouTube sources.

VERIFIED — III.I.14 bars using "any technology other than YouTube API Services" to reach API Data,
including any part of YouTube audiovisual content. INFERRED: this closes the yt-dlp-style route as
a terms matter, not merely a technical one.

VERIFIED — III.E.6 bars scraping YouTube properties or obtaining scraped data.

VERIFIED — YouTube API Services Terms of Service §16.3: "no rights or licenses are granted to
reproduce or distribute audiovisual content or make audiovisual content available in any manner".
Source: https://developers.google.com/youtube/terms/api-services-terms-of-service

VERIFIED — §24.3: on termination "you will immediately stop accessing and using all YouTube
Property and delete all YouTube API Services (including all API Data)", with certification of
deletion available on demand.

**YouTube Music verdict.** (a) and (b) prohibited explicitly and redundantly. (c) transcript-only:
YouTube caption tracks are API Data reachable via the Data API `captions` resource, but
`captions.download` is restricted to the video owner — INFERRED from the general structure of the
API and III.E.4's treatment of API Data; I did **not** find a clause explicitly permitting
third-party retention of caption text for arbitrary videos, so treat transcript capture from
YouTube as unresolved rather than permitted. (d) deep link with timestamp (`&t=`) survives and is
the intended pattern.

## 3. Apple Podcasts

VERIFIED (by absence) — NO EVIDENCE FOUND of any Apple Podcasts playback SDK, remote-control
framework, or now-playing-observation API available to third-party apps. Apple's public media
frameworks cover *your own* playback and the Apple Music library, not Podcasts.

VERIFIED — `MPNowPlayingInfoCenter` is a write-only publishing API. Apple's abstract: "An object
for setting the Now Playing information for media that your app plays." The overview describes
contributing your own track information so the system can display it on the Lock Screen and
Control Center. Nothing in the documentation offers reading another app's now-playing state.
Source: https://developer.apple.com/documentation/mediaplayer/mpnowplayinginfocenter

INFERRED (important correction to a common assumption) — Control Center's ability to show any
app's now-playing item comes from Apple's private MediaRemote framework. I did **not** find an
Apple primary source documenting a public equivalent, and I did not find a primary source stating
App Store rejection for MediaRemote use — that claim circulates on developer forums and I am
labelling it SECONDARY/UNVERIFIED rather than asserting it.

VERIFIED — ReplayKit captures only the recording app's own audio and the microphone.
`RPSampleBufferType.audioApp` is documented as "The sample audio that originates from the app" and
`.audioMic` as "The sample audio that originates from the microphone." There is no system-audio or
other-app-audio case. Sources:
https://developer.apple.com/documentation/replaykit/rpsamplebuffertype and
https://developer.apple.com/documentation/replaykit/rpscreenrecorder/startcapture(handler:completionhandler:)
Both are marked deprecated at 27.0 in favour of ScreenCaptureKit's `SCStream`.

INFERRED — the microphone route ("hold the phone near the speaker") is not a real workaround:
podcast listening is overwhelmingly via headphones, so there is no acoustic signal to capture, and
it would additionally be an unauthorised recording of the work.

VERIFIED — Apple auto-generates transcripts and ingests publisher ones: "Apple automatically
generates transcripts after a new episode is published", and "If you choose to provide your own
transcripts, we will ingest them via your RSS feed using the RSS transcript tag" (VTT or SRT).
Availability iOS 17.4+, listed languages, 170+ countries; "Episodes over 10 hours long may not be
transcribed"; private RSS feeds are not processed. Source:
https://podcasters.apple.com/support/5316-transcripts-on-apple-podcasts

INFERRED — these transcripts live inside the Apple Podcasts app. NO EVIDENCE FOUND of any API
exposing Apple-generated transcripts to third-party apps. So Apple's transcript feature does not
help mechanism (c); it is competition, not infrastructure.

**Apple Podcasts verdict.** (a) technically impossible via public API. (b) partially available —
Apple Podcasts is an RSS aggregator, so for public shows the underlying enclosure URL is
independently reachable; but you cannot learn the user's playback position inside Apple Podcasts,
which is the piece the concept actually needs. (c) unavailable via API. (d) deep links exist
(`podcasts.apple.com` / `podcast://`), but INFERRED: you cannot construct a *timestamped* bookmark
without knowing the position, so even (d) degrades to an episode-level link.

## 4. Pocket Casts and other third-party players

NO EVIDENCE FOUND of a public Pocket Casts developer API. The Pocket Casts marketing site contains
no mention of an API or developer integrations — navigation covers plans, advertising, podcaster
resources, blog, forums, help centre and apps only (https://www.pocketcasts.com/). The support
knowledge-base URL I tried for an API article returned 404. Pocket Casts is open-source in part
(github.com/Automattic/pocket-casts-ios), but INFERRED: an open-source client is not an integration
surface for a separate app.

I did not exhaustively survey every third-party player. Overcast, Castro and Snipd were not checked
for developer APIs beyond the note below. **Gap, stated plainly.**

SECONDARY / vendor marketing — Snipd (https://www.snipd.com/) is the closest existing product and
is instructive about the shape of the only viable architecture. Verbatim from its site: "Just tap
your headphones whenever you hear something worth remembering. Our AI creates a snip for you with
audio, transcript, and summary." Its listed sources are its own podcast player plus "Import YouTube
Videos", "Import Audiobooks from Libro.fm", and "Upload Any Audio File". The page never mentions
Spotify or Apple Podcasts. INFERRED: Snipd solved the legal problem by *being the player* over open
RSS, not by integrating with the incumbents. That is strong convergent evidence that (a)-via-
third-party-platform has no path, and it also means the surviving variant is already occupied by a
funded incumbent.

## 5. Open RSS feeds

VERIFIED — the RSS `<item><enclosure>` audio URL is a plain HTTP resource; fetching it is what
every podcast client does. No developer terms of service governs it, because there is no platform
in between.

**This is the crux, and the honest answer is: ToS is not the binding constraint here — copyright
is, and it is unresolved.**

VERIFIED — 17 U.S.C. §107 sets four fair-use factors: "the purpose and character of the use"
(including commercial vs nonprofit educational), "the nature of the copyrighted work", "the amount
and substantiality of the portion used in relation to the copyrighted work as a whole", and "the
effect of the use upon the potential market for or value of the copyrighted work". Source:
https://www.law.cornell.edu/uscode/text/17/107

INFERRED, factor by factor, for a 30-second private clip retained in a personal notes app:
- Purpose/character: private, non-public, note-taking, arguably transformative if the clip is
  embedded in the user's own notes. But the *app* is commercial (subscription). Courts assess the
  defendant's use; a paid tool whose value derives from others' content is a weaker position than
  a private individual doing the same thing.
- Nature of the work: creative/expressive audio. Weighs against.
- Amount: 30 seconds of a 60-minute episode is quantitatively trivial. But the "heart of the work"
  doctrine cuts the other way precisely because users will clip the *most valuable* moments — the
  insight, the punchline, the key argument. Substantiality is qualitative, not just quantitative,
  and a note-capture app systematically selects for the qualitatively substantial part.
- Market effect: private retention plausibly has no market effect and may drive listening. This is
  the strongest factor for the developer.

INFERRED — a fair-use theory here is *plausible but not settled*. I found no case law directly on
user-initiated retention of short podcast excerpts in a commercial notes app. Anyone who tells you
this is "obviously fine because it's 30 seconds" is asserting something the statute does not say.

INFERRED — the stronger framing is **user-side processing / private copying**: the clip is created
on the user's device, from a file the user is already lawfully fetching, stored only for that user,
never redistributed. Under this framing the developer is a tool provider, not a copier. Betamax-
style substantial-non-infringing-use reasoning supports tool provision. **This is exactly the
question a lawyer must answer** — and note that Betamax-style protection has historically been
weakest where the tool's primary marketed purpose is capture.

INFERRED — "ephemeral copy" is the weakest of the three theories and I would not lean on it: the
product promise is that the clip *persists* in your notes. Ephemeral-copy doctrines protect
transient technical copies incidental to a lawful process, not durable user libraries.

**Jurisdiction gap, stated plainly.** Fair use is US. The UK/EU equivalent is fair dealing plus
specific exceptions, and there is **no general fair-dealing exception for private copying of sound
recordings in the UK** — the private-copying exception introduced in 2014 was quashed by the High
Court in 2015. I am flagging this from general knowledge and did **not** verify it against a
primary source in this pass; treat as UNVERIFIED and material. If it holds, an EU/UK launch is on
weaker ground than a US-only one, which matters for App Store territory strategy.

VERIFIED — Apple App Store Review Guideline 5.2.3: "Apps should not facilitate illegal file sharing
or include the ability to save, convert, or download media from third-party sources (e.g. Apple
Music, YouTube, SoundCloud, Vimeo, etc.) without explicit authorization from those sources.
Streaming of audio/video content may also violate Terms of Use, so be sure to check before your app
accesses those services. Authorization must be provided upon request." Source:
https://developer.apple.com/app-store/review/guidelines/

This is the single most operationally dangerous clause in this document. INFERRED: it is broad
enough on its face to reach a feature that saves an audio excerpt from an RSS enclosure, because
the podcast publisher is a "third-party source". "Authorization must be provided upon request"
means the developer can be asked at any time, post-launch, to produce permission — and cannot.
Whether reviewers actually apply 5.2.3 to open RSS clipping is an empirical question about App
Review behaviour that I could not resolve from primary sources. Snipd's continued presence on the
App Store is SECONDARY evidence that clipping open RSS audio does pass review in practice, but
review outcomes are not precedent and can change.

VERIFIED — Guideline 5.2.2: "If your app uses, accesses, monetizes access to, or displays content
from a third-party service, ensure that you are specifically permitted to do so under the service's
terms of use. Authorization must be provided upon request." INFERRED: this independently forecloses
any Spotify/YouTube integration of type (a) or (b), since those terms demonstrably do not permit it.

VERIFIED — Guideline 2.5.14: "Apps must request explicit user consent and provide a clear visual
and/or audible indication when recording, logging, or otherwise making a record of user activity.
This includes any use of the device camera, microphone, screen recordings, or other user inputs."
INFERRED: a rolling always-on buffer of the last N seconds is a compliance design problem, not just
a legal one — it needs a persistent, visible recording indicator, which damages the "invisible,
frictionless" UX the concept depends on.

## 6. Publisher transcripts — the `<podcast:transcript>` tag

VERIFIED — the tag exists and is specified in the Podcast Namespace. It is "used to link to a
transcript or closed captions file", sits inside `<item>`, and may repeat once per format.
Attributes: `url` (required, "URL of the podcast transcript"), `type` (required, "Mime type of the
file such as `text/plain`, `text/html`, `text/vtt`, `application/json`", plus
`application/x-subrip`), `language` (optional), and `rel` (optional; `rel="captions"` marks the file
as closed captions "regardless of what the mime type is", with timing data presumed). Source:
https://github.com/Podcastindex-org/podcast-namespace/blob/main/docs/tags/transcript.md

VERIFIED — the namespace spec is at `https://podcastindex.org/namespace/1.0` with prefix `podcast`,
resource URLs must be `https:`, and the 1.0 specs "are considered locked" with backward
compatibility prioritised. Source:
https://github.com/Podcastindex-org/podcast-namespace/blob/main/docs/1.0.md

VERIFIED — Apple ingests the tag, which is the strongest signal of real-world adoption pressure:
"we will ingest them via your RSS feed using the RSS transcript tag" (VTT or SRT).
https://podcasters.apple.com/support/5316-transcripts-on-apple-podcasts

**NO EVIDENCE FOUND for the coverage question the ticket asks.** I attempted
`stats.podcastindex.org`, `podcastindex.org/stats`, and the Podcast Index stats API endpoints; all
returned 403 to WebFetch. **I therefore cannot tell you what fraction of feeds — or of the top N
shows — carry `<podcast:transcript>`.** I am not going to estimate it. This is a real gap and it is
load-bearing for mechanism (c): transcript-only capture is only a product if coverage among the
shows the target user actually listens to is high, and that is unmeasured here.

INFERRED — two structural reasons to expect coverage to be *worse* than the raw feed percentage
suggests, both worth testing directly:
1. Apple auto-generating transcripts *removes* the publisher's incentive to supply their own. Since
   iOS 17.4 the listener gets a transcript in Apple Podcasts regardless, so the tag is redundant for
   the publisher's main audience.
2. The biggest shows are disproportionately Spotify exclusives or partially-gated, i.e. not in open
   RSS at all, so they cannot carry the tag in a feed you can read.

INFERRED — even where a transcript URL exists, retaining and republishing chunks of it is a
copyright question in its own right, not a free pass. A transcript is a derivative work of the
episode and the publisher holds rights in it. The fair-use analysis in §5 applies to text excerpts
too, with one difference that cuts *for* the developer: quoting text is far more culturally and
legally normalised than retaining audio.

Suggested next step (not done here): pull the top 100–200 shows from a chart source, fetch their
feeds, and count `<podcast:transcript>` occurrences directly. That is a one-afternoon measurement
and it should be made before mechanism (c) is priced.

## 7. Four-mechanism verdict

### (a) Full audio clip from the played stream

**Does not survive on any third-party platform.**
- Spotify: VERIFIED prohibited by ToS IV.2.b.iii ("stream ripping ... capture or otherwise make
  permanent copies"), plus VERIFIED no technical surface exposes audio, plus VERIFIED VI.5 duty to
  help Spotify pursue such capture.
- YouTube Music: VERIFIED prohibited by Developer Policies III.E.1(a) (no "download, import, backup,
  cache, or store") and III.I.7 (no "separate, isolate, or modify the audio or video components").
- Apple Podcasts: VERIFIED no public API exposes another app's audio; ReplayKit is scoped to
  "audio that originates from the app" and the microphone.
- Own player over open RSS: **survives technically and contractually**, with unresolved copyright
  exposure (§5) and App Review 5.2.3 risk.

### (b) Re-fetch the public audio file by timestamp and clip locally

**Survives for open RSS only.** VERIFIED there is no ToS barrier for a public enclosure URL.
VERIFIED it is unavailable for Spotify and YouTube Music (no public file, and III.I.14 bars
non-API routes). For Apple Podcasts the file is reachable but INFERRED you cannot obtain the
playback position, which is the input the mechanism requires.

INFERRED — the copyright position of (b) is *no better* than (a) once the clip persists. The
distinction between "captured from the stream" and "re-fetched and clipped" is technically real but
legally thin: both produce a retained reproduction of a portion of the work. Do not treat (b) as a
compliance solution. It is a compliance solution to the *platform terms* problem only.

### (c) Transcript-only capture, no audio

**Survives, with two large caveats.**
- VERIFIED the mechanism exists in the ecosystem (`<podcast:transcript>`).
- NO EVIDENCE FOUND on coverage — unmeasured, and the ticket's coverage question is unanswered.
- INFERRED the copyright position is meaningfully better than audio: shorter, text, more clearly
  quotation-shaped, and it does not touch App Review 5.2.3 (which is about saving *media*).
- INFERRED it still requires knowing the playback position, so it inherits the same
  you-must-be-the-player constraint as (a) and (b).
- Where no publisher transcript exists, the fallback is running ASR on audio you fetched — which
  puts you straight back into (b)'s copyright posture, plus Spotify's IV.2.a.i AI-training clause if
  Spotify content were ever involved.

### (d) Timestamp bookmark + deep link back to source

**Survives everywhere, and is the only mechanism with no meaningful legal exposure.** VERIFIED:
Spotify's policy actively *requires* link-backs for preview clips; YouTube supports timestamped URLs;
Apple Podcasts has public deep links. INFERRED: on Spotify you can get position from player state,
so a timestamped bookmark is genuinely constructible; on Apple Podcasts you cannot, so it degrades
to an episode link.

INFERRED, and the developer should sit with this: (d) is legally clean precisely because it captures
nothing. A bookmark does not solve the problem the concept exists to solve — the user still has to
come back later and re-listen to find the idea. The legal safety and the product value are inversely
correlated across (a)→(d).

## 8. Where a lawyer is required

Non-negotiable, in priority order:
1. Whether retaining a user-initiated 30-second audio excerpt of a podcast, on-device, in a paid
   app, is defensible under fair use in the US — and under UK/EU law, where private copying of sound
   recordings is materially more restricted (see the UNVERIFIED 2015 quashing note in §5).
2. Whether App Store Guideline 5.2.3's "save ... media from third-party sources without explicit
   authorization" reaches open-RSS podcast clipping. This is a business-existence question, not a
   detail.
3. Whether Spotify ToS IV.2.a.i ("train a machine learning or AI model") captures inference-only ASR
   or LLM summarisation, if any Spotify surface is used at all.
4. Whether a multi-source app violates Spotify's Developer Policy "Do not create any product or
   service which is integrated with streams or content from another service."

## 9. What I could not verify

Listed explicitly so these are not mistaken for findings:
- Coverage of `<podcast:transcript>` across feeds or top shows. All Podcast Index stats endpoints
  returned 403.
- Whether YouTube's `captions.download` permits third-party retention of caption text for videos the
  client does not own. I inferred the owner restriction from API structure; I did not read a clause.
- Whether Apple actually rejects apps for using the private MediaRemote framework. Widely claimed in
  developer forums (SECONDARY), no Apple primary source found.
- Whether the UK private-copying exception's 2015 quashing is still the operative position. Asserted
  from general knowledge, not verified here.
- Whether any Spotify Web API surface exposes podcast transcripts. I found none, but I did not
  enumerate every endpoint.
- Pocket Casts', Overcast's and Castro's developer offerings beyond the absence of any API mention on
  the Pocket Casts site.
- App Review's actual behaviour toward clipping features. Snipd's App Store presence is suggestive
  (SECONDARY) but not determinative.

## Sources

Primary:
- https://developer.spotify.com/terms
- https://developer.spotify.com/policy
- https://developer.spotify.com/documentation/ios
- https://developer.spotify.com/documentation/web-playback-sdk
- https://developers.google.com/youtube/terms/api-services-terms-of-service
- https://developers.google.com/youtube/terms/developer-policies
- https://developer.apple.com/app-store/review/guidelines/
- https://developer.apple.com/documentation/mediaplayer/mpnowplayinginfocenter
- https://developer.apple.com/documentation/replaykit/rpsamplebuffertype
- https://developer.apple.com/documentation/replaykit/rpscreenrecorder/startcapture(handler:completionhandler:)
- https://podcasters.apple.com/support/5316-transcripts-on-apple-podcasts
- https://github.com/Podcastindex-org/podcast-namespace/blob/main/docs/tags/transcript.md
- https://github.com/Podcastindex-org/podcast-namespace/blob/main/docs/1.0.md
- https://www.law.cornell.edu/uscode/text/17/107

Secondary / vendor marketing (labelled as such in text):
- https://www.snipd.com/
- https://www.pocketcasts.com/

Attempted and unreachable (403/404): stats.podcastindex.org, podcastindex.org/stats,
api.podcastindex.org stats endpoints, support.pocketcasts.com knowledge-base API article,
spotify.github.io/ios-sdk, podcasters.apple.com marketing-tools article.






