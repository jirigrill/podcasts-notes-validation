# 02 — Is friction-free capture (headphone button, lock screen, background) actually achievable on iOS?

Type: research
Status: resolved
Blocked by: —

## Question

The entire value proposition rests on **zero-friction capture**: no unlocking, no app switching.
If that moment isn't achievable, the concept has no wedge regardless of the licensing answer.
Establish what iOS permits today.

Answer specifically:

- **`MPRemoteCommandCenter`**: which commands can a third-party audio app register, and can any
  of them be repurposed as a "capture now" trigger? Cover the headphone remote (single/double/
  triple click), `togglePlayPause`, `nextTrack`, `seekForward`, and the `MPRemoteCommandCenter`
  handlers. Critically: can a command be bound to a *non-playback* action without App Store
  review rejection?
- **AirPods**: what gestures are exposed to third-party apps vs. reserved by the system? Cover
  press-and-hold, stem clicks, and the AirPods Pro/4 controls. Note whether Siri interception is
  possible.
- **Action Button** (iPhone 15 Pro and later): can a third-party app bind to it, and by what
  mechanism (Shortcuts / App Intents)? What's the latency and reliability of that path in practice?
- **Control Center controls** and **Lock Screen widgets**: what does the iOS 18+ `ControlWidget`
  / `AppIntent` API allow? Can a control fire an intent that captures without launching the app?
- **Live Activities** and the Dynamic Island: usable as a capture surface?
- **Background execution**: what are the real constraints on an audio app maintaining a rolling
  buffer? Cover the `audio` background mode, the rolling-buffer approach, memory limits, and
  whether the app can stay alive long enough to be useful during a 90-minute episode.
- **Siri / voice**: is "Hey Siri, clip that" viable via App Intents, and what's the latency?

Then rank the capture surfaces by **friction** (taps/latency from thought to captured) and by
**risk** (App Store review, reliability, device availability). State which single surface is the
best v1 bet and whether *any* of them clear the "near-zero friction" bar the concept claims.

Distinguish verified (documented API behaviour) from inferred throughout.

## Answer

Full findings, with Apple documentation URLs per claim:
[research/02-ios-capture-surfaces.md](../research/02-ios-capture-surfaces.md)

### The finding that reframes the ticket

**iOS gives no third-party app access to another app's audio.** `RPScreenRecorder` captures only
your own app's audio (`.audioApp`) plus the mic; Core Audio process taps (`CATapDescription`) are
macOS/Catalyst only despite misleading iOS entries in the DocC metadata; `ScreenCaptureKit`'s
`SCStream` reaches iOS only at **27.0 (beta)** — not shippable today. VERIFIED.

So the app must **be the podcast player**. There is no "capture button that clips whatever
Overcast is playing." The capture moment analysed below is conditional on having already won the
user's player slot — a far larger ask than the concept's framing admits, and no button design
fixes it.

Consequence for the buffer question: if the app is the player and the episode is downloaded,
"rolling buffer" is the wrong model. Capture = write one playback timestamp; clip extraction is an
offline seek into a file you already hold. This eliminates the memory concern and makes the
capture action near-instant — which is exactly what a control extension's `perform()` needs.

### Ranked friction / risk table

Latency marked **U** = unverified estimate, not a measurement.

| Rank | Surface | Actions | Look at screen? | Phone out? | Latency | Review risk | Availability | Verdict |
|---|---|---|---|---|---|---|---|---|
| 1 | **Control Center `ControlWidgetButton`** + background `AppIntent` | 3 | Yes | Yes | fast, U | **Low** | iOS 18+, universal | **Best v1** |
| 2 | Lock Screen control (same code) | 2 | Yes | Yes | fast, U | Low | Universal, but ~2 slots contested with Camera/Flashlight | Strong second |
| 3 | Action Button | 1 (press-and-hold) | **No** | Maybe not | U, cold-start risk | Low | Pro/16+ only (model list UNVERIFIED); one slot per phone | Lowest friction, smallest reach |
| 4 | `bookmarkCommand` (headphone / Now Playing) | 1 | Depends | Maybe not | fast | Medium (2.3.1, 2.5.14) | Universal *if it renders* | **Highest upside, biggest unknown** |
| 5 | Repurposed `nextTrack` / AirPods press | 1 | No | No | fast | **High** — breaks a standard control | Universal | Don't ship as default |
| 6 | Live Activity / Dynamic Island | 2 (hold-expand + tap) | Yes | Yes | fast | Low | **Dead in CarPlay** (documented) | Feedback surface, not trigger |
| 7 | Siri App Shortcut | speak 6+ words incl. app name | No | No | slow, U | Low | Universal | Worst for this context |
| — | Capture another app's audio | — | — | — | — | — | **Impossible on iOS 26** | Ruled out |

