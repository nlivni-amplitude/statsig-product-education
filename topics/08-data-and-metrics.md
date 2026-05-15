---
topic: data-and-metrics
source_modules:
  - Statsig 3 / Module 3 — Connect Events and Metrics
amplitude_counterpart: "Amplitude event taxonomy + Custom Metrics"
audit_note: "CUPED mechanics are introduced but not deeply explained in the corpus."
---

# Data and Metrics

How events get into Statsig, how the Metric Catalog works, warehouse-native vs. cloud ingestion, and variance reduction with CUPED.

## Learning Objectives

### LO1. Choose the right ingestion path.

**Prompt:** *A customer is deciding how to get events into Statsig. They use Segment for product analytics already, have a Snowflake warehouse, and have an internal mobile SDK. What ingestion paths could they choose, and what's the trade-off of each?*

**Canonical answer:** Three viable paths, each with different trade-offs:

1. **Direct via Statsig SDK** — instrument events through `statsig.logEvent()` calls in their codebase.
   - **Pros:** lowest latency, tightest integration with exposure logging, no third-party in the path.
   - **Cons:** duplicate work if they're already instrumenting in Segment.

2. **Via a CDP (Segment, RudderStack)** — pipe their existing CDP event stream into Statsig.
   - **Pros:** zero new instrumentation, reuse what's already wired.
   - **Cons:** dependent on the CDP being healthy; introduces a hop of latency; event schema is whatever the CDP delivers.

3. **Warehouse-native (Snowflake)** — Statsig queries directly from their warehouse, no event ingestion at all.
   - **Pros:** data never leaves their environment; works for batch-historical analysis; can use existing analytics tables.
   - **Cons:** not real-time (whatever the warehouse refresh cadence is); requires the warehouse schema to be appropriately modeled.

**Most customers** combine: warehouse-native for big metric tables + SDK for real-time exposures.

---

### LO2. Build a metric in the Metric Catalog.

**Prompt:** *Walk through how you'd build a metric in Statsig's Metric Catalog for "% of users who completed onboarding within their first session." What configuration choices matter most?*

**Canonical answer:**
1. **Pick the source** — typically an event (e.g., `onboarding_completed`) or a derived computation.
2. **Choose the metric type:**
   - **Rate / conversion** — % of users who did X. (This is the right pick here.)
   - **Count** — total events.
   - **Mean / sum** — average or sum of a numeric property.
3. **Add filters** — restrict to `first_session = true` or session_number = 1.
4. **Set the unit** — per user (so the % is users-based, not events-based).
5. **Aggregation window** — within a session, daily, weekly, all-time? For "first session" specifically, the window is per-user-first-session.
6. **Optional: CUPED** — variance reduction, useful if this metric will be used in experiments.

**Why these matter:** the same event can produce wildly different metrics. "Users who did X" vs "events of X per user" vs "events of X per session" answer different questions. Sloppy metric definitions are how teams ship "winning experiments" that didn't measure what they thought.

---

### LO3. Recognize when CUPED is worth turning on.

**Prompt:** *Statsig (and Amplitude Experiment) offer CUPED for variance reduction. What is CUPED at a conceptual level, and when does it actually help?*

**Canonical answer:** **CUPED (Controlled-experiment Using Pre-Experiment Data)** uses each user's pre-experiment behavior as a covariate to reduce noise in the experiment-period measurement. Conceptually: instead of measuring "what did user X do during the experiment," measure "how much did user X *change* from their pre-experiment baseline." That removes the variance contributed by users naturally being high-spenders or low-spenders.

**Helps most when:**
- The metric has high user-level variance (revenue, engagement minutes, session counts)
- Pre-experiment data exists for the same users (you've been tracking them for weeks before the experiment)
- The user population is stable (the same users are likely in pre- and during-experiment windows)

**Helps less when:**
- The metric is on first-time users (no pre-experiment data)
- Variance is already low (e.g., a binary conversion event)
- The pre-experiment period was atypical (e.g., a sale or seasonality skew)

**Note:** the corpus introduces CUPED but doesn't deeply explain the math. For implementation specifics, check Statsig docs.

---

### LO4. Connect a warehouse for warehouse-native experiments.

**Prompt:** *You're setting up Statsig in warehouse-native mode against a Snowflake warehouse. What's the high-level flow, and what configuration is critical to get right?*

**Canonical answer:**
1. **Create a metric source** — point Statsig at the warehouse (Snowflake, BigQuery, Redshift, Databricks). Provide credentials and the table/view to query.
2. **Configure the schema mapping** — Statsig needs:
   - **Unit ID column** — the user/account identifier the experiment unit is bucketed on
   - **Timestamp column** — when the event happened (used for windowing and freshness)
   - **Event/metric value columns** — what to measure
3. **Build metrics** referencing this source — same Metric Catalog flow as cloud, but the source is the warehouse table.
4. **Run experiments** — Statsig queries the warehouse on a schedule (vs. real-time streaming in cloud mode).

**Critical to get right:**
- **Unit ID consistency** — if the warehouse uses `user_id` but exposures use `stable_id`, your joins will silently miss most of the data.
- **Timestamp timezone / format** — UTC mismatches lead to events appearing in the wrong day.
- **Permissions** — Statsig needs read access to the table; least-privilege role recommended.

**For warehouse-native results:** the experiment results page shows the same scorecard concepts (CIs, lift, p-values) but the underlying compute happens in your warehouse, not Statsig's.

---

### LO5. Contrast Statsig's Metric Catalog with Amplitude's event-stream model.

**Prompt:** *How does Statsig's Metric Catalog approach differ from Amplitude's event-stream + custom metrics? What does the difference mean for someone migrating?*

**Canonical answer:**
**Statsig Metric Catalog** is the central, first-class place where metrics are defined. You name a metric, configure it (source, type, filters, aggregation), and then reference that named metric anywhere — in experiments, dashboards, charts. Change the definition once and every consumer updates.

**Amplitude** is more event-stream-shaped. Events flow in, you define event taxonomy, and most metrics are built ad-hoc inside each chart (with custom event types and saved cohorts as the closest analog to a metric catalog). Custom Metrics exist as a feature but they're less the dominant mental model.

**For a migrator from Statsig to Amplitude:** the customer probably has a Metric Catalog with 50-200 metric definitions. Mapping that into Amplitude means:
- Standardize the underlying events first (Amplitude needs event taxonomy to be clean)
- Create the metrics as Custom Events or Custom Metrics where direct equivalents exist
- Recreate saved cohorts for any user-segment metrics
- Accept that some metrics may not need to exist in Amplitude (they may have been built around Statsig-specific constructs)
