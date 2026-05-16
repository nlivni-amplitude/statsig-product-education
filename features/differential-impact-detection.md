---
feature: Differential Impact Detection
slug: differential-impact-detection
statsig_concept: Differential Impact Detection (DID)
amplitude_counterpart: "Heterogeneous treatment effects (manual)"
match_quality: partial
audit_flagged_shallow: true
---

# Differential Impact Detection

**What it is:** Auto-detect segments where the treatment effect differs significantly from the global effect (e.g. 'this works for new users but hurts power users'). Heterogeneous treatment effect detection.

## Amplitude counterpart

- **Concept:** Heterogeneous treatment effects (manual)
- **Match quality:** partial
- **Key differences:**
  - Statsig auto-surfaces segments with significantly different effects
  - Amplitude requires manual segmentation to find heterogeneous effects

## Primary Statsig docs

- https://docs.statsig.com/experiments/analyzing-results/heterogeneous-effects

## Related doc pages

- https://docs.statsig.com/experiments/exploring-results/aggregated-impact
- https://docs.statsig.com/experiments/exploring-results/differential-impact-detection
- https://docs.statsig.com/experiments/exploring-results/interaction-detection
- https://docs.statsig.com/experiments/statistical-methods/topline-impact
- https://docs.statsig.com/statsig-warehouse-native/features/differential-impact
- https://docs.statsig.com/statsig-warehouse-native/features/exploring-results/aggregated-impact
- https://docs.statsig.com/statsig-warehouse-native/features/statistics/topline-impact

## YouTube (Statsig channel)

- [Dude, Where's My Impact? A guide to reporting A/B tests](https://www.youtube.com/watch?v=FDdw86XWzVk)

> ⚠️  Audit-flagged as shallow in the Statsig Academy corpus.
> Prefer the docs above when answering depth questions.
