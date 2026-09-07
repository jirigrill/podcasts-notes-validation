# 06 — Transcription and hosting unit economics

Type: research
Status: resolved
Blocked by: —

## Question

Establish the **cost per active user per month**, so gross margin is visible in the revenue
arithmetic (ticket 07). This ticket is arithmetic, not opinion.

Answer specifically:

- **Transcription options and current prices per audio hour**:
  - On-device: Apple's `Speech` framework / `SpeechAnalyzer` (iOS 26+), and on-device Whisper
    variants (whisper.cpp, WhisperKit). Cost is zero marginal but assess accuracy, battery, and
    whether it can run on a rolling buffer during playback.
  - Hosted: OpenAI Whisper API and `gpt-4o-transcribe`, Deepgram, AssemblyAI, Groq's Whisper.
    Get **current** published per-hour or per-minute pricing.
  - Note that transcribing only a 30-second clip is vastly cheaper than transcribing whole
    episodes — quantify both, since the product design choice drives the cost by ~100x.
- **AI summarisation cost** per clip: token counts for a 30-second transcript in and a summary
  out, priced against current cheap models (Haiku-class, gpt-4o-mini-class, Gemini Flash).
- **Storage and bandwidth**: audio clips per user per month, at what bitrate, on what backend
  (CloudKit, S3/R2, Supabase). Note that CloudKit shifts storage to the user's iCloud quota and
  costs the developer nothing — assess whether that's a viable architecture.
- **Apple's 15–30% cut**: which applies (Small Business Program at 15%) and the effect on net
  revenue.

Then build a **cost table** for three usage profiles — light (2 clips/week), typical
(5 clips/week), heavy (5 clips/day) — under two architectures:
(a) clip-only transcription, on-device, CloudKit storage — the cheap design;
(b) whole-episode transcription, hosted API, server storage — the expensive design.

State the **gross margin** at plausible price points for each. Flag any profile where a heavy user
is unprofitable, since that's the standard failure mode for flat-rate AI subscriptions.

All prices must be current and cited. Distinguish verified pricing from inferred usage assumptions.

## Answer

Full workings, all prices cited and retrieved 2026-09-07:
[research/06-unit-economics.md](../research/06-unit-economics.md)

### The 100x design choice, quantified

Whole episode (50 min, INFERRED) vs one clip (30 s) = **exactly 100x** on transcription duration,
vendor-independent. At OpenAI Whisper's $0.006/min (VERIFIED): $0.300/episode vs $0.003/clip.
Once hosted-vendor fees and episode-scale summarisation compound on top, total COGS differs by
**~4,000x** between the two architectures.

### Cost table — COGS per paying active user per month

Profiles (arithmetic on the ticket's definitions): light 8.7 clips/mo, typical 21.7, heavy 152.1.

| Profile | (a) clip-only + on-device + CloudKit | (a') clip-only + hosted Whisper | (b2) whole-ep + Groq turbo | (b1) whole-ep + OpenAI Whisper |
|---|---|---|---|---|
| Light | **$0.0007** | $0.027 | $0.315 | **$2.73** |
| Typical | **$0.0016** | $0.067 | $0.787 | **$6.82** |
| Heavy | **$0.0114** | $0.468 | $5.52 | **$47.88** |

Cheapest verified hosted transcription is Groq `whisper-large-v3-turbo` at **$0.040/audio hour**
(9x cheaper than OpenAI Whisper's $0.360/h, at 12% vs 10.3% WER). Clip summarisation is
**economically free** — ~$0.000065/clip on gpt-5-nano; transcription *duration*, not LLM tokens,
is the only real cost driver. CloudKit private DB is **$0.00 to the developer** (VERIFIED: private
data sits in the user's iCloud quota), and it also removes Supabase's $25/mo fixed floor.

### Gross margin after Apple's 15% (Small Business Program — VERIFIED, applies at ≤$1M proceeds)

| Price | Net/mo | Cheap (a) | Exp-Groq (b2) | Exp-OpenAI (b1) |
|---|---|---|---|---|
| $5/mo | $4.25 | 100% / 100% / 99.7% | 92.6% / 81.5% / **-30%** | 35.8% / **-60.5%** / **-1,026%** |
| $10/mo | $8.50 | 100% / 100% / 99.9% | 96.3% / 90.7% / 35.0% | 67.9% / 19.8% / **-463%** |
| $50/yr | $3.54 | 100% / 100% / 99.7% | 91.1% / 77.8% / **-56%** | 23.0% / **-92.6%** / **-1,252%** |

(cells read light / typical / heavy)

### FLAG — heavy-user unprofitability

**Architecture (b) fails the flat-rate test; architecture (a) does not.** Under (b1) a heavy user
loses **$44.33/month** at $50/yr — needing ~13 light users to subsidise them. Worse: (b1)'s
break-even is ~27 episodes/month ≈ **6.2 clips/week**, i.e. the *typical* user sits within 25% of
the loss line, leaving no headroom for the usage drift that follows any engagement improvement.
Under (a), even a heavy user costs just over **one cent per month** — no flat-rate risk exists at
any modelled price.

Largest single mitigation for (b): cache the episode transcript across clips from the same episode
(assumption A8). At 4 clips/episode, (b1) typical-user margin at $10/mo rises 19.8% → ~77%. It still
does not rescue the heavy user. Clips-per-episode is **unmeasured** — flagged as the highest-leverage
unknown in the expensive design.

### Conclusion: cheap vs expensive architecture

**Clip-only is what saves the economics — not on-device.** Clip-only with the *most expensive*
credible hosted vendor still yields 89% GM for a heavy user at $5/mo. On-device transcription
(Apple `SpeechAnalyzer`, iOS 26+, free, streaming, no duration cap) is a privacy/offline/latency
choice, not a margin choice.

Under architecture (a), total COGS at the map's $2–5k MRR bar (~500–1,000 users) is **under $12/month
even if every user is heavy**. Infrastructure cannot sink this product, and a "don't build" verdict
**cannot be justified on cost**. The go/no-go therefore turns entirely on demand and distribution.
The inverse also holds: if the surviving concept variant is forced into whole-episode transcription
(by legal constraints from ticket 01, or by product need), the economics become genuinely hostile
and flat-rate pricing stops working — that would be a business-model change, not a feature.

**NOT VERIFIED / gaps:** iPhone battery drain and real-time factor for on-device transcription (no
published figures from Apple or Argmax) — the main technical risk in the cheap path; Gemini's
per-audio-hour rate (billed per audio token, constant unpublished); Argmax Pro SDK price;
episode-length distribution and clips-per-episode ratio (both inferred, uncited).
