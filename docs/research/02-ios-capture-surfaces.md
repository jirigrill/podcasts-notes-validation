# 02 — iOS capture surfaces: is friction-free capture actually achievable?

Research for [issues/02-ios-capture-surfaces.md](../issues/02-ios-capture-surfaces.md).
Date: September 2026. Current OS: iOS 26.

Method: Apple developer documentation fetched directly (DocC JSON where the rendered HTML did
not return body text), App Store Review Guidelines, Apple Support user guides. WebSearch was
unavailable in this environment, so secondary sources (Stack Overflow, Apple Developer Forums,
indie blogs) could NOT be consulted. **Every real-world-constraint claim that would normally
come from secondary sources is marked as a GAP below rather than asserted.** This is the main
weakness of this report and is stated plainly rather than papered over.

Labels used throughout: **VERIFIED** = stated in a cited Apple document. **INFERRED** = my
reasoning from verified facts. **GAP** = no evidence found; not filled in.

---

## 0. The finding that reframes the whole question

Before ranking surfaces, one architectural fact dominates everything:

**On iOS there is no API that lets a third-party app capture the audio another app is playing.**

- `RPScreenRecorder` records "the audio and video **inside of the app**, along with user
  commentary through the microphone." Buffer types are `.audioApp` (your own app's audio) and
  `.audioMic`. Only one app at a time may use the recorder, and "Your app can't record video
  from `AVPlayer`." Now deprecated at 27.0 in favour of ScreenCaptureKit.
  — VERIFIED, https://developer.apple.com/documentation/replaykit/rpscreenrecorder
