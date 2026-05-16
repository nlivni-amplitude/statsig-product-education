---
topic: newer-statsig-surfaces
source_modules:
  - LXD-synthesized from docs.statsig.com (May 2026)
amplitude_counterpart: "Mostly none; Web Analytics has a partial Amplitude analog"
---

# Newer Statsig Surfaces

Statsig product features that aren't taught in the Academy courses but exist in the docs and are commonly asked about by Ampliteers. Covers AI Evals, Release Pipeline, Topline Alerts, Web Analytics autocapture, Local Metrics, Custom DAU, and Metric Dimensions.

## Learning Objectives

### LO1. Explain Statsig AI Evals and when to use them.

**Prompt:** *What are AI Evals in Statsig, what's the offline vs. online split, and when would I use them?*

**Canonical answer:**

**AI Evals** is Statsig's first-class surface for evaluating AI/LLM systems. It has two flavors:

**Offline evals** — Run a curated test set (a "golden dataset" of prompts) through your AI system and score the outputs against criteria you define (e.g., faithfulness, format compliance, refusal correctness). Outputs a per-criterion score and can compare two model versions or two prompt templates head-to-head.

**Online evals** — Score live production AI responses. Statsig samples real user interactions, runs them through grader prompts (or human review), and produces a continuous quality signal you can chart alongside product metrics.

**When to reach for each:**
- **Offline:** before shipping — pre-flight check that a new prompt or model doesn't regress on known cases.
- **Online:** after shipping — catch quality drift, surface failure modes you didn't anticipate, monitor real-world performance.

**How it slots into the rest of Statsig:**
- An AI feature can be feature-gated like any other capability.
- An AI model swap can be an A/B test where the metric is "online eval quality score" plus downstream product metrics (conversion, retention).
- An AI-Evals score is a metric like any other — feeds into Pulse, dashboards, alerts.

**No direct Amplitude equivalent.** This is a Statsig-only surface; Ampliteers will need to learn it fresh.

**Where to go for depth:** `https://docs.statsig.com/ai-evals/overview`, `https://docs.statsig.com/ai-evals/offline-evals`, `https://docs.statsig.com/ai-evals/online-evals`.

---

### LO2. Explain Statsig Release Pipeline.

**Prompt:** *What is Release Pipeline, and how does it differ from just using feature gates directly?*

**Canonical answer:**

**Release Pipeline** is a structured rollout flow that promotes a change through pre-defined stages — typically `dev → staging → production` or `internal → 1% → 25% → 100%` — with explicit actions (promote, halt, abort) and triggers (manual click, time-based, metric-based).

**Why it exists:**
- Feature gates by themselves let you set "this is at 25%." A pipeline says "this should go 5% Monday → 25% Wednesday → 100% Friday, automatically, with a halt if the error rate exceeds X."
- Codifies a release process that teams often run informally (Slack messages, manual edits, no audit trail).

**Components:**
- **Stages** — the named steps of the rollout (dev, staging, prod, etc.).
- **Actions** — what happens at each stage (set gate to N%, send a notification, run a check).
- **Triggers** — what advances or halts the pipeline (time, manual approval, metric threshold).
- **Audit trail** — full history of who promoted what when.

**Relationship to feature gates:** the pipeline doesn't replace gates — it orchestrates them. Underneath, the gate's pass-percentage is what changes at each stage.

**When it's worth setting up:**
- Frequent, repeatable rollout patterns (every release follows the same dev → staging → prod path).
- Compliance / change-management requirements (need an audit trail of promotions).
- Multi-team coordination (PM owns the gate, SRE owns the halt criteria).

**No direct Amplitude equivalent.** Amplitude Experiment has scheduled rollouts but not a multi-stage pipeline-as-an-object.

**Where to go for depth:** `https://docs.statsig.com/release-pipeline/overview`, `https://docs.statsig.com/release-pipeline/create-and-manage`.

---

### LO3. Use Topline Alerts to catch metric regressions outside of experiments.

**Prompt:** *What are Topline Alerts, and when do they fire?*

**Canonical answer:**

