---
feature: Event Ingestion
slug: event-ingestion
statsig_concept: Event ingestion (SDK / CDP / warehouse)
amplitude_counterpart: "Event ingestion (SDK / Segment / warehouse)"
match_quality: close
---

# Event Ingestion

**What it is:** Both support direct SDK, CDP relay (Segment/RudderStack), and warehouse import

## Amplitude counterpart

- **Concept:** Event ingestion (SDK / Segment / warehouse)
- **Match quality:** close
- **Key differences:**
  - Statsig favors Metric Catalog as central registry; Amplitude favors event taxonomy
- **Amplitude docs:**
  - https://amplitude.com/docs/partners/create-an-event-ingestion-integration
  - https://amplitude.com/docs/feature-experiment/under-the-hood/event-tracking
  - https://amplitude.com/docs/data/custom-events

## Primary Statsig docs

- https://docs.statsig.com/api-reference/ingestions/get-ingestion-event-count
- https://docs.statsig.com/api-reference/ingestions/get-ingestion-event-delta-ledger
- https://docs.statsig.com/metrics/ingest

## Related doc pages

- https://docs.statsig.com/guides/logging-events
- https://docs.statsig.com/infra-analytics/events-mode-logs-explorer
- https://docs.statsig.com/metrics/deprecate-event-dau
- https://docs.statsig.com/metrics/raw-event-metrics
- https://docs.statsig.com/metrics/raw-events
- https://docs.statsig.com/statsig-warehouse-native/configuration/qualifying-events
- https://docs.statsig.com/statsig-warehouse-native/features/mex-on-warehouse-native

## Amplitude Academy courses

- [Setting Up Statsig](https://academy.amplitude.com/setting-up-statsig)

## Internal videos (Wistia)

- [SDK logging events and exposures](https://amplitude.wistia.com/medias/07xfhbsn1i)
- [Connect events](https://amplitude.wistia.com/medias/o4yrx101ir)
- [Connect your warehouse](https://amplitude.wistia.com/medias/x4ounfqp50)

## YouTube (Statsig channel)

- [Deep Dive 101: SDK logging events and exposures](https://www.youtube.com/watch?v=rkjq5eCOY9w)
- [Unlocking Agility with Warehouse Native Experimentation](https://www.youtube.com/watch?v=wo_Sbr-ZRC4)
- [Statsig Warehouse Native Product Walkthrough](https://www.youtube.com/watch?v=clWLTXgving)
- [Statsig Warehouse Native](https://www.youtube.com/watch?v=tjK_gUr6Luc)
- [A Day in London With Our Event Marketing Manager](https://www.youtube.com/watch?v=VXfpzUXevcE)

## Where this lives in the teaching corpus

Topic file: `08-data-and-metrics.md`

- LO1. Choose the right ingestion path.
- LO2. Build a metric in the Metric Catalog.
- LO3. Recognize when CUPED is worth turning on.
- LO4. Connect a warehouse for warehouse-native experiments.
- LO5. Contrast Statsig's Metric Catalog with Amplitude's event-stream model.