- Core Audio process taps (`CATapDescription` — "The input stream is a mix of all of the
  specified processes' output audio") are **macOS / Mac Catalyst only**. The DocC metadata lists
  iOS 15.0 but the actual Swift and Objective-C declarations scope the class to `Mac Catalyst`
  and `macOS` only; the iOS numbers are a Catalyst version-mapping artifact.
  — VERIFIED, https://developer.apple.com/documentation/coreaudio/catapdescription
- `ScreenCaptureKit`'s `SCStream` — the replacement that *does* do per-app audio selection — is
  macOS 12.3, Mac Catalyst 18.2, and **iOS/iPadOS 27.0 (beta)**. Not shippable in September 2026
  on a current-OS iPhone.
  — VERIFIED, https://developer.apple.com/documentation/screencapturekit/scstream

**INFERRED, and this is the load-bearing inference of the whole report:** the app can only clip
audio it is itself playing. It must be the podcast player. It cannot be a "capture button that
clips whatever Overcast/Spotify/Apple Podcasts is playing." That is not a friction problem, it
is a product-scope problem — the user must switch their entire podcast listening to this app
before any capture surface matters. The 'capture moment' friction analysed below is therefore
*conditional on having already won the player slot*, which is a far larger ask than the
concept's framing admits.

The only microphone-based alternative — record ambient audio through the mic while a *different*
app plays the podcast — is defeated by routing: with AirPods, the podcast audio goes to the
AirPods speakers, not into the mic. INFERRED. And `AVAudioSession.Category.playAndRecord` is
"nonmixable" by default, so activating a recording session interrupts other audio sessions
unless `.mixWithOthers` is set. VERIFIED,
https://developer.apple.com/documentation/avfaudio/avaudiosession/category/playandrecord

Everything below assumes the app *is* the player.

---

## 1. `MPRemoteCommandCenter` — the headphone-button path

### What commands exist (VERIFIED)

`MPRemoteCommandCenter` is "An object that responds to remote control events sent by external
accessories and system controls." iOS 7.1+. Complete property list from the reference page:

| Group | Commands |
|---|---|
| Playback | `pauseCommand`, `playCommand`, `stopCommand`, `togglePlayPauseCommand` |
| Between tracks | `nextTrackCommand`, `previousTrackCommand`, `changeRepeatModeCommand`, `changeShuffleModeCommand` |
| Within a track | `changePlaybackRateCommand`, `seekBackwardCommand`, `seekForwardCommand`, `skipBackwardCommand`, `skipForwardCommand`, `changePlaybackPositionCommand` |
| Rating | `ratingCommand`, `likeCommand`, `dislikeCommand` |
| **Bookmarking** | **`bookmarkCommand`** |
| Language | `enableLanguageOptionCommand`, `disableLanguageOptionCommand` |

Source: https://developer.apple.com/documentation/mediaplayer/mpremotecommandcenter

### `bookmarkCommand` is the single most important discovery in this report

`bookmarkCommand` is an `MPFeedbackCommand`, documented as "indicating a user wants to remember a
media item." `MPFeedbackCommand`'s overview: "The shared `MPRemoteCommandCenter` object vends
feedback objects for liking, disliking, and bookmarking media items... **You might also perform
other tasks related to receiving feedback.**" It exposes `isActive`, `localizedTitle`, and
`localizedShortTitle` — i.e. **the app supplies the button's own visible label**.
VERIFIED, https://developer.apple.com/documentation/mediaplayer/mpfeedbackcommand

**INFERRED (high confidence):** "capture this moment" is a *bookmark*, semantically. Binding
`bookmarkCommand` to a clip-capture action with `localizedTitle = "Clip"` is using the API for
exactly its documented purpose, not repurposing it. This substantially de-risks the App Store
question versus hijacking `nextTrackCommand`.

### Can a command be bound to a non-playback action without rejection?

- App Store Review Guideline **2.5.4** (marked as applying to both App Store Review and
  Notarization): "Multitasking apps may only use background services for their intended purposes:
  VoIP, audio playback, location, task completion, local notifications, etc." VERIFIED,
  https://developer.apple.com/app-store/review/guidelines/
- Guideline **2.3.1**: "Don't include any hidden, dormant, or undocumented features." VERIFIED,
  same source.
- Guideline **2.5.14**: "Apps must request explicit user consent and provide a clear visual
  and/or audible indication when recording, logging, or otherwise making a record of user
  activity. This includes any use of the device camera, microphone, screen recordings, or other
  user inputs." VERIFIED, same source.

**INFERRED:** no guideline prohibits an `MPRemoteCommandCenter` handler from doing non-playback
work. The `MPFeedbackCommand` docs explicitly bless "other tasks." The real exposure is 2.3.1
(undocumented behaviour) and 2.5.14 (recording indication) — both mitigable by describing the
behaviour in App Review notes and showing a Live Activity / on-screen indicator while capturing.
Hijacking `nextTrackCommand` so that "skip forward" clips instead of skipping is a different and
worse risk: it makes a standard system control lie about what it does. Do not do that.

**GAP:** I could find no Apple documentation, and could not reach forum/Stack Overflow evidence,
on whether `bookmarkCommand` actually surfaces as a *tappable control anywhere the user can reach
without unlocking* on iOS 26 — Control Center's Now Playing view, the Lock Screen player, or
CarPlay. Historically `likeCommand`/`dislikeCommand` surfaced in CarPlay and on watchOS but not
reliably in the iPhone Lock Screen player. **This is the single highest-value unknown in the
report and must be settled by device testing before any build decision.** If `bookmarkCommand`
renders nowhere reachable, the whole "bookmark button on the Lock Screen" idea collapses and you
fall back to Control Center controls (section 4).

### The headphone remote click mapping

**GAP.** The `MPRemoteCommandCenter` reference does **not** document which physical
headphone-remote gestures map to which commands. It says only that it responds to "remote control
events sent by external accessories and system controls." I found no Apple developer document
stating "single click → togglePlayPause, double click → nextTrack, triple click → previousTrack."
That mapping is widely believed and is consistent with the AirPods user-guide behaviour in
section 2, but **I am not asserting it as VERIFIED because I could not cite it.**

What *is* verified is the AirPods side (section 2), from which the mapping can be inferred: the
user guide says press = play/pause, double = next track, triple = previous track. INFERRED that
these arrive as `togglePlayPauseCommand`, `nextTrackCommand`, `previousTrackCommand`
respectively.

**Consequence:** there is no free gesture. Every AirPods press is already spoken for by a
playback command a podcast player genuinely needs. Rebinding triple-press (previous track) is the
least-costly theft, but it is still theft of a real function, and it is exactly the 2.3.1 risk.

### Routing: only one app gets the events

`MPNowPlayingInfoCenter`'s docs never state that only one app can be the Now Playing app; the
only eligibility language is in the sample-code abstract: "Ensure your app is **eligible to
become the Now Playing app** by adopting best practices for providing Now Playing info and
registering for remote command center actions."
VERIFIED (as a quote), https://developer.apple.com/documentation/mediaplayer/mpnowplayinginfocenter
and https://developer.apple.com/documentation/mediaplayer/becoming-a-now-playable-app

**GAP:** Apple's prose documentation does not spell out the arbitration rule. The word "eligible"
implies competition and therefore exclusivity. INFERRED: remote command events go to the current
Now Playing app, which reinforces section 0 — you must be the player.

---

## 2. AirPods gestures

### What exists (VERIFIED)

From the AirPods User Guide, "Use controls and gestures with your AirPods":
https://support.apple.com/guide/airpods/use-controls-and-gestures-with-your-airpods-devb2c431317/web

| Model | Press | Double | Triple | Press & hold | Other |
|---|---|---|---|---|---|
| AirPods 1/2 | double-tap only; assignable per bud to play/pause, next, previous, or Siri | — | — | — | — |
| AirPods 3 | play/pause, answer call | next track | previous track | Siri | — |
| AirPods 4 / 4 ANC | play/pause, answer | next | previous | **configurable**: Siri, or (ANC) cycle noise modes | both stems = Live Translation; head nod/shake |
| AirPods Pro 1 | play/pause, answer | next | previous | **configurable**: Siri or ANC/Transparency | — |
| AirPods Pro 2 / Pro 3 | play/pause, answer | next | previous | **configurable**: Siri or ANC/Transparency/Adaptive | swipe stem = volume; both stems = Live Translation; head gestures |
| AirPods Max 1/2 | crown: play/pause, answer, mute | next, decline/end call | previous | Siri | crown turn = volume; mode button = ANC/Transparency |

### What is exposed to third parties

- **No third-party AirPods gesture API exists.** VERIFIED by absence: I found no AirPods gesture
  API in the AVFoundation, AVFAudio, AVKit, or MediaPlayer references. Third-party access is
  entirely indirect, via `MPRemoteCommandCenter` receiving whatever playback command the gesture
  is mapped to.
- **Press-and-hold is reserved.** It is user-configurable but only among Apple's own choices
  (Siri, or listening-mode cycling). There is no way for a third-party app to appear in that
  picker. VERIFIED from the user-guide table above.
- **Siri interception is not possible.** No API is documented for intercepting the press-and-hold
  Siri invocation. VERIFIED by absence.
- **Both-stems-held** is claimed by Live Translation on AirPods 4 ANC / Pro 2 / Pro 3. VERIFIED,
  same source. Not available to apps.

### The AirPods hardware-button API that does exist — and why it doesn't help

`AVCaptureEventInteraction` (iOS 17.2+) registers "handlers to respond to capture events from
system hardware buttons," with primary/secondary handlers. `AVCaptureEvent` has a `play(_:)`
method documented as "Plays the specified capture sound through AirPods" — so AirPods are in
scope for this API.
VERIFIED, https://developer.apple.com/documentation/avkit/avcaptureeventinteraction and
https://developer.apple.com/documentation/avkit/avcaptureevent

But the reference carries a hard blocker, quoted verbatim:

> "You can only use this API for capture use cases. The system sends capture events only to apps
> that actively use the camera. Backgrounded capture apps, and apps not performing capture, don't
> receive events."

VERIFIED. **This kills it.** A podcast app is not using the camera and is backgrounded. This is
also the API that receives the iOS 26 AirPods camera-remote stem press, meaning that headline
"AirPods can now trigger your app" feature is camera-only and unavailable here. Attempting to run
a camera session to qualify would be a 2.5.4 / 2.4.2 violation and an obvious rejection.

**GAP:** whether Apple has ever approved a non-camera use of `AVCaptureEventInteraction`. The
documentation says no; I could not check forums for exceptions. Treat as closed.

### iOS 26 AirPods recording quality (relevant but not a capture surface)

`AVAudioSession.CategoryOptions.bluetoothHighQualityRecording`, iOS 26.0+, "enables full-bandwidth
audio when the Bluetooth route supports it, such as on certain AirPods models," combinable with
`allowBluetoothHFP` as fallback, requires `AVAudioSession.Mode.default`, and — noteworthy —
**"Bluetooth high-quality recording isn't currently supported in the European Union."** The docs
also note it "may increase input latency" and recommend
`setPrefersNoInterruptionsFromSystemAlerts(_:)` while recording.
VERIFIED, https://developer.apple.com/documentation/avfaudio/avaudiosession/categoryoptions/bluetoothhighqualityrecording

Relevant only if the concept retreats to voice-memo-style capture. The EU exclusion is a real
constraint worth noting for a solo indie whose early adopters skew EU.

---

## 3. Action Button (iPhone 15 Pro and later)

### Mechanism (VERIFIED)

There is **no Action Button API**. A third-party app becomes assignable in two ways, both built
on App Intents:

1. **Controls.** Apple's WidgetKit article states plainly: "A control allows your app to execute
   an action, launch your app to a specific view, or launch a locked camera capture extension
   **from Control Center, the Lock Screen, or by using the Action button**."
   VERIFIED, https://developer.apple.com/documentation/widgetkit/creating-controls-to-perform-actions-across-the-system
2. **Shortcuts.** The user assigns the Action Button to a Shortcut, which runs an `AppIntent`.

Controls are automatically available for the Action button — no separate opt-in. The refinements
article documents the Action-button-specific hint text derived from `displayName`, e.g.
`"Hold for 'Perform Action'"`, and custom hints via `controlWidgetActionHint(_:)` which render as
`"Hold to Perform the Action"`.
VERIFIED, https://developer.apple.com/documentation/widgetkit/adding-refinements-and-configuration-to-controls

**Note the verb: "Hold."** The Action Button requires a press-and-hold, not a click. Apple's own
hint strings say so. INFERRED: that is a deliberate accidental-press guard, and it costs you a
deliberate ~0.5s hold rather than an instant click.

### Latency and reliability

**GAP.** Apple publishes no latency figure for Action Button → control intent → `perform()`.
I could not reach forum or blog measurements. The only documented timing constraint is: "The
system queries for the state of a control when `perform()` returns; finish all actions and save
all state data before it returns."
VERIFIED, https://developer.apple.com/documentation/widgetkit/creating-controls-to-perform-actions-across-the-system

**Do not assume this path is instant.** The intent runs in the widget extension process, which
must be launched cold if not resident. INFERRED that first-press latency after a period of
inactivity is materially worse than warm latency, and that this is the difference between "near
zero friction" and "press, wait, wonder if it worked." **This must be measured on device.**

### Device availability

**GAP.** I could not retrieve the Apple Support article listing Action Button models (multiple
URL attempts 404'd or returned only the guide's table of contents). Commonly understood to be
iPhone 15 Pro / Pro Max and all iPhone 16 and later models — treat as **UNVERIFIED**. The
material point stands regardless: it is absent from all non-Pro iPhones older than the 16, which
excludes a large share of the installed base.

### The exclusivity problem (INFERRED, and it is severe)

The Action Button holds **exactly one** assignment. To use it for clip capture the user must give
up Camera, Flashlight, Voice Memo, Focus, Translate, or whatever they currently have. A
brand-new app from an unknown solo developer asking for the single most contested piece of real
estate on the phone, before the user has any trust in it, is a very large ask. Apple's own HIG
guidance for controls is that you should never "make it required for core functionality"
(paraphrase — the exact HIG page body did not render; **UNVERIFIED quote**, but the design
principle is echoed in the docs' emphasis that the *user* configures these spaces).

INFERRED verdict: the Action Button is the lowest-friction surface *for the subset of users who
configure it*, and configuring it is itself the friction. The friction has been moved from the
capture moment to onboarding, not eliminated. For a cold-start solo developer, moving friction to
onboarding is moving it to where it kills conversion.

---

## 4. Control Center controls and Lock Screen widgets

### What `ControlWidget` allows (VERIFIED)

- `ControlWidgetButton`, iOS 18.0+. Overview, verbatim: "Buttons don't have state; use them for
  fire-and-forget actions such as playing a sound or launching an app."
  VERIFIED, https://developer.apple.com/documentation/widgetkit/controlwidgetbutton
- Controls appear in **Control Center, the Lock Screen, and the Action button**, and "Customers
  configure these system spaces with your app's controls." VERIFIED (article cited in §3).
- "When someone interacts with a control, it performs its action using an app intent you specify.
  Use `AppIntent` or `OpenIntent` for control buttons and `SetValueIntent` for control toggles."
  VERIFIED, same article.
- Lock Screen controls "can replace the default flashlight/camera slots" — i.e. **two slots on the
  whole Lock Screen**, and the user must sacrifice Flashlight or Camera. This is stated in the
  HIG-derived summary; the article itself says only that controls appear on the Lock Screen.
  Treat the two-slot specific as **partially verified**.

### Can it fire without launching the app? YES — and this is well documented

- To launch the app you must *opt in*: "Set your control's action to an app intent that conforms
  to `OpenIntent` to open your app." VERIFIED, same article. A plain `AppIntent` therefore does
  not launch the app.
- iOS 26 replaced the old `openAppWhenRun` flag with `supportedModes: IntentModes`.
  `openAppWhenRun` is **deprecated as of iOS 26.0** with the note "Please provide `supportedModes`
  instead," and "Setting this property to `true` generates an error if the app intent runs in an
  app extension."
  VERIFIED, https://developer.apple.com/documentation/appintents/appintent/openappwhenrun
- `supportedModes` (iOS 26.0+) options: `.background` runs "entirely in the background";
  `.foreground(.immediate)`, `.foreground(.dynamic)`, `.foreground(.deferred)`; combinable. In
  `perform()` you consult `systemContext` / `IntentModes.Current` and
  `canContinueInForeground`.
  VERIFIED, https://developer.apple.com/documentation/appintents/appintent/supportedmodes

**So the answer to the ticket's sharpest question is a documented yes:** a `ControlWidgetButton`
wired to an `AppIntent` with `supportedModes = [.background]` fires and completes without
launching or foregrounding the app. This is the strongest technical result in the report.

### Locked-device behaviour

- `authenticationPolicy` on the intent gates it: "Require authentication if a control performing
  its action would be problematic if done unintentionally or not by the device owner."
- `privacySensitive()` on a `ControlWidgetTemplate` redacts state "while the device isn't
  authenticated."
  VERIFIED, https://developer.apple.com/documentation/widgetkit/adding-refinements-and-configuration-to-controls

INFERRED: capture is not sensitive, so you would *not* set `requiresAuthentication`, and the
control fires from a locked Lock Screen with no Face ID. That is genuinely low friction — the
concept's "no unlocking" claim survives here specifically.

### Reliability caveats (VERIFIED)

- The intent must be in the widget extension's target membership (the article states target
  membership in both app and extension is required for the `OpenIntent`/app-launching case).
- The extension is a separate short-lived process. Widget reload budget rules note that "the
  widget performs an app intent (button tap, toggle)" does *not* count against reload budget, and
  that reloads are free while "the containing app has an active audio or navigation session."
  VERIFIED, https://developer.apple.com/documentation/widgetkit/keeping-a-widget-up-to-date
  INFERRED: since a podcast player *has* an active audio session, control-state freshness is not
  budget-constrained here. Good news.
- **GAP:** Apple publishes **no numeric memory limit** for widget/control extensions. The
  documentation is qualitative only. Any figure (the commonly cited ~30MB) is **UNVERIFIED** and I
  am not asserting one. This matters because the capture intent runs in that extension.

**Architectural consequence, INFERRED:** the control's `perform()` runs in the *widget extension*,
but the rolling audio buffer lives in the *app* process. The extension cannot reach into the app's
memory. So the intent must signal the app (shared container file, `NSUserDefaults` in an app
group, Darwin notification) and the *app* must do the actual clip extraction. Since the app is
alive under the `audio` background mode (§6), this works — but "the system queries for the state of
a control when `perform()` returns; finish all actions and save all state data before it returns"
means the extension must not return before the signal is durably written. This is a real
engineering wrinkle, not a blocker.

### Friction count

Control Center: wake/raise device → swipe down from top-right → locate the control → tap. Lock
Screen: wake device → press-and-hold-ish tap on one of two slots. Both require **looking at the
phone**, i.e. taking it out of your pocket. That is not "no app switching, no unlocking" — it is
"no unlocking, but yes, get your phone out and look at it." Roughly 2–4 seconds and 2–3 discrete
physical actions. Honest, not near-zero.

---

## 5. Live Activities and the Dynamic Island

### Verified capabilities

From https://developer.apple.com/documentation/activitykit/displaying-live-data-with-live-activities:

- **Interactive buttons are supported.** "To add a toggle or button to a Live Activity, adopt the
  AppIntents framework and use the initializers for `Button` and `Toggle` that take an app intent."
  VERIFIED.
- Caveat, verbatim: "Buttons and toggles on Live Activities don't perform actions in CarPlay."
  VERIFIED. Relevant — podcast listening in the car is a major use case, and it is excluded.
- **Duration limit: active up to 8 hours**, then the system automatically ends it and "immediately
  removes it from the Dynamic Island." It remains on the Lock Screen up to 4 further hours;
  **maximum total Lock Screen lifetime 12 hours.** VERIFIED. A 90-minute episode is comfortably
  inside this — the 8-hour limit is not a constraint for this use case.
- Payload limit: static + dynamic data "can't exceed a combined size of 4 KB." VERIFIED.
- Each Live Activity "runs in its own sandbox: no network access, no location updates." VERIFIED.
- "Starting normally requires the app to be in the foreground; updating/ending can happen in the
  background." VERIFIED. But: "To **start** a Live Activity while your app is in the background,
  use an app intent conforming to `LiveActivityIntent`." VERIFIED — so a control can start one.
- Dynamic Island presentations: compact leading/trailing, minimal, expanded (via touch-and-hold),
  plus Lock Screen. "Tapping compact/minimal opens the app." VERIFIED.

### Assessment (INFERRED)

The Dynamic Island **compact** presentation is too small for a reliable button target and a tap
there *opens the app* rather than firing an intent. So the usable path is: touch-and-hold to expand
the Dynamic Island, then tap a button in the expanded region. That is **two deliberate gestures
plus visual targeting** — worse than a Control Center control, not better.

However, a Live Activity is excellent as the **confirmation and status surface**: it satisfies
Guideline 2.5.14's "clear visual indication when recording" requirement, and gives the user
feedback that a clip was taken. INFERRED: use Live Activities for feedback and as a secondary
capture button, not as the primary trigger.

---

## 6. Background execution and the rolling buffer

### What the `audio` background mode gives you (VERIFIED)

- `UIBackgroundModes` is an array; `audio` is one of 14 permitted values. Notably, the DocC data
  for this page has **empty descriptive content for every value including `audio`** — Apple does
  not describe it on that page.
  VERIFIED, https://developer.apple.com/documentation/bundleresources/information-property-list/uibackgroundmodes
- The Xcode article describes `audio` as: "The app plays audible content in the background."
  General rule, verbatim: "Typically, an app is in a suspended state when it's in the background.
  However, there are a limited number of background execution modes your app can support that
  enable it to run when in the background, such as playing audio... For apps that adopt one or
  more of these modes, the system launches or resumes the app, in the background, and affords it
  time to process any related events." Plus: "Use background execution modes sparingly because
  overuse can negatively impact device performance and battery life."
  VERIFIED, https://developer.apple.com/documentation/xcode/configuring-background-execution-modes
- **Recording in the background is explicitly supported.** `AVAudioSession.Category.record`:
  "To continue **recording** audio when your app transitions to the background (for example, when
  the screen locks), add the `audio` value to the `UIBackgroundModes` key."
  VERIFIED, https://developer.apple.com/documentation/avfaudio/avaudiosession/category/record
  Same statement for `playAndRecord` (continue playing in background).
  VERIFIED, https://developer.apple.com/documentation/avfaudio/avaudiosession/category/playandrecord

  This is a meaningful correction to a common assumption: Apple's own docs sanction background
  recording under the `audio` mode. There is no separate "recording" background mode.

