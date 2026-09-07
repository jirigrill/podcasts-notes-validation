# 07 — MRR arithmetic: what funnel does $2–5k MRR actually require?

All external benchmarks retrieved **2026-09-07**. Every line is **VERIFIED** (a figure read on a
cited page), **INFERRED** (my assumption, stated so it can be attacked independently), or
**NOT FOUND** (no source publishes it — not estimated).

---

## 0. The answer first

The base rate is the most decision-relevant number in the map, and it exists as actual
Productivity-category data rather than a proxy.

**Share of newly-launched Productivity apps that reach the bar within their first 2 years:**

| Milestone (monthly revenue) | Productivity | All categories |
|---|---|---|
| $1K | 15.3% | 17.3% |
| **$2.5K** (~the low end of the bar) | **8.8%** | 10.7% |
| **$5K** (the high end of the bar) | **5.7%** | 7.2% |
| $10K | 3.9% | 4.6% |

**VERIFIED** — RevenueCat *State of Subscription Apps 2026*, chart "Share of newly-launched apps
that hit revenue milestones in their first 2 years", basis = monthly trailing revenue (MTR).
Population: 115,000+ apps, $16B+ revenue, 2025 data, apps required to have active subscription
revenue and meet a minimum install/revenue threshold.
[Report](https://www.revenuecat.com/state-of-subscription-apps/) ·
[machine-readable chart payload](https://www.revenuecat.com/page-data/state-of-subscription-apps/page-data.json)

So: **roughly 1 in 11 reach $2.5k/mo; roughly 1 in 18 reach $5k/mo.** And that denominator
includes funded teams, apps with existing audiences, and apps with marketing budgets. A solo
developer with no audience is in the *unfavourable* tail of that population, not at its median.

There is **no $2K tier** in the published data — $2.5K is the nearest, so the bar's low end is
being measured slightly generously.

Supporting distribution figures (**VERIFIED**, same report): median monthly revenue **one year
after launch is ~$72**; median **time to first $1,000/mo is 58 days** (2026 edition, monthly basis;
the 2025 edition's near-identical 60 days measured *cumulative* revenue — different metric, do not
read as a trend).

---

## 1. Price points

### The anchors (all VERIFIED, from tickets 03 and 05, retrieved 2026-09-07)

| Product | Price | Relevance |
|---|---|---|
| **Snipd** (the direct competitor) | **$11.90/mo**, **$83.90/yr** (= $6.99/mo billed annually) | The category leader's actual charged amounts. Price unmoved ~20 months. Also runs $42.00 / $59.90 win-back SKUs. |
| **Pocket Casts Plus** | $3.99/mo, **$39.99/yr** | Shipped Smart Bookmarks 3 Sep 2026. The concept's core loop at this price, Automattic-backed. |
| **Readwise (full)** | **$9.99/mo** | Upper anchor for PKM willingness-to-pay. |
| Readwise Lite | $5.59/mo billed annually | |
| Podwise | $9.99/mo, $70.90/yr | Closest AI-summary clone. 80 ratings. |
| Podurama | $29.99/yr, **$69.99 lifetime** | The only lifetime price point in the set. |
| Overcast Premium | $19.99/yr | Largest indie player (47,689 ratings). |
| Castro Plus | $24.99/yr | |
| Airr | **delisted** — no price to anchor to | The ticket asked for Airr's pricing; the app is dead (ticket 04, `resultCount: 0`). |

Market context (**VERIFIED**, Adapty 2026, global medians 2025): **$12.99/mo**, **$38.42/yr**,
$7.48/wk. European apps charge 29–39% more than North American.

### The price I would pick

**$39.99/yr with a $6.99/mo option, no lifetime tier.** Reasoning, with the tensions stated:

- **The annual price is set by Pocket Casts, not Snipd.** Pocket Casts ships the core loop at
  $39.99/yr inside an app with ~14x Snipd's ratings and a free tier. Pricing above that requires
  arguing the product is better than a free feature in an app the user may already have. That
  argument has not been won (ticket 05).
- **Do not anchor to Snipd's $83.90.** Snipd is discounting to close ($42 win-back SKUs) and gives
  away headphone capture, CarPlay/Watch, *and* PKM export at $0 (ticket 03). The free tier, not the
  paid tier, is the real competitor.
- **Readwise's $9.99/mo is not available to this product.** Ticket 04's finding is that Readwise is
  the paid *destination* and the podcast app is the unpaid *feeder*. Pricing at the destination's
  level inverts an observed willingness-to-pay ordering.
- **Annual over monthly, against the category's own revealed preference.** This is a real conflict.
  Productivity is **77% of plans and 91% of revenue on monthly** (VERIFIED), so the category sells
  monthly. But Productivity monthly plans retain **8.78% at month 12** versus **22.88%** for yearly
  (VERIFIED) — a 2.6x durability difference. For a solo developer who cannot run a continuous
  acquisition engine, annual billing converts a retention problem into a once-a-year problem. The
  cost is slower cash feedback and a worse-looking conversion rate.
- **No lifetime tier.** Podurama offers one at $69.99, but a lifetime price caps revenue at roughly
  1.7 years of the annual plan while the COGS tail (ticket 06) runs indefinitely. At ~99% gross
  margin the COGS argument is weak; the real objection is that lifetime pricing removes the
  recurring revenue the $2–5k MRR *bar itself* is denominated in.

**INFERRED (challenge this):** that the product can hold $39.99/yr at all against a free incumbent
feature set. No willingness-to-pay survey for podcast capture exists (ticket 04: NOT FOUND), and
the one observed price deliberation was a *balk* at $83.90 — by a user who wanted a different
feature.

---

## 2. Conversion benchmarks — Productivity-specific, medians not means

All **VERIFIED** from RevenueCat *State of Subscription Apps 2026*. Every figure is an **app-level
median (P50)**, which is what the ticket asked for — the mean is dragged up by outliers.

| Metric | Productivity | All categories | Definition |
|---|---|---|---|
| **Install → paid (D35)** | **1.93%** | 1.99% (all *regions*) | "share of installs that result in at least one paid subscription within 35 days of the install date" |
| **Install → trial start (D30)** | **5.69%** | 5.79% | "share of installs that start a free trial within 30 days" |
| **Trial → paid** | **27.16%** | 31.06% | — |
| **M12 retention, monthly plan** | **8.78%** | 8.17% | subscription-level; 12 paid renewals to count as retained |
| **M12 retention, yearly plan** | **22.88%** (worst of any category) | 27.45% | 1 annual renewal |
| M6 retention, monthly plan | 18.72% | 18.33% | — |

**A cross-check I attempted and must withdraw.** The tempting move is to multiply the trial path —
`5.69% x 27.16% = 1.55%` — and present its closeness to the reported D35 of **1.93%** as independent
corroboration. **That argument does not hold, on four counts:**

1. **Different windows.** 5.69% is trial starts within **D30**; 1.93% is paid within **D35**. Not the
   same observation period.
2. **Not independent.** Trial→paid conversions are a *subset* of install→paid conversions, not a
   separate route to the same quantity. A subset cannot corroborate the whole.
3. **Medians don't multiply.** Both inputs are app-level medians (P50). The median of a product is not
   the product of the medians (Jensen's inequality), so 1.55% is not an estimate of anything
   RevenueCat measured.
4. **The gap is not small.** 1.55% vs 1.93% is a **25% relative** difference. Describing that as
   "agreement" would be motivated reasoning.

So **1.93% stands on RevenueCat's direct measurement alone, and is not independently corroborated
here.** It remains the load-bearing input in the whole ticket, and it is *un-cross-checked* — which
is a reason for more caution about the funnel, not less. I am leaving the failed check visible rather
than deleting it, because the map asks for rigour over a tidy narrative.

Caveat on "2.0%": the widely-quoted all-category 2.0% D35 is **not** an all-categories figure —
RevenueCat's category chart has no all-categories column. 1.99% is the **all-regions** median and
2.0% the mid-pricepoint median. Productivity's own 1.93% is the right number to use, and it is
mid-pack (Health & Fitness 2.87% best, Gaming 1.03% worst).

Geography matters more than category: North America D35 is **2.83%** vs **0.72%** for India/SEA.
A US-focused launch is therefore at the favourable end — **INFERRED** that this product would be
US-weighted, which is the generous assumption.

**Retention is declining year over year** (VERIFIED, all categories, 2023→2024 medians):
monthly 9.57% → 8.17%, yearly 31.21% → 27.45%, weekly 1.67% → 1.15%. All three fell. The
benchmarks used here are therefore a slightly optimistic snapshot of a worsening trend.

### Where the sources disagree — reported, not averaged

Adapty 2026 (16,000 apps, $3B) contradicts RevenueCat in ways that matter:

- **Revenue distribution, the consequential one.** Adapty: median app earns **$492/month**.
  RevenueCat: **~$72/month** one year post-launch. A ~7x gap. Adapty's population self-selects for
  apps that already bought paywall-optimisation tooling; RevenueCat's 115,000-app base includes the
  long tail of near-zero launches. **For a base-rate question, RevenueCat's figures are the better
  populated and more conservative, and are what this ticket uses.** Adapty's $492 should not be
  used as a base rate.
- **Adapty's "59.3% of subscription apps make under $1,000" is cumulative, not monthly.** It is
  *not* the complement of RevenueCat's 17.3% monthly figure. Do not subtract one from the other.
- **Plan duration.** Adapty finds weekly plans convert 1.7–7.4x better than annual and now drive
  55.5% of app revenue; RevenueCat finds weekly retains 1–2% at year one ("essentially total
  churn"). Not strictly contradictory — weekly wins upfront conversion and loses on durability —
  but the strategic conclusions point in opposite directions. I have weighted durability, because a
  solo developer cannot run the continuous acquisition that a weekly treadmill demands.
- Adapty's trial figures are **global averages** (10.9% install-to-trial, 25.6% trial-to-paid)
  against RevenueCat's medians. Mean-vs-median explains most of the gap; do not average them.

**NOT FOUND:** Adapty's Productivity-specific values (gated), its install-to-paid and monthly churn
figures. **Appfigures publishes no independent benchmark** for any of these metrics — it appears
only as a licensed data source *inside* RevenueCat's report.

---

## 3. The arithmetic, every step shown

### 3.1 A definitional choice that moves everything by 15%

Apple takes **15%** (Small Business Program, VERIFIED ticket 06). So "MRR" is ambiguous:

- **Net reading** (used throughout below): $2–5k is what reaches the developer's bank account.
- **Gross reading**: $2–5k is App Store billings, of which the developer keeps 85%.

I use the **net reading**, because a success bar that pays the developer less than the bar says is
not a success bar. Under the gross reading every payer count below **falls by 15%** — e.g. $2k at
$6.99/mo needs 286 payers rather than 337. **Flagged because it is a real ambiguity in the map's
own bar, and the developer should pick one deliberately.**

**A consequence for §0's base rate that cuts against my own framing.** RevenueCat's milestones are
measured on **monthly trailing revenue = gross billings**, not net. So its "$2.5K/mo" tier is
$2,125 net, and its "$5K" tier is $4,250 net. Read strictly, the 8.8% / 5.7% base rates are for
slightly *easier* targets than a $2.5k/$5k **net** bar — reaching $2.5k net requires ~421 payers at
$6.99/mo (~21,800 installs) rather than the 337 the net-$2k line shows. The base rate is therefore
a mild **over**statement of the probability of clearing the bar on the net reading, not an
understatement.

### 3.2 Paying users required

`payers = target MRR / (price x 0.85)`

| Price | Gross/mo | Net/mo | Payers for **$2k** | Payers for **$5k** |
|---|---|---|---|---|
| $4.99/mo | $4.99 | $4.24 | 472 | 1,179 |
| **$6.99/mo** (Snipd annual-equivalent) | $6.99 | $5.94 | **337** | **842** |
| $9.99/mo (Readwise anchor) | $9.99 | $8.49 | 236 | 589 |
| $29.99/yr | $2.50 | $2.12 | 941 | 2,354 |
| **$39.99/yr** (my pick, Pocket Casts parity) | $3.33 | $2.83 | **707** | **1,766** |
| $49.99/yr | $4.17 | $3.54 | 565 | 1,412 |
| $83.90/yr (Snipd actual) | $6.99 | $5.94 | 337 | 842 |

Worked example: `$2,000 / ($6.99 x 0.85) = $2,000 / $5.94 = 336.7 → 337 payers`.

Install figures are given to the nearest ten and derive from the **rounded** payer counts, so they
may differ by <0.2% from a fully unrounded chain. Immaterial to every conclusion here, but stated so
the arithmetic can be reproduced exactly.

### 3.3 Installs required

`installs = payers / 1.93%` (Productivity D35, VERIFIED)

| Scenario | Payers | **Installs required** |
|---|---|---|
| $2k @ $6.99/mo | 337 | **~17,460** |
| $5k @ $6.99/mo | 842 | **~43,630** |
| $2k @ $39.99/yr | 707 | **~36,630** |
| $5k @ $39.99/yr | 1,766 | **~91,500** |
| $2k @ $9.99/mo | 236 | 12,204 |
| $5k @ $9.99/mo | 589 | 30,509 |

Sensitivity on the single most important input, for $2k @ $6.99/mo (337 payers):

| Install→paid | Installs needed |
|---|---|
| 1.0% | 33,700 |
| **1.93% (Productivity median)** | **~17,460** |
| 2.87% (Health & Fitness, best category) | 11,742 |
| 5.0% (top-quartile territory) | 6,740 |
| 10.0% (INFERRED, no benchmark support) | 3,370 |

Note the annual plan needs **2.1x the installs** of the monthly plan for the same MRR, because
$39.99/yr yields less monthly revenue per payer. That is the price of the retention advantage in
§1, and it is the strongest argument *against* my own price pick.

### 3.4 App Store traffic required

**VERIFIED** — AppTweak, *Average App Conversion Rate per Category*, 2025 data, US storefront
([source](https://www.apptweak.com/en/aso-blog/average-app-conversion-rate-per-category)). These are
**averages, not medians**, and the page warns its figures "fluctuated greatly between categories and
should therefore be handled with caution":

- **Conversion Rate = app units / product page views = 8.56%**
- **Install Rate = app units / impressions = 3.8%**

**These two are parallel whole-funnel ratios, not stackable stages.** Multiplying them would be an
arithmetic error — Install Rate counts downloads made directly from search/browse results *without*
visiting the page. So each is applied separately below, giving two views of the same requirement.

| Scenario | Installs | Page views @ 8.56% | Impressions @ 3.8% |
|---|---|---|---|
| $2k @ $6.99/mo | ~17,460 | ~204,000 | ~459,000 |
| $5k @ $6.99/mo | ~43,630 | ~510,000 | ~1,148,000 |
| $2k @ $39.99/yr | ~36,630 | ~428,000 | ~964,000 |
| $5k @ $39.99/yr | ~91,500 | ~1,069,000 | ~2,408,000 |

**A trap I want to defuse rather than exploit.** ~459,000 cumulative impressions is **0.05% of one
week** of App Store visitors (Apple: "Over 850 million people visit the App Store every week",
2026, VERIFIED). Framed that way it sounds trivially achievable. It is not, and the reason is that
**raw traffic is not the constraint — qualified discovery is.** Apple's own figures say
"70% of App Store visitors use search" and "almost 65% of downloads happen directly after a search"
(VERIFIED, but footnoted *"App Store, worldwide, 2022"* — four years stale and static in Apple's
marketing for years). Search-driven downloads require ranking for queries people actually type. For
this product the high-intent queries ("podcast highlights", "podcast notes") are the ones Snipd,
Pocket Casts, and Podwise already occupy. The impression count is small against App Store scale and
large against *what an unranked app with no audience receives*, which is the number that actually
governs — and which is **NOT FOUND**.

### 3.5 The churn treadmill

Converting Productivity M12 retention into an average monthly churn, geometrically
(`churn = 1 - retention^(1/12)`):

- Monthly plan: `1 - 0.0878^(1/12)` = **18.3%/mo**
- Yearly plan: `1 - 0.2288^(1/12)` = **11.6%/mo** equivalent

**INFERRED**: that a 12-month retention figure can be flattened into a constant monthly hazard.
Real churn is front-loaded — heaviest at the first renewal — so this understates early losses and
overstates later ones. Challenge this if the shape matters.

Steady state requires `new payers/mo = payers x churn`:

| Scenario | Payers to hold | Churn | **New payers/mo** | **Installs/mo needed** |
|---|---|---|---|---|
| $2k @ $6.99/mo | 337 | 18.3% | **62** | ~3,200 |
| $5k @ $6.99/mo | 842 | 18.3% | **154** | ~7,990 |
| $2k @ $39.99/yr | 707 | 11.6% | **82** | ~4,250 |
| $5k @ $39.99/yr | 1,766 | 11.6% | **205** | ~10,610 |

**This is the finding that reframes the whole ticket.** The install totals in §3.3 are one-time
hurdles; these are **monthly, forever**. Holding $5k at $6.99/mo means finding ~154 new paying
customers every month indefinitely — roughly **8,000 installs per month**, in perpetuity, for a
product with no audience and no marketing budget, in a category where the incumbent gives the
feature away free. Reaching the bar and *holding* it are different problems, and the second is
harder.

---

## 4. The cost side (from ticket 06) — and why it does not matter

Ticket 06's architecture (a) — clip-only, on-device transcription, CloudKit storage — costs
$0.0007–$0.0114 per paying user per month.

| Scenario | Payers | Gross billings | Net after Apple 15% | COGS (typical) | COGS (all-heavy) | Margin (typical) | Margin (all-heavy) |
|---|---|---|---|---|---|---|---|
| $2k @ $6.99/mo | 337 | $2,353 | $2,000 | $0.54 | $3.84 | **99.97%** | 99.81% |
| $5k @ $6.99/mo | 842 | $5,882 | $5,000 | $1.35 | $9.60 | **99.97%** | 99.81% |
| $2k @ $39.99/yr | 707 | $2,353 | $2,000 | $1.13 | $8.06 | **99.94%** | 99.60% |
| $5k @ $39.99/yr | 1,766 | $5,882 | $5,000 | $2.83 | $20.13 | **99.94%** | 99.60% |

Both margin columns are shown because quoting only the typical figure beside an all-heavy COGS column
would be misleading — but the spread (99.94–99.97% vs 99.60–99.81%) makes no difference to any
decision.

**Apple's cut dwarfs all infrastructure combined — ~92x even if every user is heavy, ~653x at the
typical usage profile.** At $5k net the developer pays Apple ~$882/mo and the AI/storage vendors
$1.35 (typical) to $9.60 (all-heavy). Ticket 06's conclusion holds exactly: **COGS is not a
constraint, and a "don't build" verdict cannot be justified on cost.** The only scenario where this
inverts is if legal or product constraints force whole-episode transcription (architecture b), which
ticket 06 shows breaks flat-rate pricing outright.

### 4.1 The number that kills paid acquisition

This follows from the benchmarks above and is, I think, the second most decision-relevant figure
after the base rate.

```
LTV per payer   ($6.99/mo, 18.3% churn) = $6.99 x 0.85 / 0.183 = $32.38
LTV per install ($32.38 x 1.93% D35)                           = $0.62
```

So **the developer can afford to pay at most ~$0.62 per install** and break even — before valuing
their own time at anything.

| Benchmark CPI (AppTweak, US medians, 2025) | vs $0.62 breakeven |
|---|---|
| Shopping, **cheapest category published** — $1.33 | **2.1x over** |
| Games — $4.63 | 7.4x over |
| Sports, most expensive — $26.70 | 43x over |

**Productivity CPI: NOT FOUND** (AppTweak and SplitMetrics gate per-category CPT/CPI behind lead
forms). But the conclusion does not depend on finding it: the breakeven is below the *cheapest
category median published anywhere*, so **paid acquisition loses money at every price point
modelled.** At $39.99/yr LTV per install is only ~$0.47, which is worse.

Growth must therefore be entirely organic — ASO, press, community, word of mouth — which is
precisely the capability a developer with no audience lacks. **This is where the funnel actually
fails**, exactly as ticket 06 predicted it would.

Do not read "60%+ conversion rates" from Apple Search Ads marketing as a rescue: that figure is
**tap→install**, a different denominator from the install→paid economics above, and it cannot be
placed in the same column.

---

## 5. Reachability, judged plainly

### 5.1 The steelman — state it before knocking it down

The arithmetic contains a genuine counter-argument, and it deserves to be made at full strength.

Ticket 04 estimates Snipd's install base at roughly **23,000–114,000** (1,142 ratings at an
INFERRED 1–5% ratings-per-install rate — order of magnitude only). Run the funnel at Snipd's scale:

```
57,100 installs x 1.93% D35 = 1,102 payers x $6.99 x 0.85 = $6,548/mo net
```

**A defect in that calculation, which I must state because it inflates my own steelman.** It applies
a **35-day cohort** conversion rate to a **five-year cumulative** install base, and then treats the
resulting 1,102 payers as a *standing stock with zero churn* — while §3.5 insists that 18.3%/mo churn
is the finding that reframes the ticket. Both cannot be true. Those 1,102 conversions accrued across
five years, and at Productivity's retention most of them are long gone. The steady-state stock that
matters is set by **new installs per month x conversion x average lifetime**, not by cumulative
installs. So the honest version of the steelman is weaker than the $6,548 figure suggests: it
survives as "the funnel arithmetic is not absurd at leader scale", not as "the leader's base would
yield $6.5k/mo net today."

**At the category leader's scale, the bar is not arithmetically absurd.** Even at the pessimistic
end (23,000 installs) the cohort model yields ~$2,600/mo net. Reaching $2k needs a **fraction** of
the leader's cumulative install base rather than a multiple of it. Exactly what fraction depends
entirely on A5's unmeasured ratings-per-install multiplier, and I should not quote the flattering
end of it:

| Ratings/install (INFERRED) | Implied Snipd installs | $2k needs this share of it |
|---|---|---|
| 1% | 114,200 | **15%** |
| 2% | 57,100 | **31%** |
| 3% | 38,067 | **46%** |
| 5% | 22,840 | **76%** |

Note the direction: the "pessimistic" 23,000 install floor is the **5%** multiplier, which is where
the steelman is *weakest* (76% of the leader's base needed), not where it is safest.

So the honest range is **15–76%**, not the 15–30% that the optimistic end alone would suggest. The
steelman is strongest at 1–2% and becomes very weak at 5%, where the new entrant would need
three-quarters of the leader's entire five-year base. That is a real and non-trivial observation
either way, and it is why A5 is listed among the three assumptions that would most change the
conclusion.

### 5.2 Why it still fails

The steelman assumes what the whole map has spent six tickets disproving: that a new entrant can
reach a meaningful fraction of the leader's scale. Against that:

1. **The base rate is 8.8% / 5.7%** for $2.5k / $5k — and that population includes funded teams with
   audiences. Nothing in tickets 01–06 places this project *above* that median; several findings
   place it below.
2. **Snipd took five years, $700k pre-seed, a team of five, three Product Hunt launches, and a
   TechCrunch feature** to reach 1,142 ratings (VERIFIED, ticket 03). The steelman's "just reach
   30% of Snipd" is 30% of an outcome that consumed resources the solo developer does not have.
3. **Snipd gives away the exact feature set this product would charge for** — headphone capture,
   CarPlay/Watch, PKM export, all free (VERIFIED, ticket 03). The steelman silently assumes a payer
   conversion rate drawn from apps that are not competing against a free version of themselves.
   **The 1.93% D35 median is therefore optimistic in this specific competitive position** — and D35
   is the input the entire funnel pivots on.
4. **Pocket Casts shipped the core loop on 3 Sep 2026** into a free tier with ~14x the ratings
   (VERIFIED, ticket 05). The install ceiling is being lowered as the arithmetic is being written.
5. **The treadmill, not the target, is binding**: ~8,000 installs/month forever at $5k, with paid
   acquisition ruled out at any price by §4.1.
6. **Demand volume is tiny**: best-ever "does this app exist?" post in r/podcasts got 7 upvotes, and
   the target segment reports ~10% of captures ever revisited (VERIFIED, ticket 04).

### 5.3 Verdict on reachability

**$2k MRR is reachable in principle and unlikely in practice; $5k MRR should be treated as out of
reach for this concept as specified.**

The failure is not the arithmetic — the arithmetic closes at plausible scale, and costs are
irrelevant (§4). The failure is **distribution against a free incumbent**, and it shows up as three
independent walls that must *all* be cleared:

| Wall | Requirement | Status |
|---|---|---|
| Base rate | Beat a 5.7–8.8% category outcome | No evidence this project is above the median |
| Acquisition | ~17,500 installs cold, then ~3,200/mo forever ($2k @ $6.99/mo) | Paid ads lose money at $0.62 breakeven CPI; organic requires the audience the developer lacks |
| Differentiation | A reason to pay when Snipd is free and Pocket Casts is bundled | Ticket 05: 5 of 9 differentiators already evaporated |

### 5.4 Time to get there — partially answered

The ticket asked how long a cold start plausibly takes. The only VERIFIED anchors are
RevenueCat's **median 58 days to first $1,000/mo** and **~$72 median monthly revenue one year after
launch**. Note these two are in tension and both are all-category, not Productivity: the 58-day
median is conditioned on apps that *reach* $1k at all (a ~15–17% minority), while the ~$72 median
describes the whole population. Read together they say **the typical launch does not get there, and
the ones that do get there fast.** That pattern — fast success or none — suggests early signal is
informative, which is the one genuinely encouraging structural fact in this ticket.

A dedicated search for **named indie iOS developers with published month-by-month revenue timelines**
returned after the arithmetic above was written. Its findings are consistent with, and sharpen, the
picture. All figures are **self-reported by the developers**, which is the only form this evidence
takes:

**The base case — HabitKit (Sebastian Röhl), the closest thing to a genuine no-audience cold start:**

| Point | Figure |
|---|---|
| Launch day | **$13 MRR** |
| Month 4 | **$400 MRR** |
| Month 6 | ~$1.5k/mo — judged insufficient; he **returned to salaried work** |
| ~Month 9 | Inflection, which the developer **attributes** to organic App Store keyword ranking for "habit tracker", reporting no metadata change and no viral post |

That month-9 attribution is a **single self-reported case with no counterfactual** — a ranking change
and a revenue change coinciding is not proof of cause, and it is the developer's own read. Treat it as
the most plausible available mechanism, not as established causation.

Read this as the base case rather than the ceiling: **month six looked like failure.** Runway must be
planned on that assumption. The inflection came from a mechanism — ranking a high-volume, plainly
named consumer search term — and that is exactly where this product is structurally weakest.
"Podcast notes" / "podcast highlights" is a far thinner query, and Snipd already occupies it *with a
free tier*. This argues that **a keyword strategy should be validated before building, not after**,
and it corroborates §3.4's point that qualified discovery, not raw traffic, is the constraint.

**The sharpest single data point in the set — FocusKit, the same developer's follow-up:** launched
with 20,000 X followers, a 1,225-subscriber newsletter, and a $600k/year app to cross-promote from,
it produced **$874 total revenue and $52 MRR in month one**. **Audience does not substitute for a
distribution mechanism.** If the plan depends on one, that is the assumption to test first — and this
developer had far more audience than the subject of this map.

**On App Store features — do not model one as a growth channel.** The nomination channel is genuinely
open, but Röhl applied and received nothing; another developer (Sinclair) got two features and **no
sales spike**; and the only measured lift data found is eight years stale.

**The recurring failure modes are demand and distribution, never craft.** Named cases: QuickReps
never validated the problem; Rithm shipped a vitamin rather than a painkiller; Respawn had 4.2% D1
retention after four onboarding rebuilds. None failed on code quality. RabbitHole may be a prior
attempt in this category, but the evidence found is thin and I would not lean on it.

**Two survivorship caveats, and they compound rather than offset.** First, published timelines exist
only because those developers chose to publish, which correlates with articulateness and emotional
distance from the outcome — so the true median outcome sits *below* the worst case documented here.
Second, that research also ran through a captcha-blocked network; discovery leaned on Hacker News and
the Apple blogosphere, i.e. developers *with* an audience, and the r/iOSProgramming and r/SideProject
revenue posts — which skew smaller and more anonymous — were inaccessible. **The case set is
incomplete precisely on the low end.**

---

## 6. Every assumption, so each can be attacked independently

| # | Assumption | Value | Status / basis |
|---|---|---|---|
| B1 | Base rate for the bar | 8.8% ($2.5K), 5.7% ($5K) | **VERIFIED** — RevenueCat 2026, Productivity, newly-launched, 2-year window, MTR basis |
| B2 | Install→paid conversion | **1.93%** | **VERIFIED** median (Productivity D35). **Not** independently cross-checked — the trial-path check fails (§2) |
| B3 | Trial start / trial→paid | 5.69% / 27.16% | **VERIFIED** medians, Productivity |
| B4 | M12 retention | monthly 8.78%, yearly 22.88% | **VERIFIED**, subscription-level medians |
| B5 | Apple's cut | 15% | **VERIFIED** — Small Business Program (ticket 06) |
| B6 | Page-view→install / impression→install | 8.56% / 3.8% | **VERIFIED** but **averages, not medians**, US 2025, vendor-owned dataset with self-declared volatility |
| A1 | "$2–5k MRR" means **net** to the developer | net reading | **INFERRED.** Gross reading cuts every payer count by 15% (§3.1) |
| A2 | M12 retention flattens to a constant monthly churn | 18.3% / 11.6% | **INFERRED.** Real churn is front-loaded; understates early losses |
| A3 | Launch is US-weighted | — | **INFERRED**, and *generous*: NA D35 is 2.83% vs 0.72% India/SEA |
| A4 | The 1.93% median applies to an app competing with a free incumbent | — | **INFERRED and probably optimistic** — see §5.2 item 3. The most attackable assumption here |
| A5 | Snipd install base | 23k–114k | **INFERRED** from 1,142 ratings at 1–5% (ticket 04). Order of magnitude only |
| A6 | COGS per user | $0.0007–$0.0114/mo | **INFERRED** — verified vendor prices, but ticket 06's usage profiles (clips/mo, episode length, token counts) are themselves inferred |
| A7 | No free tier modelled | — | **INFERRED.** A free tier would raise installs and lower D35 — unmodelled, and it is what Snipd actually does |
| A8 | Churn is independent of price | — | **INFERRED and known-false in direction.** Productivity's *worst-in-category* 44% cost-related churn (VERIFIED) means a higher price raises churn |

### The three that would most change the conclusion if wrong

1. **A4 / B2 — install→paid against a free incumbent.** Everything scales linearly off 1.93%. If the
   true figure is 1%, installs required double; if 5%, the picture improves materially. This is the
   number to instrument first.
2. **A5 — Snipd's install base.** The whole steelman in §5.1 rests on a 1–5% ratings multiplier that
   is a guess. If Snipd is at 23,000 installs rather than 114,000, the reachable ceiling is far lower.
3. **B1 — whether the base rate applies.** It is drawn from apps that launched and had subscription
   revenue. Selection effects cut both ways and are not quantified.

---

## 7. What could not be verified

Stated as gaps, not estimated.

- **Organic download volume for a new no-audience iOS app.** **NOT FOUND** — no published median
  first-month or first-year download figure for a new subscription app. This is the largest gap in
  the ticket: it is precisely the input needed to convert §3's install requirements into a timeline.
  Appfigures' Insights archive, ASO guides, and AppTweak's methodology pages contain no
  download-distribution data. Realistic paths are Appfigures Explorer (paid) or an Apple Analytics
  pull, not published benchmarks.
- **Named indie revenue timelines — now partially answered (§5.4), but incomplete on the low end.**
  The case set skews toward Hacker-News-visible developers *with* audiences because the searches ran
  through a captcha-blocked network; r/iOSProgramming and r/SideProject revenue posts, which skew
  smaller and more anonymous, were unreachable. Combined with publication bias (developers who fail
  rarely blog), **the documented cases overstate reachability and the true median sits below the worst
  case recorded.** Worth one more pass before ticket 09 if a working search index is available.
- **Productivity-category CPI/CPT for Apple Search Ads.** **NOT FOUND** — gated behind lead forms at
  AppTweak and SplitMetrics. Immaterial: §4.1's breakeven of $0.62 sits below the cheapest category
  median published anywhere, so the conclusion holds without it.
- **$2K monthly milestone.** Does not exist in RevenueCat's data; $2.5K is the nearest tier, so the
  bar's low end is measured slightly generously.
- **Productivity figures from Adapty**, and any independent Appfigures benchmark. **NOT FOUND.**
- **Willingness to pay for podcast capture specifically.** **NOT FOUND** (ticket 04) — so §1's price
  pick rests on competitor anchors, not on measured demand.
- **A methodological caution on §3.4.** The traffic-conversion research ran with a broken WebSearch
  API and worked from directly-guessed vendor URLs. The two figures used (8.56%, 3.8%) were read on
  the page and are solid; the NOT FOUNDs in that area are weaker — "could not reach it" is not
  "not published."

---

## 8. Conclusions

1. **The base rate is 8.8% for $2.5k/mo and 5.7% for $5k/mo** among newly-launched Productivity
   apps in their first two years — actual category data, not a proxy. The ticket asked for the single
   most decision-relevant number in the map; this is it, and it is unfavourable.
2. **The arithmetic itself is not the obstacle.** $2k needs ~337 payers at $6.99/mo (~17,460
   installs); $5k needs ~842 (~43,630). At the category leader's estimated scale the model clears the
   bar. The concept is not arithmetically impossible.
3. **Distribution is the obstacle, and it is decisive.** Paid acquisition is ruled out at every
   modelled price — breakeven is **$0.62 per install** against a cheapest-published-category median
   CPI of $1.33. Growth must be organic, which requires the audience the developer does not have.
   And audience alone is not sufficient either: the FocusKit case (§5.4) shows a developer with
   20,000 followers and a $600k/yr app to cross-promote from launching to **$52 MRR in month one**.
   What is needed is a *distribution mechanism* — for the one documented cold-start success, organic
   App Store ranking on a high-volume search term, which is the asset this product is least able to
   acquire.
4. **The treadmill is worse than the target.** Holding $5k at $6.99/mo needs ~154 new payers and
   ~8,000 installs *every month, indefinitely*, in a category whose monthly plans retain 8.78% at
   twelve months.
5. **Costs are irrelevant to the decision.** Net margin is 99.94–99.97% at the *typical* usage profile
   and still 99.60–99.81% if **every** user is heavy; Apple's cut is
   ~92–653x all infrastructure combined, depending on usage profile. Ticket 06's finding is confirmed: **a "don't build" verdict
   cannot be justified on cost, and must be argued on demand and distribution.**
6. **Annual pricing is the least-bad structure and it is genuinely a trade-off.** $39.99/yr matches
   Pocket Casts, and yearly plans retain 2.6x better than monthly — but need 2.1x the installs for
   the same MRR, and Productivity's yearly retention is the worst of any category (22.88%).
7. **For ticket 09**: nothing here rescues the concept, and the arithmetic sharpens rather than
   softens tickets 03–05. The most defensible reading is that **$2k is a low-probability outcome and
   $5k should not be planned for.** The one structurally encouraging fact is that apps reaching $1k
   do so fast (median 58 days), so a cheap launch would produce an informative signal quickly — which
   makes a *time-boxed* experiment more defensible than a long build. Temper it with the one
   documented cold-start case: HabitKit's inflection came at **month nine**, and month six looked
   like failure. So a time box drawn at six months would have killed the single success in the
   evidence set — the box must be defined by *signal*, not by elapsed calendar time.
8. **The cheapest decisive test is not code.** Two findings converge on this: the binding constraint
   is organic App Store discovery (§3.4, §5.4), and the only documented cold-start success was won on
   keyword ranking. So the highest-value next step is a **keyword-demand check on "podcast notes" /
   "podcast highlights" against Snipd's and Pocket Casts' existing rankings** — answerable before
   writing any app code, and it directly attacks assumption A4, the most attackable input in the
   ticket.
