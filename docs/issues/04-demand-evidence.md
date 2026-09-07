# 04 — Demand evidence: is anyone actually describing this pain?

Type: research
Status: resolved
Blocked by: —

## Question

Find **first-hand evidence** of people describing the specific pain this app addresses: hearing
something worth keeping in a podcast and having no low-friction way to capture it. Evidence, not
speculation.

Search and quote verbatim, with links and dates:

- **Reddit**: r/podcasts, r/PKM, r/ObsidianMD, r/Zettelkasten, r/productivity, r/AppleWatch,
  r/apolloapp-style player communities, r/Overcast if it exists.
- **Hacker News**: search for podcast highlight / clip / note-taking threads and read the comments,
  not just the submissions. HN comments on Snipd and Airr launches are especially valuable.
- **X / Twitter**: PKM and podcast-productivity circles.
- **App Store reviews** of mainstream players (Overcast, Pocket Casts, Castro) requesting clip or
  highlight features.
- **Podcast-industry reports**: Edison Research Infinite Dial, Podtrac, Buzzsprout stats — for
  listener population, listening context (commute / gym / walking), and any data on note-taking
  or engagement behaviour.

Then answer:

- **Which segment feels this most acutely?** Candidates: knowledge workers, PKM/Obsidian power
  users, students, academic researchers, language learners. Rank them by intensity of the pain and
  by evidence volume, and say which is the acute one.
- **How large is the addressable segment, really?** Build up from listener population → share who
  listen to *informational* rather than entertainment podcasts → share who take notes on anything
  → share who'd pay for a tool. Show every step and label each number verified or inferred.
- **Willingness to pay**: is there evidence of people paying for adjacent tools (Readwise,
  Snipd, Audiopen, Voicenotes)?

Critical instruction: also look for **counter-evidence** — people saying they tried highlight
apps and stopped, that they never revisit their saved clips, or that the capture problem isn't
real because they just don't need the ideas later. The "capture graveyard" problem (users capture
enthusiastically then never return) is a known failure mode in PKM tooling and should be
investigated rather than assumed away.

Distinguish verified from inferred. Where evidence is thin, say it is thin.

## Answer

Full research with all quotes and links: [`research/04-demand-evidence.md`](../research/04-demand-evidence.md)

**Verdict on evidence strength: thin-to-moderate, and thinner than it first appears.** The pain
is real and specifically described. The demand *volume* is very low, and the strongest
counter-evidence comes from the same community as the strongest supporting evidence.

### Coverage gaps — read before using this

- **X/Twitter: not searched.** `WebSearch` returned HTTP 400 all session and every major search
  engine blocked scripted fetches. Zero coverage, not searched-and-empty.
- **App Store reviews: not obtained.** Apple's customer-review RSS feed returned empty payloads
  for every app and page tried (2026-09-07); it appears deprecated. The ticket's requirement to
  quote Overcast/Pocket Casts/Castro clip-feature requests **was not met.** Rating counts below
  came from the still-working Lookup API.
- Evidence came from the HN Algolia API, the Arctic Shift Reddit archive, and iTunes Lookup.

### Verbatim evidence the pain is real

> "It's cumbersome to take notes because I mainly don't have my hands free when listening or I
> don't want to type on my phone" — u/julian_englert, [HN, 2022-08-17](https://news.ycombinator.com/item?id=32498490)