**Topline Alerts** is anomaly detection on a metric. You designate a metric as "topline" and set sensitivity thresholds; Statsig watches the metric and pings you when it deviates from expected.

**How "expected" is computed:**
- Statsig builds a baseline from historical values of the metric (week-over-week, day-over-day depending on the metric's seasonality).
- Confidence bands around the baseline are computed.
- An alert fires when the current value falls outside those bands by more than the configured sensitivity.

**Where alerts go:**
- In-app notification.
- Slack / email / webhook (integrations).
- Visible in the metric's detail page with the anomaly window highlighted.

**Why this matters separate from experiment scorecards:**
- Experiment scorecards tell you "this change moved this metric by X%."
- Topline alerts tell you "something in the world (could be a bug, a third-party outage, a marketing campaign, a competitor) moved this metric."
- Alerts catch regressions that have nothing to do with an active experiment — the kind that would otherwise sit silently for days.

**Common pitfalls:**
- **Alert fatigue:** if sensitivity is too tight, you get an alert every Monday morning when traffic shifts. Tune to your metric's natural variability.
- **Seasonality misses:** a metric with strong weekly seasonality needs at least 3-4 weeks of history to baseline correctly.

**Amplitude counterpart:** Amplitude has Anomaly Detection on chart series; similar idea, different surfacing. Statsig's coupling with experiments means an alert can be cross-referenced against any active test that overlapped the anomaly window.

**Where to go for depth:** `https://docs.statsig.com/product-analytics/topline-alerts`, `https://docs.statsig.com/product-analytics/alerts-overview`.

---

### LO4. Use Web Analytics autocapture.

**Prompt:** *What is Statsig Web Analytics, and when does autocapture beat manual instrumentation?*

**Canonical answer:**

**Web Analytics** is Statsig's lightweight web surface that captures page views, clicks, form submits, and scroll depth automatically without you writing event-tracking code. Drop in the script tag; events start flowing.

**When autocapture wins:**
- **First-event speed.** You can start seeing funnels, retention, and click maps within hours of adding the tag.
- **Coverage of forgotten events.** Manual instrumentation always misses something; autocapture catches click events on any button.
- **Low-engineering teams.** Sites where there isn't an engineer to add tracking calls for every button.

**When manual instrumentation still wins:**
- **Custom business events** — "user upgraded plan," "lead qualified," "order placed with discount X." Autocapture can't infer business semantics.
- **High-fidelity analytics shops.** If you've already built a careful event taxonomy with naming and properties, autocapture's "every-click-is-an-event" noise is a downgrade.
- **Compliance / governance.** Autocapture pulls more data than you may want under strict privacy regimes.

**Practical pattern:** use both. Autocapture for click maps and page-flow insights; manual events for the business-critical conversion points (signup, upgrade, purchase). Most teams converge on this hybrid.

**Amplitude counterpart:** Amplitude Analytics has autocapture too. The capability set is comparable; Statsig's is newer (and reportedly less battle-tested on edge cases), Amplitude's is more mature. Coverage of attributes is similar.

**Where to go for depth:** `https://docs.statsig.com/webanalytics/overview`, `https://docs.statsig.com/webanalytics/autocapture`.

---

### LO5. Use Local Metrics for per-experiment ad-hoc analysis.

**Prompt:** *What are Local Metrics, and when would I use them instead of a metric in the catalog?*

**Canonical answer:**

**Local Metrics** are metrics defined inside a single experiment that aren't promoted to the global Metric Catalog. They exist only within that experiment.

**Why this matters:**
- An experiment often has a question that's narrow enough not to deserve a global metric (e.g., "what's the rate at which users who entered this flow returned within 5 minutes?"). Adding it to the catalog clutters every other experiment with a metric that's irrelevant outside this context.
- Local metrics let you ask the narrow question without polluting the catalog.

**How to use them:**
- Create the metric definition (event filter, aggregation, optional unit) in the experiment's configuration.
- It shows up on the scorecard alongside primary/secondary/guardrail metrics.
- When the experiment concludes, the metric stays with the experiment record but isn't reusable elsewhere.

**When to promote a Local Metric to the catalog:**
- If you find yourself defining the same local metric in 3+ experiments, promote it. That's a sign it's a real metric.
- If a stakeholder is asking "show me this number from last month's experiment again" weeks later — promote it so the definition is stable.

**Amplitude counterpart:** Amplitude doesn't distinguish "local" from "global" metrics in this way. Analysts either build the chart ad-hoc and don't save it (the "local" pattern, but ungoverned) or save it to the central library (the "global" pattern). Statsig's split makes the distinction explicit.

**Where to go for depth:** `https://docs.statsig.com/metrics/` general docs; search for "local metric."

---

### LO6. Configure Metric Dimensions for slice-able metrics.

**Prompt:** *What's a Metric Dimension, and how is it different from just segmenting after the fact?*

**Canonical answer:**

A **Metric Dimension** is a property baked into a metric's definition that lets it be sliced by that property without re-defining the metric. Define `purchase_revenue` with dimensions `country` and `payment_method`; now any chart on `purchase_revenue` can be split by either dimension with one click.

**Why this matters:**
- **Performance.** Pre-defined dimensions get pre-aggregated. Slicing is fast.
- **Consistency.** Everyone slicing by `country` uses the same definition of `country` — no one is using `country_code` vs `country_name` vs `geo_country`.
- **Discoverability.** When you open the metric, the available dimensions are visible. You don't have to guess what's slice-able.

**vs. post-hoc segmentation:**
- Post-hoc segmentation is open-ended — you can slice by any event property the platform has.
- Metric Dimensions are *curated* — the metric author chose what's worth slicing by.
- Both are valuable. Dimensions are for the "you'll always want this slice" cases; ad-hoc segmentation is for exploration.

**Common dimensions worth defining:**
- `country` / `region` (geographic)
- `plan_tier` / `subscription_status` (business)
- `platform` / `device_type` (technical)
- `acquisition_source` / `campaign` (marketing)

**Amplitude counterpart:** Amplitude's "Custom Metric Properties" and segmentation surfaces overlap with this. The architecture is different (Amplitude is more ad-hoc-segmentation-first); the analyst outcome is similar.

**Where to go for depth:** `https://docs.statsig.com/metrics/` and search for "dimension."

---

### LO7. Define a Custom DAU metric.

**Prompt:** *What's a Custom DAU metric, and when is it different from out-of-the-box DAU?*

**Canonical answer:**

**Custom DAU** lets you define what counts as "active" for your product, rather than relying on the default (any-event DAU).

**Default DAU:** a user who fired any event in the last 24 hours.

**Custom DAU:** a user who performed a specific qualifying action in the last 24 hours. Examples:
- **Editor product:** "opened the editor" — not just "logged in."
- **Music app:** "played a song for >30 seconds" — not just "opened the app."
- **B2B SaaS:** "ran a query" or "created a dashboard" — not just "loaded the homepage."

**Why this matters:**
- Default DAU includes drive-by traffic, accidental opens, bot-like sessions.
- A custom DAU tied to "meaningful usage" is a more honest health metric.
- Custom DAU often diverges 20-40% from default DAU. That gap is the noise in your default metric.

**How to define it:**
- Pick the qualifying event(s).
- Optionally add a property filter (e.g., "duration > 30 seconds").
- Optionally add a recurrence requirement (e.g., "fired at least 3 times in the day").
- Save it as a metric in the catalog.

**Companion metrics:**
- **Custom WAU** — weekly active using the same definition.
- **Custom MAU** — monthly active using the same definition.
- **Stickiness** — DAU / MAU. With custom definitions this becomes a real product-health signal.

**Amplitude counterpart:** Amplitude lets you define custom active-user metrics via event-property filters and saved cohorts. Same outcome, different config flow.

**Where to go for depth:** `https://docs.statsig.com/metrics/` and search for "custom DAU" or "active user."

## Why this topic exists

The Bucket A gap audit at `data/synthesized/coverage-audit.md` flagged these seven Statsig surfaces as having zero coverage in our course/caption/topic content despite each having meaningful depth in the docs. This topic file lets the skill answer "what is AI Evals" or "explain Topline Alerts" without inventing or hallucinating.