### Interruptions (VERIFIED)

From https://developer.apple.com/documentation/avfaudio/handling-audio-interruptions:
- System alerts (incoming call) interrupt the session; observe
  `AVAudioSession.interruptionNotification`, handle `.began` / `.ended`, check `.shouldResume`.
- iPad Smart Folio hardware mic muting interrupts by default; suppressible with
  `overrideMutedMicrophoneInterruption`.
- `setPrefersNoInterruptionsFromSystemAlerts(_:)` expresses a preference not to be interrupted by
  system alerts. Note "preference" — not a guarantee.
- `record` category docs add: "Using this category doesn't prevent phone calls, alarms, or other
  nonmixable audio sessions from interrupting the audio session." VERIFIED.

### Can the app survive a 90-minute episode?

**VERIFIED, yes — with a critical condition.** The `audio` background mode keeps the app running
*while it is actually playing or recording*. Since (per §0) the app must itself be the player, it
is continuously playing for the full 90 minutes, so it is continuously alive. The 90-minute
duration is **not** the hard part.

**INFERRED:** the rolling buffer is cheap and does not need much memory if done correctly. The app
already has the decoded audio it is playing. A 60-second rolling buffer of compressed source audio
is on the order of a megabyte; even a 60s PCM ring buffer at 44.1kHz/16-bit/mono is ~5MB. Either is
trivially affordable in the *app* process. The correct implementation is a ring buffer of the
*encoded* stream or simply retaining a byte-range window of the downloaded episode file — for a
downloaded episode you don't need a live buffer at all, you need a timestamp plus the file, and can
extract the clip lazily.

