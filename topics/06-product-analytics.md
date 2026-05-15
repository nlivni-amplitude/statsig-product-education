---
topic: product-analytics
source_modules:
  - Statsig 1 / Module 4 — Product Analytics Deep Dive
  - Statsig 2 / Module 5 — Product Analytics
amplitude_counterpart: "Amplitude Analytics"
---

# Product Analytics

Statsig's analytics surface: Dashboards, Metric Drilldown, Funnels, User Journeys, Retention, Distribution. The "what are users doing" half of the loop.

## Learning Objectives

### LO1. Choose the right chart type for a question.

**Prompt:** *For each of these questions, pick the Statsig chart type that answers it most directly: (a) Where in the sign-up flow are users dropping off? (b) Are users coming back after 7 days? (c) Which users use feature X heavily vs. lightly? (d) What did users do *between* searching and purchasing?*

**Canonical answer:**
- (a) **Funnel** — staged conversion through an ordered set of events.
- (b) **Retention** — % of users returning after a triggering event, over time intervals.
- (c) **Distribution** — histogram of behavior across a user population. Shows the long tail vs. the bulk.
- (d) **User Journey** — flows users took between two events. Reveals unexpected paths.

The bonus chart: **Metric Drilldown** — investigate why a single metric moved. Use it when *one chart* changed and you want to slice the why.

---

### LO2. Build a meaningful metric definition.

**Prompt:** *Your team wants to track "engagement." That's too vague to measure. Walk through how you'd turn that into a specific, measurable metric definition.*

**Canonical answer:** "Engagement" alone is meaningless until you specify:
- **The event** that proxies engagement (session_started? feature_used? content_viewed?)
- **The unit** (per user per day, per user per session, total)
- **The qualifier** (any feature, or specific ones; >= X seconds; with a follow-up action)

Example specific definitions:
- "Daily active users" — distinct users with ≥1 `app_opened` event per calendar day
- "Engagement depth" — count of distinct features used per session per user
- "Meaningful sessions" — sessions ≥60 seconds AND with ≥1 non-navigation event

**The principle:** log every event that *could* be a proxy for the behavior. Define the metric in Statsig's Metric Catalog by combining those events with filters and aggregations.

---

### LO3. Design a Funnel with the right number of steps.

**Prompt:** *A PM hands you a 7-step funnel they want to track. Why is 7 probably too many, and how would you slim it down?*

**Canonical answer:** **The drop-off problem.** Each step compounds attrition. A 7-step funnel that converts at 80% per step ends at 0.8^7 ≈ 21%. Tiny per-step issues become invisible inside the noise of overall attrition. You also can't tell which step is "the real one" — you have seven candidates.

**Slim it down:**
- Identify 3-5 **decision points** that matter (where the user actually chooses to continue or quit) and ignore mechanical steps (loading screens, transitional pages).
- Group consecutive trivial steps into a single funnel step ("completed registration" rather than "filled name → filled email → filled password → clicked submit").
- Use separate funnels for separate user journeys rather than one giant funnel that tries to capture everything.

The best funnels surface where the user is making a *decision*, not where the app is doing housekeeping.

---

### LO4. Decide between Retention and User Journeys.

**Prompt:** *A PM asks "are users coming back?" — that could be a Retention or a User Journey question. How do you decide, and what does each answer that the other can't?*

**Canonical answer:**
- **Retention** answers **"do they come back?"** — % of users from cohort X who returned at day N. Bucketed, time-based. Compares behavior across cohorts (e.g., does the new onboarding cohort retain better than the old one?).
- **User Journeys** answers **"what did they do?"** — the paths users took between events. Reveals unexpected sequences ("I thought everyone who searched went to checkout, but 30% bounce to the help page first").

**Use Retention when** the question is binary or rate-based: did they come back, how many, over what window.
**Use User Journeys when** the question is about *paths*: what's the typical sequence, what surprising paths exist, where do users go that we didn't expect.

Most PM questions about "engagement" map to Retention. Most PM questions about "user behavior" map to Journeys.

