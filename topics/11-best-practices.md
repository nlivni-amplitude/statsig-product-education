---
topic: best-practices
source_modules:
  - Statsig 1 / Module 5 — Product Best Practices (partial — product hygiene only)
amplitude_counterpart: "Same hygiene principles apply across both products"
---

# Best Practices — Product Hygiene

Cross-cutting product hygiene for using Statsig's primitives well. Scoped to product knowledge an internal Ampliteer needs; experimentation program management and team-culture practices are taught separately and out of scope here.

## Learning Objectives

### LO1. Decide if a flag should be short-lived or long-lived.

**Prompt:** *When should a Feature Gate be a temporary if/else block vs. a long-lived configuration parameter? What makes the difference?*

**Canonical answer:**

**Short-lived (if/else gate):** the feature will eventually be 100% on or 100% off. The gate exists for rollout safety. After ramp-up, **delete the gate and the dead branch**.

*Examples:*
- New checkout UI launching to all users — gate it for the rollout, kill it once at 100%.
- A bug fix you want to ship cautiously — gate, ramp, delete.

**Long-lived (config parameter):** different users need different values, permanently. The gate isn't temporary; it's the mechanism for ongoing personalization.

*Examples:*
- Free-tier vs. paid-tier feature access — there will always be users on each tier.
- Region-specific behavior (compliance differences for EU vs. US).
- Per-customer feature toggles for enterprise contracts.

**The hygiene rule:** every short-lived gate must have an owner and a "delete by" date. Otherwise they accumulate and become **flag debt** — codebases fill with stale `if (feature_X_enabled)` branches nobody remembers, can't safely remove, and that add complexity to every change.

---

### LO2. Decide client-side vs. server-side gating.

**Prompt:** *Statsig recommends "localize the gating decision inside the service whose behavior is being changed." What does that mean in practice? When is client-side gating right vs. server-side?*

**Canonical answer:**
- **Client-side** — gate where the user *sees* the change and where the context lives in the browser/app. Examples: a new landing page layout, an onboarding tooltip, a UI experiment. The browser has the context; the browser makes the decision.
- **Server-side** — gate where the *backend behavior* changes and the context lives on the server. Examples: a new ranking algorithm, a new API endpoint, a different cache strategy. The server has the context (user tier, request payload, system load); the server makes the decision.

**The "wrong side" failure modes:**
- **Gating server behavior on the client** — leaks implementation. Client knows the server is doing X. Brittle (client can lie about its variant); insecure (client can change the variant).
- **Gating client UX on the server** — round-trip latency hit for a decision the client could have made locally. Also: the client UX often depends on context the server doesn't have (window size, scroll position).

**Test:** ask "where does the context for this decision live?" — that's where the gate lives.

---

### LO3. Recognize feature-gate anti-patterns.

**Prompt:** *List three common anti-patterns when teams use Feature Gates poorly, and explain the cost of each.*

**Canonical answer:**

1. **One gate controls multiple features.**
   *Example:* a single `new_redesign` gate controls a header change, a sidebar change, AND a checkout change.
   *Cost:* troubleshooting is confusing — when a metric moves, you can't isolate which sub-feature drove it. Rollback is all-or-nothing. **Fix:** master gate + child gates, or separate gates per feature.

2. **Gates that never get cleaned up.**
   *Example:* a 2-year-old `experimental_pricing_v2` gate still in the codebase, ramped to 100% for 18 months.
   *Cost:* dead branches multiply, every code change has to consider the dead path, refactors get harder. Eventually nobody removes it out of fear. **Fix:** mandatory delete-by-date on every short-lived gate; quarterly cleanup.

3. **Gates as configuration sprawl.**
   *Example:* every minor setting is a gate. Hundreds of gates, no governance.
   *Cost:* the gate list becomes unmanageable; production has gates ramped to weird percentages because someone was testing something and forgot. **Fix:** consolidate to Dynamic Configs for parameterization; reserve Gates for actual rollout/experimentation.