**This is the real insight on the buffer question:** if the app is the player and the episode is
downloaded (or progressively cached), "rolling buffer" is the wrong mental model. Capture = record
a playback timestamp; clip extraction is an offline seek into a file you already hold. That
eliminates the memory question entirely and makes the capture action near-instant (write one
timestamp), which is exactly what you need inside a control extension's `perform()`.

**GAPs on background execution:**
- No published numeric memory limit for the app under background audio mode. UNVERIFIED.
- No published figure for how quickly the system reclaims the app if playback pauses. The docs say
  only that non-adopting apps are "typically suspended." UNVERIFIED.
- Whether App Review objects to `audio` mode on an app whose *primary* pitch is capture rather than
  playback. Guideline 2.5.4 permits "audio playback"; if the app genuinely plays podcasts this is
  squarely intended use. INFERRED low risk.

---

## 7. Siri / voice — "Hey Siri, clip that"

### Mechanism (VERIFIED)

- App Shortcuts are declared via `AppShortcutsProvider` with `AppShortcut`s carrying `phrases`.
  "You create App Shortcuts programmatically in your code... the shortcuts you create are
  available as soon as someone installs your app, and you don't have to register them yourself...
  Inside this type, construct one or more `AppShortcut` types using **static data**."
  VERIFIED, https://developer.apple.com/documentation/appintents/app-shortcuts
