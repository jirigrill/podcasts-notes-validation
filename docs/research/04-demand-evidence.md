# 04 — Demand evidence for a podcast idea-capture app

Research for ticket `issues/04-demand-evidence.md`. Compiled 2026-09-07.

**Method note, read this first.** The `WebSearch` tool was broken for the whole of this
session (HTTP 400 on every call), and Google, Bing, DuckDuckGo and Brave all blocked
scripted HTML fetches. Reddit's own JSON API returned 403. Evidence below was gathered
through three channels that did work: the **Hacker News Algolia API** (full comment
search and full thread trees), the **Arctic Shift Reddit archive**
(`arctic-shift.photon-reddit.com`), and the **Apple iTunes review/lookup APIs**. This
means coverage of **X/Twitter is zero** — that source is simply missing from this ticket,
not searched-and-empty. Say so downstream rather than treating the absence as a finding.

---

## 1. Verbatim evidence that the pain is described

The pain is real and consistently articulated. It has a stable shape across nine years of
posts: **hands are busy, the idea passes, and the recovery cost is disproportionate.**

### 1.1 The core "hands busy, idea gone" complaint

> "It's cumbersome to take notes because I mainly don't have my hands free when listening
> or I don't want to type on my phone"
>
> — u/julian_englert, Hacker News, 2022-08-17,
> [comment 32498490](https://news.ycombinator.com/item?id=32498490)

> "Worst part abt this system though is that I often listen to podcasts while doing the
> dishes. Inevitably I rush to write an idea down but my hands are sopping wet.. :^)"
>
> — u/pizza, Hacker News, 2021-03-03,
> [comment 26335645](https://news.ycombinator.com/item?id=26335670)

> "Often I listen to the podcasts when I'm on the go and whenever something valuable comes
> up, I'm trying to remember it, so that I can get to whenever possible. But so far, the
> most effective way is to stop and send it to Evernote. any hack recommendations?"
>
> — u/dabderax, r/podcasts, 2016-08-22,
> [4z34sj](https://reddit.com/r/podcasts/comments/4z34sj/what_would_be_the_best_way_to_take_a_note_while/)

> "I always had to rewind like 5 times to get a single idea written down."
>
> — u/Crisgarher, r/Zettelkasten, 2022-06-20,
> [id286je](https://reddit.com/r/Zettelkasten/comments/vgjm8m/how_to_get_specific_podcast_snippets_with_one_tap/id286je/)

> "I've tried to hack together a system for capturing what I learn from podcasts: talking
> into my phone + speech recognition via Otter.ai + copy/paste text from iPhone to Macbook
> etc. All of this has been pure hassle, and I've looked for a better solution for years."
>
> — u/jacmo, Hacker News, 2020-07-29,
> [comment 23985313](https://news.ycombinator.com/item?id=23985313)

> "I always wanted some way to bookmark sections in podcasts that was worth a revisit. The
> problem was that I almost exclusively listened to podcasts while driving (pre-covid)
> which meant I needed a mostly-hands-free solution."
>
> — u/me_smith, Hacker News, 2020-09-01,
> [comment 24348056](https://news.ycombinator.com/item?id=24348056)

The most exact statement of the product thesis comes from someone who independently built
the same thing:

> "Hey! I was frustrated that I would listen to a podcast and then forget everything. When
> I read I like highlighting and storing but it's hard to replicate that with a podcast.
> I've built a version of this that works for capturing the last 30 seconds said on a
> podcast and then it goes right to my obsidian vault. [...] I don't want this to be a
> notes app, I just want it to be good at the capturing part!"
>
> — u/Lucoda, r/podcasts, 2026-03-01,
> [1rjlr1g](https://reddit.com/r/podcasts/comments/1rjlr1g/is_it_possible_to_have_an_easier_way_of_capturing/)
> — 5 upvotes, 5 comments.

Note the engagement number. This is the single closest match to the proposed product found
anywhere in the search, posted in the largest relevant subreddit, and it drew **five
upvotes and five comments** — three of which were founders promoting their own tools. That
is a signal about market temperature, and it is a cold one.

### 1.2 The workaround-tax evidence

The strongest demand signal is not people asking for the feature — it is people building
absurd Rube Goldberg machines to get it. The workarounds are the evidence.

The screenshot-the-lock-screen workaround appears independently at least four times:

> "If I'm on the go on my phone and there's a cool idea in the podcast I'm listening, then
> I take a screenshot of my locked screen as it shows my audio player (with the button
> shortcuts). And then later on I go back to those screenshots and I know which podcasts
> and which moments had important ideas."
>
> — u/emgo, Hacker News, 2021-03-06,
> [comment 26369169](https://news.ycombinator.com/item?id=26369169)

> "I'm in Spotify taking screenshots of podcast episodes like I'm righteously going to
> freaking go back to that exact point in that podcast, grab my laptop and use Whisper or
> manually type out the clip I want to be used in something later."
>
> — u/HouseTrout, r/PKMS, 2026-05-17,
> [on3oirp](https://reddit.com/r/PKMS/comments/1tj3nry/anyone_else_collecting_audiobook_or_podcast/on3oirp/)

And the hardware-hack extreme:

> "I already have my original Amazfit Bip watch configured to send a 'track back' signal to
> Snipd via Gadgetbridge to snip podcast notes while I'm driving or washing dishes or
> whatever. [...] In other words, I am apparently exactly the kind of weirdo who would use
> the heck out of something like this!"
>
> — u/smeej, Hacker News, 2025-12-09,
> [comment 46211684](https://news.ycombinator.com/item?id=46211684)

That last quote is worth reading twice. The person doing the most elaborate version of this
workflow **describes themselves as a weirdo** and is correct to. Self-identified outlier
status from your most enthusiastic user is a market-size warning, not an endorsement.

### 1.3 Multi-year unmet demand in r/podcasts

The "does an app do this?" question recurs in r/podcasts at a steady, low rate from 2017 to
2026 — which establishes both that the desire is durable and that it is small.

| Date | Post | Score / comments |
|---|---|---|
| 2016-08-22 | [what would be the best way to take a note while listening](https://reddit.com/r/podcasts/comments/4z34sj/what_would_be_the_best_way_to_take_a_note_while/) | 5 / 6 |
| 2017-10-11 | [any apps that allow you to tag/bookmark specific times](https://reddit.com/r/podcasts/comments/75q9aw/weird_question_are_there_any_apps_preferable_for/) | 1 / 3 |
| 2019-03-28 | [Bookmark episode file position?](https://reddit.com/r/podcasts/comments/b6f6oh/bookmark_episode_file_position/) | 5 / 5 |
| 2021-01-13 | [Looking for app that lets you bookmark specific points](https://reddit.com/r/podcasts/comments/kwtmxy/looking_for_app_that_lets_you_bookmark_specific/) | 2 / 3 |
| 2023-05-16 | [Podcast apps that can take notes or bookmark](https://reddit.com/r/podcasts/comments/13itnci/podcast_apps_that_can_take_notes_or_bookmark/) | 7 / 5 |
| 2026-03-01 | [Is it possible to have an easier way of capturing snippets](https://reddit.com/r/podcasts/comments/1rjlr1g/is_it_possible_to_have_an_easier_way_of_capturing/) | 5 / 5 |

**Read the right column.** Ten years of demand, and the best-performing post scored 7. For
comparison, a post in r/ObsidianMD about a *cosmetic dashboard plugin* scored **334**
([1u56bn3](https://reddit.com/r/ObsidianMD/comments/1u56bn3/custom_views_has_literaly_changed_my_obsidian/),
2026-05-19). The pain is real and it is niche. Both halves of that sentence are load-bearing.

### 1.4 One explicit feature request to a mainstream player

> "I've been begging Marco to add this to Overcast, but haven't heard back. No idea if he's
> even seen it... However, he's still working on transcripts and that's a prereq for
> bookmarking w/ text extraction, so I keep my fingers crossed."
>
> — u/jkmcf, r/podcasts, 2026-06-09,
> [orf6355](https://reddit.com/r/podcasts/comments/1rjlr1g/is_it_possible_to_have_an_easier_way_of_capturing/orf6355/)

This is a double-edged citation. It evidences demand, and it flags that **Overcast is
building transcripts**, which is the prerequisite for shipping this as a free feature inside
an app that already owns the user. Platform risk, from the user's own mouth.

### 1.5 The segmentation quote — the single most useful line found

> "Mostly I listen to podcasts but there's a few I listen to for learning [...] **I think
> most people listen to podcasts for fun and entertainment so it's unlikely they'll want to
> clip, get transcripts etc. But the small number of podcasts doing deep dives on scholarly,
> technical or professional matters? It's potentially quite useful.**"
>
> — u/lawtalkinghuman, Hacker News, 2022-10-24,
> [comment 33316379](https://news.ycombinator.com/item?id=33316379)

An unprompted user articulating the exact market-size constraint, four years ago. Treat this
as the frame for section 3 below.

---

## 2. Counter-evidence (the most important section)

The capture-graveyard failure mode is **not hypothetical and not rare**. It is the dominant
theme when PKM veterans discuss podcast notes, and in several cases the people describing it
are the exact power users this app would target. Read this section before section 1.

### 2.1 "Podcast notes are the easiest capture trap"

> "biggest lesson after a few years: **podcast notes are the easiest capture trap.**
> listening + summarizing feels productive, but unless something forces those notes back
> into your work later, **the value was already extracted during the listening itself. the
> notes mostly become archive.**"
>
> — u/That_Lemon9463, r/PKMS, 2026-04-22,
> [oicr8wm](https://reddit.com/r/PKMS/comments/1svbvy3/for_those_that_are_using_pkms_for_years_what_are/oicr8wm/)
> — 5 upvotes, the top-scoring reply in the thread.

"The value was already extracted during the listening itself" is the sharpest challenge to
the product premise found in this research. If true for most listeners, the capture artifact
is worthless and the app solves a problem that resolves itself.

> "That example about storing podcast notes highlights the biggest trap. The main lesson
> after a few years is that **treating a vault like a filing cabinet for other people's
> thoughts is basically useless.**"
>
> — u/emiliobay, same thread, 2026-04-24,
> [oiqgarr](https://reddit.com/r/PKMS/comments/1svbvy3/for_those_that_are_using_pkms_for_years_what_are/oiqgarr/)

### 2.2 Self-measured revisit rates — the numbers users report on themselves

One user tracked it:

> "I save ~15 notes/highlights per week. **I revisit less than 10% of them within 30 days.**
> The ones I DO revisit are almost always because I stumbled on them accidentally, not
> through any intentional system."
>
> — u/Limp-Bad-5113, r/PKMS, 2026-03-23,
> [1s4pdq3](https://reddit.com/r/PKMS/comments/1s4pdq3/how_do_you_handle_the_gap_between_saving_notes/)

> "The biggest one: **most notes I write will never be read again, including by me.** [...]
> **Maybe ten percent of what I capture ever ends up in this layer.** [...] The honest
> version is that most of the value of notes is in the act of writing them, not in
> re-reading. So I optimize for capture being fast and friction-free, not for retrieval
> being elegant. **Retrieval rarely happens.**"
>
> — u/Actual-Secretary-646, r/PKMS, 2026-04-22,
> [oic2ynh](https://reddit.com/r/PKMS/comments/1svbvy3/for_those_that_are_using_pkms_for_years_what_are/oic2ynh/)

> "maybe **1 in 10** quick captures becomes a real note"
>
> — u/funonmobile, r/PKMS, 2026-04-22,
> [oie0qu0](https://reddit.com/r/PKMS/comments/1svbvy3/for_those_that_are_using_pkms_for_years_what_are/oie0qu0/)

Three independent self-reports converge on **~10% of captures ever being revisited.** All
are self-reported and unverifiable, and all three come from people motivated to keep doing
PKM, which biases *upward* if anything. Note carefully that u/Actual-Secretary-646 draws a
pro-capture conclusion from this ("optimize for capture being fast") — the 10% figure does
not automatically kill the product, but it does mean the retention story cannot rest on
"users will come back to their library."

### 2.3 The most-cited alternative is "just don't save it"

> "The fact that you're not going back to read/make use of the things you save is your
> answer. **You didn't need to save them in the first place.** You're confusing collecting
> with creating knowledge."
>
> — u/448899again, r/PKMS, 2025-12-22,
> [o130i8j](https://reddit.com/r/PKMS/comments/1qjnndv/how_do_you_deal_with_content_you_want_to/o130i8j/)

> "What purpose does this collection of information really serve? I like having things
> organized neatly and easily accessible, but **I have a hard time seeing what goal
> thousands of scattered annotations, text bookmarks, podcast bookmarks, etc. serve.**"
>
> — u/eXpl0it3r, Hacker News, 2019-11-29,
> [comment 21664594](https://news.ycombinator.com/item?id=21664594)

> "If it's just hoarding links with a hope to be productive in future, that's a whole
> different thing."
>
> — u/threespire, r/PKMS, 2026-04-26,
> [oj94zsa](https://reddit.com/r/PKMS/comments/1svbvy3/for_those_that_are_using_pkms_for_years_what_are/oj94zsa/)

### 2.4 Tried a highlight app, bounced off it

Direct churn evidence. Rare, but it exists and it is specific:

> "**Love Airr! Tried it but did not manage to make it part of my daily routine — the audio
> highlighting feature somehow did not feel natural to me.** However, I was really impressed
> with all the transcripts they generate."
>
> — u/louisfialho, Hacker News, 2021-05-11,
> [comment 27116331](https://news.ycombinator.com/item?id=27116331)

This is the single most damaging quote in the file: someone who *loved* the product and had
the problem still could not retain the habit, and the reason was that the core interaction —
the highlight gesture itself — "did not feel natural." That is a product-design objection to
the central mechanic, not a pricing or marketing objection.

> "This might be an irrational thought, but almost right away as I started using these
> [Snipd, Airr], I said, **'ehh I don't want a whole new podcast player.** I just want a
> better way to take podcast notes and organize them'."
>
> — u/yankpat9, Hacker News, 2022-10-26,
> [comment 33345269](https://news.ycombinator.com/item?id=33345269)

Player-switching cost is a real, articulated barrier. Any variant of this product that
requires abandoning Overcast/Pocket Casts inherits this objection.

> "Snipd's cloud dependency kills it offline. Overcast just downloads and plays."
>
> — u/Main_Problem_2696, r/podcasts, 2026-05-25,
> [ookl518](https://reddit.com/r/podcasts/comments/1tqrud4/snipd_dealbreaker/ookl518/)

> "Love the 'Snips' feature but the major downer of this App is that **you need a reasonably
> good network connection for it to work. It was dead in the water on a flight to LA.** And
> even when driving around will hang while trying to download favorites (never had either of
> these issues with Overcast)"
>
> — u/BartSmithsonn, r/podcasts, 2026-05-25,
> [1tqrud4](https://reddit.com/r/podcasts/comments/1tqrud4/snipd_dealbreaker/)

Note the overlap between the *listening contexts that create the need* (driving, flights) and
the contexts where a transcript-dependent architecture fails. Worth carrying into the
technical variant decision.

### 2.5 "The capture problem isn't real for me" — the mainstream listener

This is the largest and most consistent body of counter-evidence, and it is decisive on
market size. Asked directly whether they retain what they hear
([r/podcasts 1ufb4bc](https://reddit.com/r/podcasts/comments/1ufb4bc/do_you_actually_remember_what_you_hear_in/),
2026-06-25, 17 upvotes / 27 comments), essentially nobody wanted a tool. They wanted
*permission not to care*:

> "I'm definitely an in the moment listener. I am usually gardening when I listen to a
> podcast and often realize I have even missed a good chunk of the story because I'm focused
> on my work." — u/kengigi, 10 upvotes,
> [otqg2rz](https://reddit.com/r/podcasts/comments/1ufb4bc/do_you_actually_remember_what_you_hear_in/otqg2rz/)

> "Enjoy the moment. Sometime it's nice to have some background noise when your cleaning the
> house or cooking" — u/Useful_Region9179,
> [otrokhd](https://reddit.com/r/podcasts/comments/1ufb4bc/do_you_actually_remember_what_you_hear_in/otrokhd/)

> "In the moment! If there's something I want to explore more about I open a browser tab 😂"
> — u/midasgoldentouch, 3 upvotes,
> [otrheqr](https://reddit.com/r/podcasts/comments/1ufb4bc/do_you_actually_remember_what_you_hear_in/otrheqr/)

> "**I've just accepted that for my ease of life, I need to just accept that I'll forget
> things or lack access to notes. Sometimes I just need to enjoy the ride, not worrying
> whether or not the ride lasts forever.**" — u/Ok_Return_777, **downvoted to −3**,
> [otqecko](https://reddit.com/r/podcasts/comments/1ufb4bc/do_you_actually_remember_what_you_hear_in/otqecko/)

The scoring pattern in that thread is itself data: the "just enjoy it" answers were upvoted,
and the one commenter who mentioned using AI to take notes for them was **downvoted to −3**
and challenged:

> "The downvote is probably for the ai use bc ai is making so many things in our world worse.
> **Why not just check for transcripts or take notes yourself?**"
> — u/heathers-damage, 3 upvotes,
> [otr3rna](https://reddit.com/r/podcasts/comments/1ufb4bc/do_you_actually_remember_what_you_hear_in/otr3rna/)

r/podcasts is actively hostile to this product category. Which brings us to:

### 2.6 The community assumes you are a spammer

> "What kind of podcasts are you listening to that you need to remember specific details?
> **I shouldn't even answer this honestly. 95% of posts like this are phony set-ups to
> promote some shitty vibe-coded AI app**"
>
> — u/Joe_Sacco, r/podcasts, 2026-06-11, 3 upvotes,
> [ox6uhk4](https://reddit.com/r/podcasts/comments/1uux2mm/how_much_do_you_remember/ox6uhk4/)

He is not wrong about the base rate. In the threads sampled, r/podcasts moderators removed
comments under the self-promotion rule **at least five times** in the capture-related threads
alone, and the "capture snippets" thread from 2026-03-01 attracted three separate founders
pitching AskAlong, podtalk studio and an unnamed mark-and-chat app. This has a direct
consequence for the cold-start distribution assumption in `map.md`: **the most obvious
organic channel for a solo developer with no audience is a subreddit that reflexively bans
this exact pitch.**

### 2.7 The category is crowded and the graveyard is full of suppliers, not just notes

Distinct products found addressing this problem, all discovered incidentally during search:
Snipd, Airr, Podwise, NoteCast, Momento, AskAlong, Recall, PodScribe.IO, Interleave,
Omphalis, Aurilix, DriftNote, TLDC, Steadcast, Second Stream, spotscribe.io, TL;DL,
podcastbookmarks.com, Riptide, Shuffle.

Two observations. First, supply massively exceeds articulated demand — twenty-odd products
chasing forum threads that score 5 upvotes. Second, most of these have no visible traction,
and several are dead. **Airr in particular appears defunct**: its domain no longer resolves,
its App Store listing 404s, and the iTunes lookup API returns `resultCount: 0` for its ID
(checked 2026-09-07). Airr was the app most recommended in the 2020–2022 quotes above. The
best-loved product in this niche died, and no announcement was ever made — nobody noticed
enough to write one.

---

## 3. Which segment feels this most acutely

Ranked by **pain intensity** and **evidence volume** separately, because they disagree.

| Segment | Pain intensity | Evidence volume | Notes |
|---|---|---|---|
| PKM / Obsidian power users | **High** | **High** | Only segment where both are high. All of §1.2's workarounds come from here. |
| Knowledge workers (business/self-improvement listeners) | Medium | Medium | Present but diffuse; "financial podcasts" ([1p57w7g](https://reddit.com/r/podcasts/comments/1p57w7g/does_anyone_else_take_notes_during_podcasts_and/)), business/sales. Rarely describes *capture* friction specifically. |
| Academic researchers | **Highest per-person** | **Very low** | Only one clear instance (u/leSchaf, §3.1). Cited as a hypothetical by others, not self-reported. |
| Students | Medium | **Near zero** | Searched r/GradSchool and r/AskAcademia; found nothing on podcast capture. Genuinely absent. |
| Language learners | Unknown | **Zero** | r/languagelearning returned nothing relevant. Absence of evidence, not evidence of absence — but do not assume this segment. |

**The acute segment is PKM/Obsidian power users**, and it is the only defensible answer,
because it is the only segment where intense pain and observable volume coincide. But three
qualifications, all of which cut against the product:

1. **This segment is already served.** Snipd + Readwise + Obsidian is a working, actively
   recommended pipeline. See u/Tutwiler: *"One touch to clip a section with the transcript
   included. I sync these to Readwise and they show up periodically in my Readwise review
   emails."* ([r/PKMS, 2026-05-17](https://reddit.com/r/PKMS/comments/1tj3nry/anyone_else_collecting_audiobook_or_podcast/on66veq/)),
   and u/threecheese: *"It changes the 'back' button behavior to save snippets while driving"*
   ([HN, 2025-02-03](https://news.ycombinator.com/item?id=42918963)). A new entrant must beat
   an incumbent that these users describe as a "game changer."
2. **This segment is the one supplying the counter-evidence.** Every quote in §2.1–2.3 comes
   from r/PKMS. The people with the most acute capture pain are also the people who have
   concluded, in public, that capture was never the bottleneck. That is an uncomfortable
   coincidence and should not be smoothed over.
3. **The academic case has the highest per-person pain and almost no volume.** The clearest
   articulation is second-hand: *"if you need to go back to specific parts of a podcast
   frequently or have to be very thorough in referencing (e.g. if you use it as a source for
   a research paper)"* — u/leSchaf,
   [r/Zettelkasten, 2020-10-13](https://reddit.com/r/Zettelkasten/comments/ja9fz0/how_do_you_capture_podcast_notes/g8og605/).
   Note the same commenter's own behaviour: *"I personally listen to podcasts mostly for
   entertainment and more informal research. Therefore, I find jotting down a note just
   referencing the episode [...] more than sufficient. **This doesn't require any specialized
   app.**"* Even the person who best articulates the acute use case does not have it.

**Where intensity and volume disagree:** academics (high intensity, near-zero volume) versus
knowledge workers (medium intensity, medium volume). Chasing the academic segment means
building for a persona evidenced by roughly one forum comment. Chasing knowledge workers
means building for people who mostly do not describe capture friction at all. Neither is a
comfortable position and the honest reading is that **there is no segment with both high
intensity and enough volume to underwrite a business** — only one with enough of each to be
worth a hypothesis.

---

## 4. Audience-size funnel

Every line is labelled. **VERIFIED** means a cited figure from a named source. **INFERRED**
means my assumption, and the assumption is stated so it can be attacked. **NO DATA** means no
source publishes it and I refuse to fill the gap.

| # | Step | Value | Status |
|---|---|---|---|
| 1 | US monthly podcast consumers, age 12+ | **167 million** | VERIFIED — Edison Research, *The Infinite Dial 2026*, published 2026-03-12 |
| 1b | US weekly podcast consumers, age 12+ | **130 million** | VERIFIED — same source |
| 2 | iOS share of US smartphones | ~57% | INFERRED (widely reported range 55–60%; I did not verify a primary source) |
| 3 | Share on a *third-party premium* iOS player (Overcast / Pocket Casts / Castro / Snipd) | **3.5% of download requests** | VERIFIED — Buzzsprout global stats, Aug 2026. Apple Podcasts alone = 35.8%. Note this is host-side download telemetry from one host, not a survey. |
| 3b | Cross-check: Apple Podcasts as "service used most often" | **15%** of US weekly consumers | VERIFIED — Edison via DemandSage, 2026-08-21. **This disagrees with 3 by design** (survey self-report vs download attribution). Report both; do not average. |
| 4 | Share who listen to *informational* rather than entertainment podcasts | — | **NO DATA.** Edison holds this behind the Podcast Metrics subscription. No primary source publishes it. |
| 5 | Share listening hands-busy (driving / gym / chores) | — | **NO DATA** for podcasts specifically. The commonly cited 36% in-car digital-audio figure bundles podcasts with streaming music and audiobooks and must not be reused here. |
| 6 | Share who take notes on audio content, ever | — | **NO DATA. From any source.** Confirmed absent from the four studies most likely to contain it. This is the load-bearing unknown in the entire funnel. |
| 7 | Share who would pay for a dedicated capture tool | — | **NO DATA** |

### 4.1 Why I am not producing a single TAM number

Steps 4, 6 and 7 are all unknown, and they are multiplicative. Any funnel that reaches a
bottom line must invent all three, and the product of three invented fractions is not an
estimate — it is a number with the *appearance* of derivation. The brief asked for rigour
over encouragement, so: **this funnel does not close.**

What can be said with a citation is the constraint at step 3, and it is severe. If the app is
a standalone iOS player, its realistic pool is the **3.5%** of listening that already happens
on third-party premium players — the people who have demonstrated willingness to leave the
default app. That is the addressable population before any filter for genre, note-taking
propensity, or willingness to pay is applied.

### 4.2 The one bottom-up number that is real

Rather than a top-down TAM, the useful figure is the observed size of the *existing best
competitor*:

| App | Rating count (US App Store) | Status |
|---|---|---|
| Snipd | **1,142** ratings | VERIFIED via iTunes lookup, 2026-09-07 |
| Podwise | **80** ratings | VERIFIED, same |
| Airr | **delisted** (`resultCount: 0`) | VERIFIED, same |
| Overcast | (mainstream comparator) | see §5 |

Rating counts are **not** user counts. Common rules of thumb put ratings at roughly 1–5% of
installs, which would imply Snipd is somewhere in the tens of thousands of downloads —
**INFERRED, and the multiplier is a guess, so treat the order of magnitude only.**

The point survives the imprecision: **the category leader, after five years, three funding
announcements, a TechCrunch feature and Product Hunt launches, has accumulated four figures
of ratings.** That is the ceiling this product would be competing for a share of. Against a
$2–5k MRR bar and a cold start with no audience, this is the most important number in the
ticket — and it points the wrong way.

### 4.3 The comparator table that matters most

All figures VERIFIED via the iTunes Lookup API, 2026-09-07:

| App | Version | Last updated | US ratings | Avg |
|---|---|---|---|---|
| Overcast | 2026.8.1 | 2026-08-24 | **47,689** | 4.54 |
| Pocket Casts | 8.19 | 2026-08-31 | **15,664** | 4.51 |
| Castro | 2026.7.1 | 2026-07-15 | **9,177** | 4.58 |
| Snipd | 4.1.21 | 2026-08-24 | **1,142** | 4.74 |
| Podwise | 1.3.3 | 2026-08-31 | **80** | — |
| Airr | — | — | **delisted** | — |

Two readings, and both should be presented to the developer rather than one being chosen:

- **Pessimistic:** the highlight-native category (Snipd 1,142) is **~2.4% the size** of a
  single indie mainstream player (Overcast 47,689). Ten years of demand threads have produced
  a category one-fortieth the size of one competitor's ratings base.
- **Optimistic:** Snipd's 4.74 average is the **highest of the six** — the people who do want
  this want it badly. Small but intense. That is exactly the shape that can support a $2–5k
  MRR target *if* the developer can reach them, which is precisely what §2.6 says is hard.

---

## 5. Willingness to pay

### 5.1 What is verified

The only hard price point found in first-hand user speech, and notably it is a complaint:

> "However, this app is pricey; **$83.90 a year.** Is there any other app the has an auto
> chapter creation feature?"
>
> — u/woldeselassie on Snipd, r/podcasts, 2025-09-29,
> [1ntr3bz](https://reddit.com/r/podcasts/comments/1ntr3bz/i_want_to_sign_up_for_snipd_just_for_the_auto/)

Read the full post: this user was on a 30-day trial, liked the app, and explicitly said
**"I don't really care about the snipping feature"** — he wanted auto-generated chapters. The
one person found publicly deliberating a purchase in this category was willing to pay for a
*different feature than the one this product is built around*, and still balked at the price.
That is the single most instructive WTP data point in the file.

### 5.2 Adjacent-tool payment evidence — real but indirect

Evidence that people pay for the *downstream* half of this workflow is genuine:

> "I've been using spaced repetition to review highlights from books. I do it with Readwise
> (not affiliated, just a very happy customer). A large part of the reason I never stuck to
> Anki was the friction of creating, syncing, formatting the cards."
> — u/jborichevskiy, [HN, 2020-03-04](https://news.ycombinator.com/item?id=22485166)

> "It's so bad I've mostly moved to the much better Readwise. [...] **I'm probably in the
> 99th percentile of Pocket users** in terms of usage and am happily paying them for Premium."
> — u/gxqoz, [HN, 2023-07-09](https://news.ycombinator.com/item?id=36650848)

> "Reader is incredibly polished. I absolutely love it, and I'm delighted when they add new
> features. I've been on the beta for 11 months"
> — u/karlb, [HN, 2022-12-15](https://news.ycombinator.com/item?id=34007435)

**But note the direction of the money.** In every observed workflow, Readwise is the paid
destination and the podcast app is the *feeder* into it. Snipd's own users describe it this
way — *"I sync these to Readwise and they show up periodically in my Readwise review emails"*
(u/Tutwiler). A new capture-only tool is competing for the low-value, easily-substituted end
of a pipeline whose paid anchor is somebody else's product. The developer's stated plan is to
be "good at the capturing part" (echoing u/Lucoda in §1.1) — which is precisely the part users
have not been shown to pay for independently.

### 5.3 What is NOT verified

- **Readwise subscriber count or revenue:** NOT FOUND. Not disclosed.
- **Obsidian, Anki, Snipd user counts:** NOT FOUND. Snipd's "hundreds of thousands" is vendor
  marketing language with no methodology; do not cite it as a figure.
- **Any survey of willingness to pay for podcast capture specifically:** does not exist.
- **App Store review evidence:** Apple's public customer-review RSS feed
  (`itunes.apple.com/us/rss/customerreviews/...`) returned **empty payloads for every app and
  every page tried** on 2026-09-07 — it appears deprecated. This means the ticket's
  requirement to quote Overcast/Pocket Casts/Castro reviews requesting clip features **was
  not fulfilled.** I have no App Store review quotes. Rating *counts* above came from the
  still-working Lookup API. This gap should be closed by a human reading the App Store app
  directly before any decision rests on it.

---

## 6. How strong is this evidence, honestly

**Thin-to-moderate, and thinner than it looks on first read.**

What is genuinely solid:
- The pain is **real, specific, and consistently described** across nine years and two
  platforms. The hands-busy problem is not invented and the workaround tax is documented in
  users' own words. §1 would survive hostile review.
- The market-size constraint is **verified and severe**: 3.5% third-party player share,
  1,142 ratings for the category leader.

What is weak or absent, and must be labelled as such downstream:
- **No X/Twitter evidence at all** (tool failure, not absence).
- **No App Store review evidence at all** (feed deprecated).
- **No data on note-taking propensity, informational-genre share, or WTP** — the three
  fractions the funnel needs. The funnel does not close and I have not pretended otherwise.
- **Engagement volumes are tiny.** Every supporting thread found scores in single digits.
  This is the most honest summary of demand temperature available: the pain is real and
  almost nobody is loudly complaining about it.
- **Sample bias is severe and runs one way.** HN and r/PKMS are the two most
  capture-enthusiastic communities on the internet. Evidence gathered there *overstates*
  mainstream demand. The one mainstream-listener sample (§2.5) was almost uniformly negative.

The decisive asymmetry: the strongest pain evidence and the strongest counter-evidence come
from **the same subreddit and sometimes the same threads**. r/PKMS simultaneously supplies
the best workaround-tax quotes and the "podcast notes are the easiest capture trap" verdict.
A product thesis that cites the first while ignoring the second is cherry-picking its own
primary source.

### 6.1 What would change the picture

Ranked by how cheaply it could be tested:
1. Read Snipd's and Overcast's App Store reviews manually (the automated route is closed) —
   looking specifically for churn language and clip-feature requests.
2. Find out whether Overcast ships bookmarking on top of its in-progress transcripts. §1.4
   suggests it is a prerequisite already being built. If Marco Arment ships it free, the
   standalone case likely collapses.
3. Ask the 10%-revisit-rate question directly: recruit five PKM users who use Snipd today and
   ask what fraction of their snips they have ever reopened. If the answer matches §2.2, the
   capture premise needs replacing with a retrieval or synthesis premise.

