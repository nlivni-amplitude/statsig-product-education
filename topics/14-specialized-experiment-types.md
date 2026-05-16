---
topic: specialized-experiment-types
source_modules:
  - LXD-synthesized from docs.statsig.com (May 2026)
amplitude_counterpart: "Mostly none; Amplitude Experiment is unit-randomized A/B only"
---

# Specialized Experiment Types

Statsig supports several non-standard experiment designs that aren't taught in the Academy courses. These are the experiment types Ampliteers will hear about and need to know exist — even if most teams won't run them often.

## Learning Objectives

### LO1. Recognize when a Switchback test is appropriate.

**Prompt:** *What's a Switchback test, and why use it instead of a standard A/B?*

**Canonical answer:**

A **Switchback test** randomizes at the **time-and-place** level instead of the user level. Example: a city is in "treatment" for 30-minute windows and "control" for the next 30 minutes, with random switching.

**When to reach for it:**
- **Marketplaces and two-sided systems** where one user's experience depends on what other users see (Uber pricing, DoorDash dispatch, Airbnb search ranking). A user-randomized A/B test contaminates the marketplace because every user is interacting with the same shared system.
- **Network effects:** treatment users influence control users' experience (social feeds, group features).
- **Anywhere the unit of treatment is the place/time, not the person.**

**Why standard A/B fails here:**
If half your riders are in "new dispatch algorithm" and half in "old," they're competing for the same drivers. The algorithm's behavior under contention bleeds across arms. You can't isolate the effect.

**How switchback fixes it:**
At any given moment, the entire region is on one variant. The variant changes on a randomized schedule. You compare metric values during treatment-windows vs. control-windows.

**Costs:**
- **More noise per arm** — variation between time windows (day-of-week, weather) instead of between users.
- **Bigger sample requirements** to overcome that noise.
- **Operational complexity** — the system has to handle the switch cleanly with no inflight contamination.

**Common pitfalls:**
- **Carryover effects.** If the treatment has a multi-hour effect (e.g., changed driver supply), the next control window is biased. Common fix: a "buffer period" between switches.
- **Cyclical bias.** If your switching frequency aligns with weekly patterns, you contaminate the comparison. Randomize the switching interval.

**Amplitude counterpart:** none. Amplitude Experiment is unit-randomized only. Marketplaces using Amplitude typically don't run experiments on the marketplace mechanism itself.

**Where to go for depth:** `https://docs.statsig.com/experiments/types/switchback`.

---

### LO2. Recognize when a Geo-test is appropriate.

**Prompt:** *What's a Geo-test, and what kind of question does it answer?*

**Canonical answer:**

A **Geo-test** randomizes at the **geographic-region** level. Some markets (cities, states, DMAs) get treatment; others get control.

**When to use:**
- **Marketing channels that target geographically** — TV, billboards, regional radio, geo-targeted digital. You can't randomize an individual user away from a city's TV ad.
- **Network effects across users in a region** (similar to switchback but bigger time horizon).
- **Brand campaigns** where the effect is on a population, not an individual.

**vs. Switchback:**
- Switchback = same place, randomized in time.
- Geo-test = different places, fixed for the duration of the test.

**The hard part: synthetic control.**
Markets aren't randomly assigned to treatment in real life. You typically have, say, 10 markets in treatment and 10 in control, and you need to confirm that pre-test, the treatment markets and control markets behaved similarly.

Statsig (and most platforms) use a **synthetic control** technique:
- Build a weighted combination of control markets that mimics the treatment markets' pre-test history.
- Compare treatment markets vs. that synthetic baseline during the test.
- Differences between observed and synthetic are attributed to treatment.

**Costs:**
- **Small N at the market level.** 20 markets vs. 20,000 users — confidence intervals are much wider.
- **Long test durations** — usually weeks or months to overcome the noise.
- **Confounders.** A competitor launching in your control markets messes up the synthetic baseline.

**Amplitude counterpart:** none directly. Geo-tests are typically run on dedicated marketing measurement platforms (Meta GeoLift, Google Geo Experiments, Recast).

**Where to go for depth:** `https://docs.statsig.com/experiments/types/geo-test` and `https://docs.statsig.com/statsig-warehouse-native/geotests/`.

