---
topic: build-ship-measure-learn
source_modules:
  - Statsig 2 / Module 6 — Powering the Product Lifecycle
amplitude_counterpart: "Same loop applies; Amplitude pieces are split across Analytics + Experiment + Session Replay"
---

# Build → Ship → Measure → Learn

The product-development loop that ties Statsig's four products together. Less about features, more about *how* you use them in sequence to learn faster.

## Learning Objectives

### LO1. Trace a real product change through all four stages.

**Prompt:** *Pick a real product change — adding a "save for later" button to a checkout flow. Walk it through Build → Ship → Measure → Learn, naming which Statsig product fires at each step.*

**Canonical answer:**
- **Build** — engineering writes the "save for later" code. The new behavior is wrapped behind a **Feature Gate** so it's not exposed by default.
- **Ship** — the Feature Gate rolls out gradually (1% → 5% → 25%). At any percentage above 0%, the gate is also an A/B test (gate auto-promotes). Define the **primary metric** (checkout completion rate), **secondary metrics** (save-for-later usage), and **guardrails** (cart abandonment, revenue) up front.
- **Measure** — the **Experiment scorecard** compares users-with-feature vs. users-without. After enough exposures and the right window, it shows lift/CI/p-value on each metric.
- **Learn** — if the experiment wins → ramp to 100% and remove the gate. If it loses → roll back. If it's null → use **Product Analytics** to investigate ("did users find the button?" via funnels) and **Session Replay** to see *how* users interacted with it. The learning informs the next iteration.

Every stage produces signal for the next. That's the loop.

---

### LO2. Recognize when NOT to experiment.

**Prompt:** *List three situations where running a Statsig experiment is the wrong move, and explain what to do instead.*

**Canonical answer:**

1. **Irreversible changes** (e.g., migrating data, deleting a feature with users depending on it). Once shipped, you can't roll back. Use **shadow traffic**, **dogfooding**, or **staged migrations** instead.

2. **Low-traffic surfaces** where the experiment won't reach statistical power in any reasonable timeframe. Running anyway just slows you down with inconclusive results. Use **qualitative methods** (user interviews, dogfooding, expert review) or **roll out to 100% and measure pre/post** for major changes.

3. **Strategic decisions where the metric isn't the right oracle.** "Should we enter the European market?" isn't an A/B test — the metric an experiment would optimize doesn't capture the long-term strategic value. Use **judgment + scenario planning** instead.

4. (Bonus) **Tiny changes where the cost of the experiment exceeds the value of being right.** Renaming a button from "Buy" to "Purchase"? Just ship it; instrument it; check the funnel; don't spin up a formal experiment.

---

### LO3. Articulate why experimentation velocity drives learning.

**Prompt:** *Jeff Bezos: "If you double the number of experiments you do per year, you'll double your inventiveness." Why is this not just a motivational quote? What's the actual mechanism?*

**Canonical answer:** The mechanism is **iteration speed**.

Every experiment is a hypothesis being tested. With low experiment volume, each hypothesis is precious — you bias toward "safe" experiments you're already pretty sure will win, and you wait long periods between iterations. The variance you can explore is small.

With high experiment volume:
- You can run **bolder** experiments (counterintuitive ideas, big swings) because the cost of any single one being wrong is low.
- You **iterate** faster — winner becomes next experiment's baseline immediately.
- **Counterintuitive results** (where your intuition was wrong) compound into deeper product understanding.
- **Null results** stop being expensive — you learn that an idea doesn't work and move on, rather than agonizing.

The bottleneck on most teams isn't ideas. It's the friction of running an experiment. Lower that friction → more experiments → more learnings → better products. Self-serve experiments and good infrastructure are what unlock this.

---

### LO4. Recognize when the loop is broken.

**Prompt:** *A team has Statsig set up. They run experiments. But their product isn't getting better. What signals tell you the loop is broken, and at which stage?*

**Canonical answer:** Diagnose by stage:

- **Build broken:** the team has more features in flight than experiments. Engineering ships without gates. Symptom: no rollback path when something breaks.
- **Ship broken:** experiments launch but exposures don't fire correctly (SRM warnings, missing identifier metrics, broken instrumentation). Symptom: scorecards show wild swings or zero effect even on visible changes.
- **Measure broken:** experiments run but everyone debates the results post-hoc ("the primary metric wasn't the right one"). Symptom: post-experiment metric switching, cherry-picked secondary findings.
- **Learn broken:** results exist but don't influence the next decision. The team ran a losing experiment and shipped the variant anyway because the PM "felt" it was right. Symptom: experiment results have no decision-rights weight.

**The most common breakage:** Learn. Teams set up the infrastructure (Build, Ship, Measure) and never close the loop because the cultural step of "experiments dictate decisions" isn't in place. Symptom: lots of experiments, no behavior change.

---

### LO5. Contrast running the loop in Statsig vs. Amplitude.

**Prompt:** *How does running this Build → Ship → Measure → Learn loop differ between Statsig and Amplitude?*

**Canonical answer:**

**Statsig:** the loop is tightly coupled by design. One SDK, one console, one place to define metrics. Less wiring; less cognitive overhead crossing product surfaces. Trade-off: less flexibility — you do it Statsig's way.

**Amplitude:** the loop spans Amplitude Analytics, Amplitude Experiment, and Amplitude Session Replay. More SDKs, more configuration touchpoints. Trade-off: more modular — use what you need, integrate with existing analytics infra more flexibly, but more wiring upfront.

**For an Ampliteer:** when a customer says "we want to run this loop," figure out where their current friction is.
- New customer with no analytics infra → Statsig's bundled approach gets them shipping faster.
- Customer already on Amplitude Analytics → adding Amplitude Experiment + Session Replay reuses their existing instrumentation; no need to also add Statsig.
- Customer with strong existing analytics but missing experimentation → either Statsig (bundled experimentation+replay+analytics) or Amplitude Experiment alone (just the missing piece) are valid.