- `AppShortcutPhrase` = "A spoken phrase that causes the system to run the corresponding App
  Shortcut," iOS 16+. `AppShortcutPhraseToken` = "Dynamic values you can include in the spoken
  phrases that run your shortcut."
  VERIFIED, https://developer.apple.com/documentation/appintents/appshortcutphrase
- Apple also notes: "Apple may extract anonymized App Shortcuts data such as localized phrases..."
  and offers `NegativeAppShortcutPhrases` to "completely bypass your app." VERIFIED.

### The app-name requirement — the killer

**Partially verified.** The `AppShortcutPhrase` reference page does not state the rule in prose;
it documents `AppShortcutPhraseToken` as the interpolation mechanism, and the
`.applicationName` token is the one used in every Apple example. The requirement that **every
phrase must include the app name token** is widely enforced at build time by the App Intents
compiler. I could not find a verbatim Apple sentence saying "must." Marking this
**STRONGLY INFERRED / effectively certain but not directly cited.**

**Consequence if true:** the utterance is not "Hey Siri, clip that." It is
**"Hey Siri, clip that in Podnote."** That is 6+ words, must be said out loud, in public, over
your own podcast audio, and — INFERRED — the podcast audio in your ears makes it awkward and Siri's
own audio ducking interrupts your listening. Latency: **GAP**, Apple publishes no Siri→intent
latency figure, and I could not reach measured third-party numbers. Real-world Siri round-trips
are commonly seconds, not milliseconds; treat as UNVERIFIED but assume it is the slowest surface.