> "Inevitably I rush to write an idea down but my hands are sopping wet.. :^)" — u/pizza,
> [HN, 2021-03-03](https://news.ycombinator.com/item?id=26335670)

> "I always had to rewind like 5 times to get a single idea written down." — u/Crisgarher,
> [r/Zettelkasten, 2022-06-20](https://reddit.com/r/Zettelkasten/comments/vgjm8m/how_to_get_specific_podcast_snippets_with_one_tap/id286je/)

> "All of this has been pure hassle, and I've looked for a better solution for years."
> — u/jacmo, [HN, 2020-07-29](https://news.ycombinator.com/item?id=23985313)

> "I'm in Spotify taking screenshots of podcast episodes like I'm righteously going to freaking
> go back to that exact point in that podcast, grab my laptop and use Whisper or manually type
> out the clip" — u/HouseTrout, [r/PKMS, 2026-05-17](https://reddit.com/r/PKMS/comments/1tj3nry/anyone_else_collecting_audiobook_or_podcast/on3oirp/)

Someone independently built this exact product and posted it — *"I don't want this to be a notes
app, I just want it to be good at the capturing part!"*
([u/Lucoda, r/podcasts, 2026-03-01](https://reddit.com/r/podcasts/comments/1rjlr1g/is_it_possible_to_have_an_easier_way_of_capturing/)).
It scored **5 upvotes**. Ten years of such posts in r/podcasts; the best ever scored **7**. A
cosmetic Obsidian dashboard plugin scored **334** in the same period.

### Counter-evidence (the capture graveyard is confirmed, not hypothetical)

> "**podcast notes are the easiest capture trap.** listening + summarizing feels productive, but
> unless something forces those notes back into your work later, **the value was already
> extracted during the listening itself. the notes mostly become archive.**"
> — u/That_Lemon9463, [r/PKMS, 2026-04-22](https://reddit.com/r/PKMS/comments/1svbvy3/for_those_that_are_using_pkms_for_years_what_are/oicr8wm/) (top reply in thread)

Three independent self-reported revisit rates converge on **~10%**: *"I revisit less than 10% of
them within 30 days"* ([u/Limp-Bad-5113](https://reddit.com/r/PKMS/comments/1s4pdq3/how_do_you_handle_the_gap_between_saving_notes/));
*"most notes I write will never be read again, including by me [...] **Retrieval rarely
happens**"* ([u/Actual-Secretary-646](https://reddit.com/r/PKMS/comments/1svbvy3/for_those_that_are_using_pkms_for_years_what_are/oic2ynh/));
*"maybe 1 in 10 quick captures becomes a real note"* ([u/funonmobile](https://reddit.com/r/PKMS/comments/1svbvy3/for_those_that_are_using_pkms_for_years_what_are/oie0qu0/)).

**Strongest single counter-quote — churn from someone who loved it:**

> "**Love Airr! Tried it but did not manage to make it part of my daily routine — the audio
> highlighting feature somehow did not feel natural to me.**"
> — u/louisfialho, [HN, 2021-05-11](https://news.ycombinator.com/item?id=27116331)

A product-design objection to the *core mechanic*, from a user with the problem. Also: *"ehh I
don't want a whole new podcast player"*
([u/yankpat9, HN, 2022-10-26](https://news.ycombinator.com/item?id=33345269)) — player-switching
cost is a real articulated barrier.

**Mainstream listeners do not have this problem.** Asked directly whether they retain what they
hear ([r/podcasts, 2026-06-25](https://reddit.com/r/podcasts/comments/1ufb4bc/do_you_actually_remember_what_you_hear_in/)),
answers were *"I'm definitely an in the moment listener"* (10 upvotes), *"Enjoy the moment"*,
*"If there's something I want to explore more about I open a browser tab 😂"*. The one commenter
who mentioned AI-assisted notes was **downvoted to −3**. And r/podcasts is hostile to the
category: *"95% of posts like this are phony set-ups to promote some shitty vibe-coded AI app"*
([u/Joe_Sacco](https://reddit.com/r/podcasts/comments/1uux2mm/how_much_do_you_remember/ox6uhk4/))
— he is right about the base rate, and this kills the most obvious cold-start channel.

**Supply exceeds demand.** ~20 distinct products found chasing threads that score 5 upvotes.
**Airr — the most-recommended app in the 2020–22 quotes — is dead**: domain does not resolve,
App Store listing 404s, `resultCount: 0` (verified 2026-09-07). No shutdown announcement exists;
nobody noticed enough to write one.

### Acute segment

**PKM/Obsidian power users** — the only segment where pain intensity and evidence volume are both
high. Three caveats: (1) they are **already served** by Snipd→Readwise→Obsidian, which they call a
"game changer"; (2) they are **the source of all the counter-evidence above**; (3) academics have
the highest per-person pain but **near-zero volume** — the best articulation of the academic case
comes from someone who then says *"I personally listen to podcasts mostly for entertainment [...]
**This doesn't require any specialized app.**"*

Intensity/volume disagree for academics (high/near-zero) and knowledge workers (medium/medium).
Students and language learners: **no evidence found at all** — do not assume them.

### Funnel (does not close)

| Step | Value | Status |
|---|---|---|
| US monthly podcast consumers 12+ | **167M** | VERIFIED — Edison *Infinite Dial 2026*, 2026-03-12 |
| US weekly | **130M** | VERIFIED — same |
| iOS share of US smartphones | ~57% | INFERRED (not primary-sourced) |
| Third-party premium iOS player share | **3.5% of downloads** | VERIFIED — Buzzsprout, Aug 2026 (Apple Podcasts 35.8%) |
| — cross-check, Apple "most-used service" | **15%** | VERIFIED — Edison via DemandSage 2026-08-21. Disagrees with above by design; report both, don't average |
| Informational vs entertainment genre split | — | **NO DATA** (behind Edison Podcast Metrics paywall) |
| Hands-busy listening share | — | **NO DATA** podcast-specific |
| Note-taking propensity | — | **NO DATA from any source** — the load-bearing unknown |
| Would pay | — | **NO DATA** |

**I am not producing a TAM.** Three unknowns are multiplicative; their product would be a number
with the appearance of derivation. The bottom-up comparator is more honest (VERIFIED, iTunes
Lookup, 2026-09-07):

| App | US ratings | Avg |
|---|---|---|
| Overcast | **47,689** | 4.54 |
| Pocket Casts | **15,664** | 4.51 |
| Castro | **9,177** | 4.58 |
| **Snipd** | **1,142** | **4.74** (highest) |
| Podwise | **80** | — |
| Airr | **delisted** | — |

The category leader is **~2.4% the size of one indie mainstream player** after five years, funding,
TechCrunch coverage and Product Hunt launches. Counter-reading: Snipd's rating average is the
highest of the six — small but intense, which is the shape that *can* clear $2–5k MRR if
reachable. Reachability is exactly what the r/podcasts hostility undermines.

### Willingness to pay

Verified, and it cuts against the product:

> "However, this app is pricey; **$83.90 a year.**"
> — u/woldeselassie on Snipd, [r/podcasts, 2025-09-29](https://reddit.com/r/podcasts/comments/1ntr3bz/i_want_to_sign_up_for_snipd_just_for_the_auto/)

In the same post he says **"I don't really care about the snipping feature"** — he wanted auto
chapters. The one person found publicly deliberating a purchase wanted a *different feature* and
still balked at the price.

People clearly do pay for **Readwise** (*"happily paying them for Premium"*,
[HN 2023](https://news.ycombinator.com/item?id=36650848); *"a very happy customer"*,
[HN 2020](https://news.ycombinator.com/item?id=22485166)) — but in every observed workflow Readwise
is the **paid destination** and the podcast app is the unpaid **feeder**. Being "good at the
capturing part" targets the substitutable end of a pipeline anchored by someone else's
subscription. Readwise/Obsidian/Anki/Snipd user counts and revenue: **NOT FOUND** — not disclosed.
Snipd's "hundreds of thousands" is vendor marketing with no methodology.

### Bottom line for the go/no-go

The pain is real; the market is small, already served, and the acute segment has publicly
concluded capture was never the bottleneck. Cheapest things that would change the picture:
(1) read Snipd/Overcast App Store reviews manually; (2) check whether Overcast ships bookmarking
on its in-progress transcripts — a user is already
[begging for it](https://reddit.com/r/podcasts/comments/1rjlr1g/is_it_possible_to_have_an_easier_way_of_capturing/orf6355/)
and if Arment ships it free the standalone case likely collapses; (3) ask five current Snipd users
what fraction of their snips they have ever reopened.
