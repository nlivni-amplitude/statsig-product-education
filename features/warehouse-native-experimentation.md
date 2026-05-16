---
feature: Warehouse-Native Experimentation
slug: warehouse-native-experimentation
statsig_concept: Statsig Warehouse Native
amplitude_counterpart: "Amplitude Experiment (warehouse mode)"
match_quality: close
---

# Warehouse-Native Experimentation

**What it is:** Both query the customer's data warehouse directly instead of streaming events

## Amplitude counterpart

- **Concept:** Amplitude Experiment (warehouse mode)
- **Match quality:** close
- **Key differences:**
  - Different schema configuration patterns; same underlying statistical compute
- **Amplitude docs:**
  - https://amplitude.com/docs/web-experiment
  - https://amplitude.com/docs/feature-experiment
  - https://amplitude.com/docs/web-experiment/proxy

## Primary Statsig docs

- https://docs.statsig.com/statsig-warehouse-native/guides/sql
- https://docs.statsig.com/statsig-warehouse-native/metrics/sum
- https://docs.statsig.com/statsig-warehouse-native/metrics/log

## Related doc pages

- https://docs.statsig.com/guides/statsig-id-resolver
- https://docs.statsig.com/statsig-warehouse-native/guides/experimentation-program
- https://docs.statsig.com/infrastructure/statsig_domains
- https://docs.statsig.com/infrastructure/statsig_ip_ranges
- https://docs.statsig.com/statsig-warehouse-native/features/mex-on-warehouse-native
- https://docs.statsig.com/statsig-warehouse-native/native-vs-cloud

## Amplitude Academy courses

- [Statsig Product Onboarding](https://academy.amplitude.com/statsig-product-onboarding)
- [Statsig 101](https://academy.amplitude.com/statsig-101)
- [Setting Up Statsig](https://academy.amplitude.com/setting-up-statsig)

## Internal videos (Wistia)

- [Welcome to Statsig 101](https://amplitude.wistia.com/medias/4o8x2ejyse)
- [Setting up Statsig's SDKs](https://amplitude.wistia.com/medias/g8s2ribmnb)
- [How to build an experimentation culture](https://amplitude.wistia.com/medias/drmf84xouy)
- [Install and initialize the Statsig client SDK](https://amplitude.wistia.com/medias/jakavyfdpn)
- [Install and initialize the Statsig server SDK](https://amplitude.wistia.com/medias/izms0f5f4l)
- [Connect your warehouse](https://amplitude.wistia.com/medias/x4ounfqp50)

## YouTube (Statsig channel)

- [Advanced methods for faster experimentation](https://www.youtube.com/watch?v=uxV0teHXBjA)
- [NextDoor x Statsig Customer Story](https://www.youtube.com/watch?v=TlAg-_LjEOc)
- [Brex x Statsig Customer Story](https://www.youtube.com/watch?v=EZcplcvRJxU)
- [Life360 x Statsig Customer Story](https://www.youtube.com/watch?v=-d0AHF_LGis)
- [Statsig MCP Server Overview](https://www.youtube.com/watch?v=EM1ykHNKHNc)

## Where this lives in the teaching corpus

Topic file: `05-experiments.md`

- LO2. Choose the right experiment unit.
- LO4. Validate the experiment before declaring it live.
- LO6. Reason about interaction effects.
- LO7. Use Holdouts and recognize meta-insights.
- LO9. Use multi-arm bandits when you want to optimize, not just learn.
- LO10. Contrast Statsig experiments with Amplitude Experiment.