Voice is the worst option for the stated use case: podcast listening happens while walking, in
public, in the gym, commuting. Speaking a six-word command is *more* socially costly than taking
your phone out.

---

## 8. Ranked comparison

Friction is counted honestly as: physical actions + whether you must look at the screen + whether
you must retrieve the phone. Latency figures marked **U** are unverified estimates flagged as such,
not measurements.

| Rank | Surface | Actions from thought to capture | Look at screen? | Phone out of pocket? | Latency | App Store risk | Device availability | Verdict |
|---|---|---|---|---|---|---|---|---|
| 1 | **Control Center `ControlWidgetButton`** (background `AppIntent`) | wake + swipe + tap = 3 | Yes | Yes | fast, U | **Low** — documented intended use | iOS 18+, universal | **Best v1 bet** |
| 2 | Lock Screen control (same widget) | wake + tap = 2 | Yes | Yes | fast, U | Low | iOS 18+, universal, but only ~2 slots contested with Camera/Flashlight | Strong second, same code |
| 3 | Action Button | press-and-hold = 1 | **No** | Maybe not | U, cold-start risk | Low | **Pro/16+ only, UNVERIFIED list**; one slot for the whole phone | Lowest friction, smallest reach |
| 4 | `bookmarkCommand` via headphone/Lock Screen player | 1 tap or 1 AirPods press | Depends where it renders | Maybe not | fast | **Medium** — 2.3.1 / 2.5.14 | Universal *if it renders* | **Highest upside, biggest unknown** |
| 5 | Repurposed `nextTrack`/`togglePlayPause` AirPods press | 1 press | No | No | fast | **High** — breaks a standard control's meaning | Universal | Do not ship as default |
| 6 | Live Activity / Dynamic Island button | hold-to-expand + tap = 2 | Yes | Yes | fast | Low | Dynamic Island devices; **dead in CarPlay** | Use for feedback, not trigger |
| 7 | Siri App Shortcut | speak 6+ words incl. app name | No | No | slow, U | Low | Universal | Worst for this context |
| — | Capture another app's audio | n/a | — | — | — | — | **Not possible on iOS 26** | Ruled out (§0) |

