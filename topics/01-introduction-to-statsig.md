---
topic: introduction-to-statsig
source_modules:
  - Statsig 2 / Module 1 — Introduction to Statsig
amplitude_counterpart: "Spans Amplitude Analytics + Amplitude Experiment + Amplitude Session Replay"
---

# Introduction to Statsig

Orientation to Statsig's four product lines and the loop that ties them together. Foundation for every other topic.

## Learning Objectives

### LO1. Identify the four product lines and the specific problem each solves.

**Prompt:** *Name Statsig's four product lines. For each, describe the one problem it's built to solve in one sentence.*

**Canonical answer:**
- **Feature Flags / Feature Gates** — control *whether* a feature is exposed to a given user; solves the "ship without redeploying / kill switch / gradual rollout" problem.
- **Experimentation** — measure the *causal impact* of a change; solves "did this change actually move the metric?"
- **Product Analytics** — describe *what* users are doing; solves "we have behavior data, what's the pattern?"
- **Session Replay** — show *why* users behaved a certain way; solves "the funnel says they dropped at step 3 but I don't know what they did."

---

### LO2. Explain why Statsig packages these four together rather than as separate tools.

**Prompt:** *Why does Statsig bundle these four products? What's the loop that makes the integration matter?*

**Canonical answer:** The **Build → Ship → Measure → Learn** loop. Each product feeds the next:
- **Ship** — Feature Flags wrap the new code so you can release safely
- **Measure** — Experiments compare variants and prove (or disprove) impact
- **Learn (what)** — Product Analytics shows the resulting behavior across the user base
- **Learn (why)** — Session Replay reveals why behavior is what it is

The integration matters because every shipped change becomes a measurable change, and every measured change feeds the next hypothesis. Four separate tools can't close that loop without manual stitching.

---

### LO3. Map each Statsig product line to its Amplitude counterpart.

**Prompt:** *Map each Statsig product to its closest Amplitude equivalent. Where does the mapping break down?*

**Canonical answer:**
| Statsig | Amplitude counterpart | Mapping quality |
|---|---|---|
| Feature Flags / Feature Gates | Amplitude Experiment (flag side) | Close — both target by user attrs |
| Experimentation | Amplitude Experiment | Close — both run A/B, both have scorecards, both support warehouse-native |
| Product Analytics | Amplitude Analytics | Close — funnels, retention, dashboards |
| Session Replay | Amplitude Session Replay | Close — record-and-replay |

**Where it breaks down:** Amplitude historically separates Analytics from Experiment as distinct products with their own SDKs. Statsig bundles flag + experiment + analytics into one product surface and one SDK call. The "loop" is more tightly coupled in Statsig's UX; in Amplitude it's more modular, which can be a plus (use only what you need) or a minus (more wiring to make the loop work).

---

### LO4. Recognize this is an Amplitude product, not a competitor.

**Prompt:** *Statsig is now an Amplitude product. What does that change about how an Ampliteer should talk about it internally?*

**Canonical answer:** Statsig and Amplitude (Analytics, Experiment) are sibling products in the same portfolio. Frame comparisons like you would Amplitude Analytics vs. Amplitude Experiment — different surfaces, different opinions, but one company. Avoid "competitive" or "objection" framing. When something is genuinely stronger in Statsig (e.g., warehouse-native experimentation, multi-arm bandits), say so — it's still an Amplitude product getting credit.
