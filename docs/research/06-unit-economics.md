# 06 — Transcription and hosting unit economics

All prices retrieved **2026-09-07** from official pricing pages. Every line is either
**VERIFIED** (a cited published price) or **INFERRED** (a usage assumption, challengeable
independently).

---

## 1. VERIFIED prices (retrieved 2026-09-07)

### Transcription — hosted

| Provider / model | Published price | Per audio hour | Source |
|---|---|---|---|
| OpenAI `whisper` | $0.006/min | **$0.360/h** | [OpenAI API pricing](https://developers.openai.com/api/docs/pricing) |
| OpenAI `gpt-4o-transcribe` | $0.006/min | **$0.360/h** | same |
| OpenAI `gpt-4o-mini-transcribe` | $0.003/min | **$0.180/h** | same |
| OpenAI `gpt-transcribe` | $0.0045/min | **$0.270/h** | same |
| OpenAI `gpt-live-transcribe` (streaming) | $0.017/min | **$1.020/h** | same |
| Deepgram Nova-3 monolingual (pre-recorded, PAYG) | $0.0043/min | **$0.258/h** | [Deepgram pricing](https://deepgram.com/pricing) |
| Deepgram Nova-3 multilingual | $0.0052/min | **$0.312/h** | same |
| AssemblyAI Universal-2 (async) | — | **$0.150/h** | [AssemblyAI pricing](https://www.assemblyai.com/pricing) |
| AssemblyAI Universal-3.5 Pro (async) | — | **$0.210/h** | same |
| Groq `whisper-large-v3-turbo` | — | **$0.040/h** | [Groq STT docs](https://console.groq.com/docs/speech-to-text) |
| Groq `whisper-large-v3` | — | **$0.111/h** | same |
| Gemini 3.5 Transcribe (audio in) | $2.00 / 1M audio tokens | see note | [Gemini pricing](https://ai.google.dev/gemini-api/docs/pricing) |

**Cheapest credible hosted rate: Groq turbo at $0.040/h — 9x cheaper than OpenAI Whisper.**
Groq's own docs put turbo at 12% WER vs 10.3% for v3, so the saving costs accuracy.

Note on Gemini: audio is billed in tokens, not minutes, so a per-hour figure requires an
audio-tokens-per-second constant. Google's pricing page does not publish that constant on the
pricing page itself — **NOT VERIFIED**, so Gemini is excluded from the cost table rather than
estimated.

### Transcription — on-device (zero marginal cost)

| Option | Marginal cost | Notes | Source |
|---|---|---|---|
| Apple `SpeechAnalyzer` / `SpeechTranscriber` | **$0.00** | iOS 26+, fully on-device, streaming with volatile+finalized results, no duration cap, language models are OS-level downloadable assets not counted against app storage | [Apple SpeechAnalyzer docs](https://developer.apple.com/documentation/speech/speechanalyzer) |
| WhisperKit (Argmax, MIT) | **$0.00** | CoreML Whisper on Apple silicon; recommended iOS model is `large-v3-v20240930_626MB` (compressed large-v3-turbo); `.incremental` bounded-memory streaming mode for long audio | [WhisperKit](https://github.com/argmaxinc/WhisperKit) |
| whisper.cpp | **$0.00** | C/C++ ggml Whisper, Core ML / Metal backends for iOS | [whisper.cpp](https://github.com/ggml-org/whisper.cpp) |

**NOT VERIFIED:** neither Apple nor Argmax publishes iPhone battery-drain or real-time-factor
numbers on the pages fetched. Argmax links a BENCHMARKS.md but no figures appeared. Argmax Pro
SDK (needed for real-time transcription *with speakers*) has **no published price** — flagged,
not estimated.

### Summarisation — text model token prices

| Model | Input / 1M | Output / 1M | Source |
|---|---|---|---|
| OpenAI `gpt-5-nano` | $0.05 | $0.40 | [OpenAI API pricing](https://developers.openai.com/api/docs/pricing) |
| OpenAI `gpt-4o-mini` | $0.15 | $0.60 | same |
| OpenAI `gpt-5-mini` | $0.25 | $2.00 | same |
| Anthropic Haiku 4.5 | $1.00 | $5.00 | [Claude pricing](https://claude.com/pricing) |
| Gemini 2.5 Flash-Lite | $0.10 | $0.40 | [Gemini pricing](https://ai.google.dev/gemini-api/docs/pricing) |
| Gemini 3.5 Flash-Lite | $0.30 | $2.50 | same |
| Gemini 3.8 Flash | $0.75 (promo to 2026-12-31, then $1.50) | $3.75 (then $7.50) | same |

Batch tiers halve OpenAI, Anthropic, and Gemini rates.

### Storage and bandwidth

| Backend | Storage | Egress | Ops | Source |
|---|---|---|---|---|
| Cloudflare R2 Standard | **$0.015/GB-mo** | **$0 (free egress)** | Class A $4.50/M, Class B $0.36/M; free tier 10 GB-mo | [R2 pricing](https://developers.cloudflare.com/r2/pricing/) |
| AWS S3 Standard (us-east-1) | **$0.023/GB-mo** first 50 TB | **$0.09/GB** to internet (first 100 GB/mo free) | PUT/POST $0.005/1k, GET $0.0004/1k | [AWS S3 pricing API, pub. 2026-08-31](https://pricing.us-east-1.amazonaws.com/offers/v1.0/aws/AmazonS3/current/region_index.json) |
| Supabase Pro | $25/mo base; 100 GB included, then **$0.0213/GB** | 250 GB included, then **$0.09/GB** | — | [Supabase pricing](https://supabase.com/pricing) |
| Apple CloudKit private database | **$0.00 to the developer** — counts against the *user's* iCloud quota | included | included | [CloudKit](https://developer.apple.com/icloud/cloudkit/) |
| Apple CloudKit public database | up to 1 PB for the app | included | included | same |

**CloudKit private-DB is the decisive fact: user-scoped clip storage is free to the developer at
any scale.** The cost is externalised onto the user's 5 GB free / paid iCloud tier — a UX risk, not
a P&L line. Supabase's $25/mo base is a fixed cost, not per-user, so it only matters below ~a few
hundred users where it dominates everything else.

### Apple's cut

- **15%** commission under the Small Business Program, for developers with **≤ $1M USD proceeds**
  in the prior calendar year; developers new to the App Store also qualify.
  [App Store Small Business Program](https://developer.apple.com/app-store/small-business-program/)
- A solo dev at the $2–5k MRR bar ($24–60k/yr) is far under the threshold, so **15% applies**, not 30%.
- EU alternative terms + SBP can drop to **10%** on subscriptions after year one. Not modelled.
- Bonus, relevant here: SBP members with **< 2M first-time downloads** get **free** access to
  Apple Foundation Models on Private Cloud Compute (requires the PCC entitlement) — a potentially
  $0-marginal-cost summarisation path. Same source. Capability not verified for this use case.

---

## 2. INFERRED assumptions (challenge these independently)

Each is labelled so it can be attacked without touching the verified prices.

| # | Assumption | Value | Basis |
|---|---|---|---|
| A1 | Clip length | **30 s** | The product's own premise (ticket 06). |
| A2 | Typical podcast episode length | **50 min** | INFERRED. No cited source. Talk/interview podcasts commonly run 40–70 min; 50 min is the midpoint. Sensitivity: a 90-min episode raises the expensive-arch cost 1.8x. |
| A3 | Clips per month, by profile | light 8.7, typical 21.7, heavy 152.1 | Arithmetic on the ticket's own definitions: 2/wk x 52/12 = 8.67; 5/wk x 52/12 = 21.67; 5/day x 365/12 = 152.08. |
| A4 | Audio bitrate for stored clips | **64 kbps AAC** mono | INFERRED. Speech-adequate. 30 s = 0.24 MB; 50 min = 24 MB. |
| A5 | Transcript density | **150 words/min ≈ 200 tokens/min** | INFERRED. 30 s clip ≈ 100 tokens; 50 min episode ≈ 10,000 tokens. |
| A6 | Summary output | **150 tokens** per clip | INFERRED product choice (a short note, not an essay). |
| A7 | Server-storage retention (expensive arch) | 12 months, so average stored volume over a year ≈ 6.5x one month's additions | INFERRED. Standard linear-accumulation approximation ((1+12)/2 = 6.5). |
| A8 | In the expensive arch, one whole episode is transcribed **per clip** | 1:1 | INFERRED worst case. If a user takes 3 clips from one episode and the app caches the transcript, divide the transcription line by 3. This is the single biggest lever in the expensive arch. |
| A9 | Every clip triggers exactly one summarisation call | 1:1 | INFERRED. No retries, no regeneration modelled. |
| A10 | No free tier, no trialists, no churn timing effects | — | Costs are per *paying active* user only. |

---

## 3. The ~100x claim, quantified

This is the dominant design fact, and it is exact arithmetic, not a hand-wave.

```
whole episode (A2)   = 50 min = 0.8333 audio hours
one clip (A1)        = 0.5 min = 0.008333 audio hours
ratio                = 50 / 0.5 = 100.0x
```

**The ratio is exactly 100x, and it is provider-independent** — every transcription vendor bills
per unit of audio duration, so the multiplier survives any choice of vendor. Concretely, at OpenAI
Whisper's $0.006/min:

| Unit | Duration | Cost at $0.006/min |
|---|---|---|
| One 30-second clip | 0.5 min | **$0.003** |
| One 50-minute episode | 50 min | **$0.300** |

So the *entire* design question is: does the product need the episode, or only the clip? Any
feature that requires whole-episode context ("smart boundaries", search across the episode,
"what was said before this") drags a 100x multiplier behind it. The map already rules smart
boundaries out of scope — that ruling is worth **two orders of magnitude** on COGS and should be
treated as a load-bearing economic decision, not just a scope trim.

---

## 4. Per-clip cost build-up

### Summarisation, per clip (VERIFIED prices x A5/A6)

30 s transcript in = 100 tokens (A5). Summary out = 150 tokens (A6).

```
gpt-5-nano:      (100/1e6 x $0.05) + (150/1e6 x $0.40)
               =  $0.000005      +  $0.000060       = $0.000065  ~ $0.000075 with overhead
Haiku 4.5:       (100/1e6 x $1.00) + (150/1e6 x $5.00)
               =  $0.0001        +  $0.00075        = $0.00085
Gemini 2.5 Flash-Lite: (100/1e6 x $0.10) + (150/1e6 x $0.40) = $0.00007
```

**Clip summarisation is economically free — under one hundredth of a cent per clip.**
Even a heavy user (152 clips/mo) costs ~$0.011/mo on gpt-5-nano. Summarisation is *not* a
cost driver at clip scale and should be removed from the worry list.

Whole-episode summarisation is different: 10,000 tokens in (A5) + 500 out
= Haiku 4.5 `(10000/1e6 x $1) + (500/1e6 x $5) = $0.0125` per episode; gpt-5-nano
`$0.0005 + $0.0002 = $0.0007`. Still small relative to the transcription line, which is the point:
**transcription duration, not LLM tokens, is where the money goes.**

### Storage, per clip

```
clip at 64 kbps (A4)        = 0.24 MB
R2 storage cost of 1 clip   = 0.24/1024 GB x $0.015 = $0.0000035 / month
CloudKit private DB         = $0.00 (developer pays nothing)
whole episode at 64 kbps    = 24 MB -> $0.00035 / month on R2
```

Storage is negligible under *either* backend at these volumes. R2's free egress means bandwidth
is $0 too. The reason to prefer CloudKit is not cost — it is that it removes the fixed
platform bill (Supabase $25/mo) and the operational burden entirely.

---

## 5. The cost table

Three usage profiles (A3) x two architectures. All figures **per paying active user per month**.

### Architecture (a) — CHEAP: clip-only, on-device transcription, CloudKit storage

| Profile | Clips/mo | Transcription | Summarisation (gpt-5-nano) | Storage | **Total COGS/user/mo** |
|---|---|---|---|---|---|
| Light (2/wk) | 8.7 | $0.0000 | $0.00065 | $0.0000 | **$0.0007** |
| Typical (5/wk) | 21.7 | $0.0000 | $0.00162 | $0.0000 | **$0.0016** |
| Heavy (5/day) | 152.1 | $0.0000 | $0.01141 | $0.0000 | **$0.0114** |

Even the heavy user costs **just over one cent a month**. If summarisation also runs on-device
(Apple Foundation Models, or free-via-PCC under SBP), the cheap architecture's marginal cost is
**exactly $0.00** and the app has *no* usage-linked COGS at all.

### Architecture (a') — clip-only but *hosted* transcription (the middle path)

Worth showing because it isolates the effect of architecture (a) vs (b) from on-device vs hosted.

| Profile | Groq turbo ($0.04/h) | OpenAI Whisper ($0.36/h) |
|---|---|---|
| Light | $0.0035 | $0.0267 |
| Typical | $0.0089 | $0.0666 |
| Heavy | $0.0621 | $0.4677 |

**Clip-only with hosted transcription still costs under 50 cents/mo for the heaviest user.**
This is the important finding: *clip-only is what saves the economics, not on-device.* Going
on-device is a privacy/offline/latency decision, not a margin decision.

### Architecture (b) — EXPENSIVE: whole-episode transcription, hosted API, server storage

Priced two ways, because vendor choice moves this by 9x.

**(b1) OpenAI Whisper $0.36/h + Haiku 4.5 episode summary + R2 storage:**

| Profile | Episodes/mo (A8) | Transcription | Summarisation | Storage (A7) | Ops | **Total** |
|---|---|---|---|---|---|---|
| Light | 8.7 | $2.600 | $0.108 | $0.020 | $0.0001 | **$2.73** |
| Typical | 21.7 | $6.500 | $0.271 | $0.050 | $0.0003 | **$6.82** |
| Heavy | 152.1 | $45.625 | $1.901 | $0.348 | $0.0021 | **$47.88** |

Worked example (typical): `21.67 episodes x 0.8333 h x $0.36/h = $6.500` transcription;
`21.67 x $0.0125 = $0.271` summarisation; `21.67 x 24 MB = 520 MB/mo added, x 6.5 (A7) = 3.30 GB
avg stored x $0.015 = $0.050`.

**(b2) Groq turbo $0.04/h + gpt-5-nano episode summary + R2 storage** — the cheapest coherent
version of the expensive architecture:

| Profile | Transcription | Summarisation | Storage | **Total** |
|---|---|---|---|---|
| Light | $0.289 | $0.006 | $0.020 | **$0.315** |
| Typical | $0.722 | $0.015 | $0.050 | **$0.787** |
| Heavy | $5.069 | $0.106 | $0.348 | **$5.52** |

### The headline comparison

| Profile | Cheap (a) | Expensive (b1) | Ratio |
|---|---|---|---|
| Light | $0.0007 | $2.73 | **3,900x** |
| Typical | $0.0016 | $6.82 | **4,200x** |
| Heavy | $0.0114 | $47.88 | **4,200x** |

The gap is ~4,000x, not 100x, because the expensive architecture stacks the 100x duration
multiplier *on top of* paying a hosted vendor at all (where the cheap path pays $0) and *on top of*
episode-scale rather than clip-scale summarisation. The 100x figure is the transcription-duration
component alone.

---

## 6. Gross margin at plausible price points

Apple takes **15%** (SBP, VERIFIED). Net revenue = gross x 0.85. $50/yr is normalised to
$4.167/mo gross, $3.54/mo net. Gross margin = (net revenue - COGS) / net revenue.

| Price | Net/mo | Profile | Cheap (a) GM | Expensive-Groq (b2) GM | Expensive-OpenAI (b1) GM |
|---|---|---|---|---|---|
| **$5/mo** | $4.25 | Light | 100.0% | 92.6% | 35.8% |
| | | Typical | 100.0% | 81.5% | **-60.5% LOSS** |
| | | Heavy | 99.7% | **-30.0% LOSS** | **-1,026% LOSS** |
| **$10/mo** | $8.50 | Light | 100.0% | 96.3% | 67.9% |
| | | Typical | 100.0% | 90.7% | 19.8% |
| | | Heavy | 99.9% | 35.0% | **-463% LOSS** |
| **$50/yr** ($4.17/mo) | $3.54 | Light | 100.0% | 91.1% | 23.0% |
| | | Typical | 100.0% | 77.8% | **-92.6% LOSS** |
| | | Heavy | 99.7% | **-56.0% LOSS** | **-1,252% LOSS** |

Worked example (the worst cell): heavy user, $50/yr, architecture b1.
`Net revenue = $50 x 0.85 / 12 = $3.542/mo. COGS = $47.88/mo. Margin = (3.542 - 47.88)/3.542 = -1,252%.`
That user burns **$44.33/month** of the developer's money and would need to be balanced by
**~13 light users on the same plan** just to break even.

---

## 7. FLAGGED: heavy-user unprofitability

**Architecture (b) fails the flat-rate test. Architecture (a) does not — by four orders of magnitude.**

| Architecture | Heavy user profitable at $5/mo? | at $10/mo? | at $50/yr? |
|---|---|---|---|
| (a) clip-only + on-device + CloudKit | **Yes** (99.7% GM) | **Yes** | **Yes** |
| (a') clip-only + hosted Groq | **Yes** (98.5% GM) | **Yes** | **Yes** |
| (a') clip-only + hosted OpenAI | **Yes** (89.0% GM) | **Yes** | **Yes** |
| (b2) whole-episode + Groq turbo | **NO — -30%** | Yes (35%) | **NO — -56%** |
| (b1) whole-episode + OpenAI Whisper | **NO — -1,026%** | **NO — -463%** | **NO — -1,252%** |

Break-even usage under the expensive architectures, at $10/mo ($8.50 net):

```
(b1) $8.50 net / ($0.36/h x 0.8333 h + $0.0125 + storage) per episode ~ $0.3145/episode
     -> break-even at ~27 episodes/month = ~6.2 clips/week
(b2) $8.50 net / ~$0.0363 per episode
     -> break-even at ~234 episodes/month = ~54 clips/week
```

**So under (b1), the break-even user is barely above the "typical" profile.** A product whose
*typical* user sits within 25% of the loss line has no headroom for the usage drift that always
follows engagement improvements. This is the textbook flat-rate-AI failure and it is a
consequence of the architecture, not of the pricing.

The single mitigation with the largest effect is **A8**: cache the episode transcript and reuse
it across clips from the same episode. If a user averages 4 clips per episode, b1's typical-user
transcription line falls from $6.50 to $1.63 and typical-user margin at $10/mo goes from 19.8%
to ~77%. This does not rescue the heavy user under b1 (heavy still costs ~$12/mo, a loss at
$10/mo), but it changes the shape of the problem. **Not modelled in the main table** because it
depends on an unmeasured clips-per-episode ratio.

---

## 8. Conclusions

1. **COGS is not the constraint on this business — if and only if the app is clip-only.**
   Under architecture (a), COGS is between $0.0007 and $0.011 per user per month. At the map's
   $2–5k MRR bar (~500 users at $10/mo, or ~1,000 at $5/mo), total monthly COGS is
   **under $12 even if every single user is a heavy user** (`1000 x $0.0114`). Infrastructure
   cannot sink this product. Ticket 07's revenue arithmetic should therefore treat gross margin
   as ~99% and focus entirely on **funnel and CAC**, which is where a solo dev with no audience
   actually fails.

2. **The 100x design choice is real and it is the whole game.** Clip vs episode is exactly 100x on
   transcription duration, and ~4,000x on total COGS once vendor fees and episode-scale
   summarisation compound. Any roadmap item requiring whole-episode context should be costed as a
   business-model change, not a feature.

3. **On-device transcription is not a margin decision.** Clip-only + hosted OpenAI Whisper — the
   most expensive credible clip-only configuration — still yields 89% GM for a heavy user at
   $5/mo. Choose on-device for privacy, offline capture, and latency; do not justify it on cost.
   (The rolling-buffer question the ticket raises is a *capability* question that
   `SpeechAnalyzer`'s streaming API answers cleanly; the unresolved risk is battery, which is
   **NOT VERIFIED** — no published iPhone drain figures were found.)

4. **CloudKit private database is a viable and probably correct storage architecture.** Verified:
   private data lives in the user's iCloud account, costing the developer nothing at any scale.
   It also removes Supabase's $25/mo fixed floor, which at 100 users would be a larger line item
   than all AI costs combined. The trade is a hard dependency on iCloud sign-in and consumption
   of the user's 5 GB free tier — at 0.24 MB/clip (A4), a heavy user adds ~36 MB/month, so the
   quota concern is minor.

5. **Apple's 15% is a rounding error against these numbers.** It reduces net revenue by 15% in
   every scenario, which matters for the revenue arithmetic in ticket 07 but never flips a
   clip-only margin sign.

6. **Recommendation for the go/no-go:** the unit economics of the clip-only design are
   *excellent* and should be removed as a risk from the decision. This is not encouragement — it
   is a narrowing. It means the go/no-go turns entirely on demand and distribution (tickets 01–05,
   07), and that a "no" verdict cannot be justified on cost. Conversely, if the surviving concept
   variant requires whole-episode transcription for legal or product reasons, the economics become
   genuinely hostile and flat-rate pricing stops working.

---

## 9. What could not be verified

Stated as gaps rather than estimated, per the map's standing preference.

- **Gemini per-audio-hour transcription rate.** Billed per audio token; the tokens-per-second
  constant is not on the pricing page. Excluded from all tables.
- **iPhone battery drain / real-time factor for on-device Whisper or SpeechAnalyzer.** No
  published figures on Apple's or Argmax's pages. This is the main *technical* unknown in the
  cheap architecture.
- **Argmax Pro SDK price** (required for real-time transcription with speaker diarization).
  No published price.
- **AssemblyAI's per-minute equivalent** is published only as a per-hour rate; the underlying
  minute rate is not stated (immaterial — the per-hour figure is what the arithmetic uses).
- **Deepgram streaming/real-time rates** were not captured; only pre-recorded PAYG. Immaterial
  for a clip-only design, material if live transcription during playback is required.
- **Clips-per-episode ratio (A8)** — no data. This is the highest-leverage unknown in the
  expensive architecture and would need instrumentation or user research to pin down.
- **Actual episode-length distribution (A2)** — inferred, uncited. A 90-minute-average audience
  (history/deep-dive podcasts) would worsen architecture (b) by 1.8x.