---

## 9. Verdict on "near-zero friction"

**No surface clears a near-zero-friction bar, and the claim does not survive.** Stated precisely:

1. **The binding constraint is not the button, it is the player.** iOS gives no third-party app
   access to another app's audio (§0, VERIFIED). "Near-zero friction capture" is therefore gated
   behind "migrate your entire podcast listening to an unknown solo developer's app." That is the
   opposite of near-zero friction, and no button design fixes it. The concept's framing hides its
   largest cost.

2. **The genuinely low-friction surfaces are low-*reach*.** The Action Button is one press without
   looking at the screen — the only surface that honestly approaches the claim — but it requires
   the user to sacrifice their single Action Button assignment to a brand-new app, and it is absent
   from most of the installed base. Friction was relocated to onboarding, not removed.

3. **The high-reach surfaces all require getting the phone out and looking at it.** Control Center
   and Lock Screen controls are 2–3 actions with visual targeting. That is *better* than
   unlock-switch-type, which is a real improvement over the naive baseline — but it is not
   "no app switching, no unlocking, near-zero friction." It is "one fewer step than a voice memo."
   And the honest comparison set is not "stopping to type" — Snipd, Airr and Overcast already ship
   clip buttons, so the delta is against *their* friction, not against nothing.

4. **The one path that would clear the bar is unproven.** `bookmarkCommand` bound to clip capture,
   surfacing as a labelled button in the system Now Playing UI and/or reachable via a headphone
   press, would be genuinely near-zero friction with universal reach and defensible App Store
   semantics ("indicating a user wants to remember a media item"). **Whether it renders anywhere
   the user can reach on iOS 26 is unverified and is the highest-value experiment available.**
   It is a half-day of device testing and it should be done before any build/no-build decision.

