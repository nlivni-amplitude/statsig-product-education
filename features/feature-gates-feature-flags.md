---
feature: Feature Gates / Feature Flags
slug: feature-gates-feature-flags
statsig_concept: Feature Gates
amplitude_counterpart: "Amplitude Experiment flags"
match_quality: partial
---

# Feature Gates / Feature Flags

**What it is:** Both target users by attributes with pass-percentages

## Amplitude counterpart

- **Concept:** Amplitude Experiment flags
- **Match quality:** partial
- **Key differences:**
  - Statsig auto-promotes gates to A/B tests; Amplitude separates flag from experiment more cleanly
  - Different SDK API shapes
- **Amplitude docs:**
  - https://amplitude.com/docs/feature-experiment/stale-flag-management
  - https://amplitude.com/docs/feature-experiment/workflow/feature-flag-rollouts
  - https://amplitude.com/docs/feature-experiment/under-the-hood/flag-dependencies

## Primary Statsig docs

- https://docs.statsig.com/feature-flags/test-gate
- https://docs.statsig.com/feature-flags/permanent-and-stale-gates
- https://docs.statsig.com/feature-flags/create

## Related doc pages

- https://docs.statsig.com/guides/featureflags-or-experiments
- https://docs.statsig.com/guides/first-feature
- https://docs.statsig.com/access-management/org-admin/gates_policy
- https://docs.statsig.com/feature-flags/feature-flags-lifecycle
- https://docs.statsig.com/statsig-warehouse-native/features/other-useful-features

## Amplitude Academy courses

- [Statsig Product Onboarding](https://academy.amplitude.com/statsig-product-onboarding)
- [Statsig 101](https://academy.amplitude.com/statsig-101)

## Internal videos (Wistia)

- [Feature Gates - Introduction](https://amplitude.wistia.com/medias/u11falwfip)
- [Turning gates into A_B tests](https://amplitude.wistia.com/medias/xr41a489f7)
- [Building your first feature flag](https://amplitude.wistia.com/medias/o1setqayr7)
- [Test - analyze feature gates and experiments](https://amplitude.wistia.com/medias/y01v52rlc7)

## YouTube (Statsig channel)

- [Introducing Feature Gate Safeguards | Feature Management](https://www.youtube.com/watch?v=mBwF5_gFOI4)
- [Statsig x Vercel Integration: Get set up with Feature Flags](https://www.youtube.com/watch?v=xGlDtB3mr9s)
- [Deep Dive 101: Feature Flag and Experiment Testing and Diagnostics](https://www.youtube.com/watch?v=9XR-gVI2g1I)
- [Feature Flags Deep Dive](https://www.youtube.com/watch?v=5U_qICP4Y1Y)
- [See the whole picture: Add product analytics to feature gates & experiments](https://www.youtube.com/watch?v=WrPCtDCvr98)

## Where this lives in the teaching corpus

Topic file: `03-feature-flags.md`

- LO4. Gate client-side vs. server-side.
- LO5. Set up a scheduled rollout for risk.
- LO6. Explain how a gate promotes to an A/B test.
- LO7. Distinguish a Feature Flag from a Dynamic Config.
- LO8. Contrast with Amplitude Experiment flags.