---

### LO3. Recognize an SEO test and what makes it tricky.

**Prompt:** *Can you A/B test SEO changes, and what's the right design if so?*

**Canonical answer:**

**SEO tests** target a question like "does this title-tag change improve organic traffic?" or "does this page-template variant rank better?". You can't randomize by user (Google sees pages, not users), so the unit is the **page** or the **page-template**.

**Common designs:**
- **Page-level A/B:** half of your eligible pages get template A, half template B. Compare organic traffic and rankings per page.
- **Time-based:** apply a change to all pages, compare before/after with a synthetic-control-like model that accounts for seasonality. Weaker — confounded with everything else happening.

**Why it's hard:**
- **Google ranking is slow to update.** Effects take weeks to materialize and are noisy.
- **Search-result randomness.** A query you tested at position 4 may be at position 6 next week with no template change.
- **Network effects across pages.** Internal linking, sitewide signals — changes to a subset of pages can affect the whole site's rankings.
- **Cannot use Statsig's standard targeting** — the user isn't the unit, and the user isn't on your site yet when Google decides ranking.

**Common pitfalls:**
- **Implementation that confuses Google.** Cloaking (showing different content to Googlebot than to users) can get the site penalized. The variants must be served deterministically per URL.
- **Too few pages per arm.** If you only have 50 eligible pages, the noise is massive. SEO tests want hundreds to thousands of pages per arm.
- **Mixing in non-SEO changes.** A redesign that also changes the marketing message will move SEO and conversion together — you can't tease apart cause.

**Amplitude counterpart:** none. SEO testing is its own discipline; most teams use specialized tools (SearchPilot, Distilled ODN) or ad-hoc page-level analytics.

**Where to go for depth:** `https://docs.statsig.com/experiments/types/seo-testing`.

---

### LO4. Understand CDN edge testing.

**Prompt:** *What is CDN edge testing, and why would I serve experiment variants from the edge?*

**Canonical answer:**

**CDN edge testing** moves the experiment-assignment decision from the application (server or client) to the **CDN edge** (e.g., Cloudflare Workers, Fastly Compute, Vercel Edge). The CDN evaluates the user's bucketing, decides which variant to serve, and returns the appropriate HTML/asset response.

**Why do this:**
- **No flicker / no client-side variant swap.** Standard client-side experiments often render the control, then JS swaps to treatment — visible flash. Edge assignment serves the right variant in the first byte.
- **Faster first paint.** No round-trip to your origin server to look up the gate value.
- **SEO-safe.** Search engines see the rendered variant directly; no JS execution required.
- **Works for static / marketing pages** where you don't have a running server-side application logic for every page.

**Costs:**
- **Operational complexity.** Your CDN configuration becomes part of the experimentation surface — needs versioning, deploy hooks, monitoring.
- **Limited bucketing context.** The edge knows whatever's in the request (cookies, headers, URL). It doesn't know your application state (logged-in user attributes, account tier) unless that's in a cookie.
- **Provider lock-in.** Cloudflare Workers vs. Fastly Compute have different APIs.

**When it's worth it:**
- Marketing site experiments (landing pages, hero text, CTA copy).
- Performance-sensitive experiments where the flicker / latency cost of client-side testing is unacceptable.
- SEO-impacting experiments where you need the variant visible in the initial HTML.

**Amplitude counterpart:** none directly. Some Amplitude customers achieve similar outcomes via custom integration with their CDN, but it isn't a packaged offering.

**Where to go for depth:** `https://docs.statsig.com/guides/cdn-edge-testing`.

---

## When to point to live docs

For specific platform configuration (UI flow to set up a switchback test, exact CDN provider integration steps), point learners to the docs URLs above. The general methodology in this topic file applies regardless of platform UI.

## Why this topic exists

The coverage-audit at `data/synthesized/coverage-audit.md` flagged Switchback, Geo-tests, SEO tests, and CDN edge testing as zero-coverage gaps — Statsig has docs but our Academy / caption / topic content doesn't name them. Most Ampliteers won't run these often, but they will come up in conversations with Statsig customers who do. This topic gives the skill enough grounding to explain what they are and when they apply.
