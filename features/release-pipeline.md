---
feature: Release Pipeline
slug: release-pipeline
statsig_concept: Release Pipeline
amplitude_counterpart: "(No direct Amplitude equivalent)"
match_quality: none
audit_flagged_shallow: true
---

# Release Pipeline

**What it is:** Multi-environment rollout flow: dev → staging → production with explicit promote/abort actions and triggers. Codifies a release process as a pipeline rather than a series of manual gate edits.

## Amplitude counterpart

- **Concept:** (No direct Amplitude equivalent)
- **Match quality:** none
- **Key differences:**
  - Pipeline as a first-class object with actions, triggers, and audit trail
  - Layers on top of standard gate management — same gates, structured promotion flow

## Primary Statsig docs

- https://docs.statsig.com/release-pipeline/overview
- https://docs.statsig.com/release-pipeline/create-and-manage
- https://docs.statsig.com/release-pipeline/actions

## Related doc pages

- https://docs.statsig.com/statsig-warehouse-native/analysis-tools/pipeline-overview

## YouTube (Statsig channel)

- [Modern Feature Flags: From stress-free releases to automated experimentation](https://www.youtube.com/watch?v=eL-j6SWBEog)

> ⚠️  Audit-flagged as shallow in the Statsig Academy corpus.
> Prefer the docs above when answering depth questions.