---

### LO5. Build a Dashboard that answers a question.

**Prompt:** *A PM asks for "a dashboard showing how the new feature is doing." That request is too vague. What questions would you push back with, and what would the resulting dashboard contain?*

**Canonical answer:**
**Push back with:**
- **For whom is this dashboard?** (Exec checking quarterly? PM watching daily? Engineer debugging a regression?) Each audience needs different charts.
- **What decision will it inform?** ("Is the feature working?" → primary success metric. "Should we expand it?" → adoption + retention.)
- **What's the comparison?** (Vs. before launch? Vs. control group? Vs. another feature?)

**A focused dashboard contains** 3-7 charts max, each answering one question:
- Headline: 1-2 KPIs at the top (adoption rate, primary success metric)
- Diagnostic: 2-3 supporting charts (segmentation, time series, funnel)
- Optional: a "concerns" section (guardrails, error rates)

A dashboard that throws 30 charts at the wall doesn't get used. It gets ignored.

---

### LO6. Use Metric Drilldown to investigate a movement.

**Prompt:** *Your primary metric jumped 12% last Tuesday. You don't know why. How do you use Metric Drilldown to figure it out?*

**Canonical answer:** Metric Drilldown lets you slice a single metric by user properties, event properties, time, and source to find what's driving the change.

**Investigation path:**
1. **Time** — was it a single-day spike or a sustained shift? Spike → likely external (campaign, news event, bug). Sustained → likely a feature or marketing change.
2. **User segment** — was the lift uniform, or concentrated in one cohort (new users? a specific country? a paid plan tier?). Concentration tells you where the change came from.
3. **Event source** — was it driven by one specific event, or many? One event = a specific surface change. Many = a broad shift.
4. **Compare windows** — same metric, same slice, one week prior. Compare.

If you find one slice contains the entire lift, that's your culprit. If it's distributed evenly, look for a global change (campaign, viral moment, instrumentation change).

---

### LO7. Use Distribution when mean/median would mislead.

**Prompt:** *Average revenue per user is $50. Why is that often misleading, and what does a Distribution chart show you that the average hides?*

**Canonical answer:** Averages collapse a population into a single number. A $50 average could come from:
- Everyone spending exactly $50 (homogeneous)
- 50% spending $0 and 50% spending $100 (bimodal)
- 95% spending $5 and 5% spending $950 (whale-driven, long tail)

The product implications are completely different. In the third case, your business depends on a tiny segment — losing 1% of whales is catastrophic. In the first, the population is robust.

**Distribution chart** shows the actual shape: where users cluster, where the long tail is, what % falls into which buckets. It surfaces the bimodality or skew that averages hide.

**Rule of thumb:** any time someone quotes an average for behavioral data, suspect skew until you've seen the distribution.

---

### LO8. Contrast Statsig PA with Amplitude Analytics.

**Prompt:** *How does Statsig Product Analytics compare to Amplitude Analytics? Where does the mapping work cleanly, and where doesn't it?*

**Canonical answer:** **Maps cleanly:**
- Funnels, Retention, Dashboards → near-1:1 conceptually.
- Both support event taxonomy, user properties, custom event types.
- Both have a SQL-like or query-builder layer underneath.

**Where it diverges:**
- **Maturity** — Amplitude Analytics has been the core Amplitude product for years; the depth of features (Pathfinder, Compass, Personas, Stickiness, Recommendations) is broader.
- **Metric model** — Statsig leans on a first-class **Metric Catalog**: define a metric once, use it everywhere (in experiments, dashboards, charts). Amplitude is more event-stream-shaped: events flow in, and you build the metric ad-hoc in each chart (with custom metrics available, but less central).
- **Naming** — "Metric Drilldown" ≈ Amplitude's segmentation; "User Journeys" ≈ Pathfinder/Compass; "Funnels" and "Retention" share names.

**For a customer:** if they're heavy on Metric Catalog as a configuration tool, mapping to Amplitude means lifting metrics into custom-event-types and saved cohorts. Doable but a different mental model.
