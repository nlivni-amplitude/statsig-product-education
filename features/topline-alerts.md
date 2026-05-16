---
feature: Topline Alerts
slug: topline-alerts
statsig_concept: Topline Alerts
amplitude_counterpart: "Anomaly Detection (Amplitude Analytics)"
match_quality: partial
audit_flagged_shallow: true
---

# Topline Alerts

**What it is:** Anomaly detection on top-line metrics. Statsig watches a metric and pings you when it deviates from expected. Useful for catching regressions outside of an active experiment.

## Amplitude counterpart

- **Concept:** Anomaly Detection (Amplitude Analytics)
- **Match quality:** partial
- **Key differences:**
  - Both alert on metric deviations from expected
  - Statsig's coupling to experiments means an alert can be cross-referenced against active tests
- **Amplitude docs:**
  - https://amplitude.com/docs/analytics/anomaly-detection

## Primary Statsig docs

- https://docs.statsig.com/product-analytics/topline-alerts
- https://docs.statsig.com/product-analytics/alerts-overview

## Related doc pages

- https://docs.statsig.com/experiments/statistical-methods/topline-impact
- https://docs.statsig.com/infra-analytics/topline-alerts-logs
- https://docs.statsig.com/metrics/rollout-alerts
- https://docs.statsig.com/statsig-warehouse-native/features/statistics/topline-impact

## YouTube (Statsig channel)

- [Introducing Topline Alerts | Analytics](https://www.youtube.com/watch?v=ikLXIdmZdjc)

> ⚠️  Audit-flagged as shallow in the Statsig Academy corpus.
> Prefer the docs above when answering depth questions.
