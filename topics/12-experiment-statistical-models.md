---
topic: experiment-statistical-models
source_modules:
  - General knowledge (the validated Statsig corpus glosses over this; both products' docs have dedicated pages)
amplitude_counterpart: "Amplitude Experiment supports both frequentist and Bayesian modes with similar trade-offs"
audit_note: "Corpus only names these concepts in passing. This topic file provides product-agnostic methodology so the skill can teach the general concept and point to docs for product-specific UI."
---

# Experiment Statistical Models — General Methodology

The Statsig Academy corpus names sequential testing, Bayesian options, CUPED, and power analysis in passing but doesn't teach the underlying concepts. This topic provides product-agnostic methodology knowledge so the skill can answer general questions like "what's the difference between frequentist and Bayesian?" without needing to invent.

**Scope:** the statistics. Not the UI clicks. For product-specific configuration (where the toggle lives, defaults, etc.), point to `docs.statsig.com/experiments/advanced-setup/bayesian` or `amplitude.com/docs/feature-experiment/experiment-theory/bayesian-statistics`.

## Learning Objectives

### LO1. Distinguish frequentist from Bayesian experimentation.

**Prompt:** *In one paragraph, what's the practical difference between a frequentist scorecard and a Bayesian scorecard?*

**Canonical answer:**
- **Frequentist** answers: *"If the true effect were zero, how unlikely is the data I observed?"* You get a p-value and a confidence interval. Decision rule: if p < 0.05, reject the null (the effect is "statistically significant"). Treats the parameter (true lift) as fixed and the data as random.
- **Bayesian** answers: *"Given the data, what's the probability the effect is positive (or above some threshold)?"* You get a posterior distribution. Decision rule: if P(effect > 0) > some threshold (e.g., 95%), call it. Treats the parameter as a probability distribution and updates it with data.

**Practical implications:**
- **Frequentist** is the default in most tools because it's well-understood and resists priors. Easier to defend in formal review.
- **Bayesian** answers a more intuitive question ("how likely is this to actually work") and updates naturally with new data. Can require a prior (an opinion about what effects are plausible before the experiment).
- **They usually agree** for clean experiments with enough data. They diverge when data is sparse or when priors are informative.
- **Tool support:** both Statsig and Amplitude Experiment support both modes; frequentist is typically the default.

---

### LO2. Understand fixed-horizon vs always-valid (sequential) inference.

**Prompt:** *What's the difference between a "fixed-horizon" experiment and one using "always-valid inference" (sequential testing)? Why does it matter?*

**Canonical answer:**
- **Fixed-horizon (classical) testing:** you commit upfront to a sample size (via a power analysis) and only check the result at the end. The math (p-values, confidence intervals) is only valid if you don't peek at the data and stop early when it looks good. If you do peek and stop early, false-positive rates inflate dramatically — easily 30-50%+ instead of 5%.
- **Always-valid inference (sequential testing):** the math is rebuilt so that you *can* peek and stop early without inflating false-positive rates. The trade-off: confidence intervals are wider for any given sample size (because the method has to "spend alpha" across all possible peeking moments).

**Why it matters:**
- Real teams almost always want to peek (monitor experiments daily, stop early when a clear winner emerges, kill a clear loser before it hurts users).
- Fixed-horizon math says "you can't do that." Always-valid math says "you can."
- The cost of always-valid: longer runs to reach the same confidence, OR you accept wider CIs at the same runtime.
- **Statsig's sequential testing** (offered as an option) is a form of always-valid inference. Amplitude Experiment similarly supports always-valid / sequential modes.

---

### LO3. Recognize peeking risk and optional-stopping bias.

**Prompt:** *Someone says: "We ran the experiment for 3 days, saw +8% on the primary metric with p=0.03, and shipped it." What's the problem (if any)?*

**Canonical answer:**
**The problem depends on the math the tool was running.** If they were using fixed-horizon statistics (the default in many tools), and they didn't pre-commit to a 3-day horizon via power analysis, then **the p=0.03 is not trustworthy.**

**Why:** with fixed-horizon math, the p-value's meaning is "if I check at the planned end of the experiment, this is how often I'd see this result under the null." If you check daily and stop the first time you see p<0.05, you've essentially run a hundred-comparison experiment and reported the best one. False-positive rate is far higher than 5%.

**The fix:**
- **Pre-register the duration** (run a power analysis up front; commit to running until N days or N exposures, only then check)
- **Or use always-valid / sequential testing** so peeking is legitimate
- **Or accept the cost:** know that "we shipped on early-peek p<0.05" decisions have higher false-positive rates and treat them as exploratory rather than confirmed

This is called the **optional stopping problem** in the literature.

---

### LO4. Explain power analysis and sample size determination.

**Prompt:** *A PM wants to run an experiment but doesn't know how long to run it. Walk through what a power analysis answers.*

**Canonical answer:** Power analysis is a pre-experiment calculation that answers: *"how big does my sample need to be to detect an effect of size X with confidence Y?"*

Inputs:
- **Baseline metric value** (current conversion rate, current revenue per user, etc.)
- **Minimum detectable effect (MDE)** — the smallest lift you'd care about acting on (e.g., +2% relative)
- **Alpha** (typically 0.05) — tolerance for false positives
- **Power** (typically 0.80) — probability of detecting the effect if it's real
- **Allocation** (typically 50/50)

Output: required sample size per arm. Divide by your daily traffic on the surface to get experiment duration.

**Why it matters:**
- Running too short = underpowered, you'll miss real effects (high false-negative rate)
- Running too long = wasted opportunity cost (you could have been testing the next thing)
- Most tools have a built-in power-analysis calculator (Statsig's is in the experiment setup UI)

**Common mistake:** treating the calculator output as a "minimum" and stopping the first time results look stat-sig. That's the peeking problem (LO3) — power analysis assumes fixed-horizon stopping.

---

### LO5. Understand CUPED and variance-reduction techniques.

**Prompt:** *In simple terms, what is CUPED doing, and when does it help?*

**Canonical answer:** **CUPED** (Controlled-experiment Using Pre-Experiment Data) reduces noise in experiment results by using each user's *pre-experiment behavior* as a control covariate.

**The intuition:**
- Imagine you're measuring "how much did revenue change?" for a population that includes a few whales (very high spenders) and a long tail of light users.
- Most of the variance you see in the experiment metric is just whale-randomness — not the experiment's effect.
- CUPED removes the predictable part: "this user typically spends $X/week, so we expected $X this week." Then the experiment effect is measured on the *residual* — what's left after subtracting the predictable baseline.

**When it helps:**
- High-variance metrics (revenue, time-spent, deep-funnel events)
- Users with stable baseline behavior (returning users with history)
- Long-running experiments where pre-period data exists

**When it doesn't:**
- Brand-new users (no pre-period data)
- Metrics with low variance to begin with (e.g., click-through rate on a small change)
- Highly seasonal metrics where the pre-period doesn't predict the experiment period

**Effect:** can reduce required sample size by 20-50% on suitable metrics. Both Statsig and Amplitude Experiment offer CUPED.

---

### LO6. Read a confidence interval correctly.

**Prompt:** *An experiment shows: lift +3.2%, 95% CI [+0.5%, +5.9%]. A coworker says "we're 95% sure the true lift is between +0.5% and +5.9%." Are they right?*

**Canonical answer:** **Strictly: no.** A 95% confidence interval doesn't say "there's a 95% chance the true value is in this range" — that's a Bayesian credible interval (a different object).

**The frequentist meaning is more awkward:** *"if we re-ran this experiment many times, 95% of the intervals constructed this way would contain the true value."*

**Practically, the coworker's interpretation is close enough for most decisions, with one caveat:** it assumes the data, the model, and the assumptions (independence, stationarity, no peeking) all hold. If those break, the interval doesn't even have its frequentist guarantee.

**What to actually use a CI for:**
- **Does the interval exclude zero?** If yes, effect is statistically distinguishable from no effect.
- **Is the lower bound positive AND big enough to matter?** If yes, ship.
- **Is the interval narrow?** Narrow CI = you have enough data to be confident in the magnitude. Wide CI = the experiment is underpowered or noisy, even if it crossed significance.

**Don't:** confuse CI width with effect size. A +3% point-estimate with [+0.1%, +5.9%] is much less confident than [+2.5%, +3.5%], even though both have the same point estimate.

---

### LO7. Decide one-sided vs two-sided tests.

**Prompt:** *When (if ever) should you use a one-sided test instead of the default two-sided?*

**Canonical answer:** **Almost never. Stick with two-sided as the default.**

- **Two-sided test:** asks "is the effect different from zero in either direction?" This is the default in most tools and the right choice for almost all real experiments because surprising negative effects are real and should be flagged.
- **One-sided test:** asks "is the effect greater than zero?" (or less than zero). Halves the alpha threshold needed on one side — easier to declare positive results — but loses the ability to detect a negative effect of the same magnitude.

**The legitimate use case for one-sided** is when you genuinely don't care about the direction other than the one you're testing (e.g., a non-inferiority test: "is the new version at least as good as the old?"). Even then, the right tool is usually a non-inferiority test with an explicit margin, not a flipped one-sided test.

**Bad reason to use one-sided:** "I want it to be easier to ship the variant." That's just inflating false-positive risk in one direction.

---

### LO8. Recognize Sample Ratio Mismatch (SRM).

**Prompt:** *You configured a 50/50 experiment, but you're seeing 47/53 with the chi-square test screaming. What does this mean, and what do you do?*

**Canonical answer:** **Sample Ratio Mismatch (SRM):** the actual allocation between arms doesn't match the configured allocation, beyond what random variation would explain.

**Why it's a red flag:** if the assignment mechanism is broken, the scorecard is meaningless. Whatever caused the imbalance probably also created a non-random difference between the arms, which is the entire thing experiments are supposed to avoid.

**Common causes:**
- Bot traffic disproportionately landing in one arm
- Bucketing bug — user IDs aren't stable across page loads, so the same user gets re-randomized
- Logging dropped from one arm but not the other (artifacts in the data pipeline)
- Asymmetric pre-experiment filtering (e.g., excluding "returning users" but the filter is applied unevenly)

**What to do:**
1. Stop trusting the results immediately.
2. Find the root cause before continuing.
3. Restart cleanly once fixed. Don't ship anything based on an SRM-flagged scorecard, even if the result "looks right."

Both Statsig and Amplitude Experiment auto-flag SRM. **Take the flag seriously.**

---

### LO9. Avoid common interpretation traps.

**Prompt:** *List three common ways teams mis-interpret experiment results and what to do instead.*

**Canonical answer:**

1. **Cherry-picking metrics.** Running 10 metrics, finding one that moved, declaring victory. **Fix:** pre-register primary and secondary metrics. Treat anything not declared upfront as exploratory.

2. **Misreading "not statistically significant" as "no effect."** Underpowered experiments routinely show null results that just mean "we couldn't detect anything at this sample size." **Fix:** check the confidence interval. If it's [-2%, +8%], you can't conclude no effect — you just need more data.

3. **Treating segment slices like primary results.** "It didn't move overall, but it moved 15% for iOS users in the US." That's the post-hoc-segmentation trap. Each slice multiplies your false-positive risk. **Fix:** use slices as exploratory hypothesis generation, not conclusion. If you want to claim the iOS-US lift, re-run an experiment targeted at that segment.

**Bonus traps to flag if asked:**
- **Survivorship bias** — comparing returning users to all users will always show "returning users have higher metrics" (they returned because they were already engaged)
- **Novelty effects** — short experiments overestimate effects because users are reacting to "new" rather than the actual change
- **Network effects** — A/B tests assume independence between units; if users influence each other (social products, marketplaces), the test under- or over-estimates the true effect

---

## When to point to live docs

If a learner asks about a specific UI configuration option (where the Bayesian toggle is, how to enable sequential testing in Statsig, what the defaults are), point them to:
- `https://docs.statsig.com/experiments/advanced-setup/bayesian`
- `https://docs.statsig.com/experiments/` (general experiments docs)
- `https://amplitude.com/docs/feature-experiment/experiment-theory/bayesian-statistics`
- `https://amplitude.com/docs/feature-experiment/` (general)

The general methodology in this topic file applies regardless of platform; the platform-specific UI lives in the docs.

## Why this topic exists

The Statsig Academy corpus introduces all of these concepts but only briefly. From Statsig 1.2 Wrap-up: "actually, I prefer Bayesian or actually, I want to run at a different conference interval... we won't go too in-depth on those ones here." This topic fills that gap with general statistical methodology so the skill can answer common learner questions without inventing or hallucinating.