Key per-surface facts (all VERIFIED, cited in the research file):
- **`MPRemoteCommandCenter`** vends a **`bookmarkCommand`** documented as "indicating a user wants
  to remember a media item," with app-supplied `localizedTitle`. `MPFeedbackCommand`'s overview
  explicitly permits "other tasks related to receiving feedback." Clip capture *is* semantically a
  bookmark — this is intended use, not repurposing, and is far safer than hijacking `nextTrack`.
  **GAP: whether it renders anywhere user-reachable on iOS 26 is undocumented and untested.**
- **AirPods**: no third-party gesture API exists. Press/double/triple are already consumed by
  play-pause/next/previous; press-and-hold is user-configurable only among Apple's own choices
  (Siri, listening modes). Siri interception: not possible. `AVCaptureEventInteraction` (the API
  that receives the iOS 26 AirPods stem camera remote) is explicitly gated: "The system sends
  capture events only to apps that actively use the camera." Dead end.
- **Controls fire without launching the app** — the ticket's sharpest question, answered yes and
  documented. `openAppWhenRun` is **deprecated in iOS 26**; use `supportedModes = [.background]`.
  Launching requires opting in via `OpenIntent`. `authenticationPolicy` left unset means it fires
  from a locked Lock Screen with no Face ID. One `ControlWidget` implementation serves Control
  Center, Lock Screen **and** the Action Button.
- **Background execution is not the problem.** Apple's docs explicitly sanction background
  *recording* under the `audio` mode (no separate recording mode exists). Because the app is
  playing continuously it stays alive for the whole 90 minutes; the 8-hour Live Activity cap is
  irrelevant at 90 min. Interruptions (calls, alarms) are documented and handleable;
  `setPrefersNoInterruptionsFromSystemAlerts` is a *preference*, not a guarantee.

### Single best v1 surface

**A `ControlWidgetButton` backed by an `AppIntent` with `supportedModes = [.background]`.**
Decisive reason for a solo developer: one implementation serves three surfaces (Control Center,
Lock Screen, Action Button), with documented background execution, universal iOS 18+ reach, and
low review risk. Pair with a Live Activity for Guideline 2.5.14-compliant capture feedback, and
register `bookmarkCommand` as a near-free additional bet.

### Verdict: does any surface clear the near-zero-friction bar?

**No. The claim does not survive.**

1. The binding constraint is the **player**, not the button. "Zero-friction capture" is gated
   behind migrating all podcast listening to an unknown solo dev's app.
2. The one surface that honestly approaches the claim (Action Button, one press, no looking) has
   the **smallest reach** and demands the user surrender the single most contested control on the
   phone to a brand-new app. Friction was relocated to onboarding, where it kills conversion.
3. Every high-reach surface requires **taking the phone out and looking at it** (2–3 actions,
   ~2–4s). That is one step better than a voice memo — not near-zero.
4. The honest baseline is not "stop and type." Snipd, Airr and Overcast already ship clip buttons,
   so the delta must be measured against *them*, not against nothing.

**The one path that could clear the bar is unproven**: `bookmarkCommand` surfacing as a labelled,
reachable button in the system Now Playing UI or via a headphone press. Universal reach,
defensible App Store semantics, genuinely near-zero friction. **Half a day of device testing
settles it, and it should be settled before any build/no-build call.**

Other must-test-before-deciding items: Action Button cold-start latency; widget-extension memory
ceiling (Apple publishes no number); 90-minute background playback survival under Low Power Mode.

### Evidence caveat

WebSearch was unavailable in the research environment, so **no secondary sources** (Stack
Overflow, Apple Developer Forums, indie blogs) were consulted. Every real-world constraint Apple
doesn't document — latencies, extension memory limits, what review actually rejects, whether
`bookmarkCommand` renders — is therefore recorded as an explicit **GAP** rather than filled with a
plausible-sounding number. Two claims are marked STRONGLY INFERRED rather than verified: the Siri
app-name-in-phrase requirement, and the headphone-click→command mapping.