### Single best v1 surface

**A `ControlWidgetButton` backed by an `AppIntent` with `supportedModes = [.background]`.**

Reasons: it is the only path with (a) documented background execution without launching the app
(VERIFIED, §4), (b) universal iOS 18+ reach, (c) **one implementation serving three surfaces** —
Control Center, Lock Screen, and the Action Button — which for a solo developer is the decisive
argument, and (d) low review risk. Pair it with a Live Activity for 2.5.14-compliant capture
feedback, and register `bookmarkCommand` as a cheap additional bet that costs almost nothing to add.

### What must be tested on device before deciding

1. Does `bookmarkCommand` render as a reachable control on iOS 26 (Lock Screen player, Control
   Center Now Playing, CarPlay)? — the pivotal unknown.
2. Cold-start latency of Action Button → control extension → `perform()`.
3. Actual memory ceiling of the widget extension and of the app under background audio mode.
4. Whether the app survives 90 minutes of continuous background playback on a real device with
   Low Power Mode enabled.

---

## 10. Evidence quality — stated honestly

- **WebSearch was unavailable**, so no secondary sources (Stack Overflow, Apple Developer Forums,
  indie blogs) were consulted. All the real-world constraints Apple doesn't document — latency
  measurements, extension memory ceilings, what App Review actually rejects in practice, whether
  `bookmarkCommand` renders — are consequently **GAPs, and are labelled as such rather than filled
  with plausible numbers.**
- Several Apple HTML pages returned only their titles; where possible I fetched the DocC JSON
  (`/tutorials/data/...json`) instead, which is the same content Apple's own site renders. Pages I
  could not retrieve in either form are flagged UNVERIFIED inline: the Action Button model list, the
  Action Button and controls HIG bodies, and the Apple Newsroom AirPods announcement.
- No claim in this document about an API's existence or documented behaviour is made without a URL.
  Two claims are marked STRONGLY INFERRED rather than verified (the Siri app-name requirement; the
  headphone click→command mapping) because I could not cite Apple prose for them.
