---
topic: dynamic-configs
source_modules:
  - Statsig 2 / Module 3 — Feature Management
amplitude_counterpart: "Payloads in Amplitude Experiment"
---

# Dynamic Configs

Server-defined JSON values you can change without redeploying. Sit alongside Feature Flags as Statsig's "parameterize behavior" primitive.

## Learning Objectives

### LO1. Recognize when a hard-coded value should become a Dynamic Config.

**Prompt:** *Look at your codebase. What's the test for deciding when a hard-coded value should be lifted out into a Dynamic Config? What's the test for when it shouldn't?*

**Canonical answer:**
**Lift it to a config when:**
- The value might change without a code change being warranted (button copy, threshold, retry count, weights)
- Different segments need different values (premium users get a higher rate limit; free users get a lower one)
- You want to A/B test the value itself (try copy A vs. copy B without two code paths)

**Leave it hard-coded when:**
- The value is structurally tied to the code (e.g., it's part of an algorithm's correctness contract)
- Changing it would require code changes regardless (you'd still need to redeploy to use the new value)
- The cognitive cost of "go look up this value in the console" exceeds the benefit

The risk of over-using configs is **config sprawl** — too many tunable knobs nobody remembers exist.

---

### LO2. Use Flags and Configs together.

**Prompt:** *You're launching a new recommendations widget. You want to (a) gradually roll it out and (b) experiment with two different sort algorithms once it's live. How do you use a Flag and a Config together?*

**Canonical answer:**
- **Flag** controls *whether* the widget appears. Roll it out from 1% to 100% as you de-risk.
- **Config** holds the sort algorithm parameters (e.g., `{"algorithm": "recency", "decay_factor": 0.8}`). For users who pass the flag, the config delivers the parameters.
- To experiment with sort algorithms, you'd either:
  - Use Statsig's experiment object to vary the config across two arms, OR
  - Have the flag's pass-percentage rule serve two different config variants

The clean separation: Flag = visibility, Config = behavior. Don't conflate them into one bigger flag.

---

### LO3. Contrast Statsig Dynamic Configs with Amplitude Experiment payloads.

**Prompt:** *Both Statsig (Dynamic Configs) and Amplitude Experiment (payloads) let you parameterize behavior server-side. How are they different in practice?*

**Canonical answer:**
- **Statsig Dynamic Configs** — first-class object in the UI. You create it, manage it, target it independent of any experiment. The SDK has a dedicated `getConfig()` call. You can query a config without an associated experiment running.
- **Amplitude Experiment payloads** — a payload is an attribute of an experiment variant. The mental model is "experiment-first," and the payload is what you deliver alongside the variant assignment.

**For a migrator:** if a customer is heavy on Dynamic Configs as a configuration-management tool (without active experiments), they'll need to model that differently in Amplitude — either as experiments with a single variant, or by managing config outside of Experiment entirely.
