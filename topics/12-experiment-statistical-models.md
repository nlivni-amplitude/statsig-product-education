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

**Worked example — same data, two readings:**

Experiment on a checkout button. Control: 4,800 / 60,000 users converted (8.0%). Treatment: 5,160 / 60,000 (8.6%). Lift = +0.6 percentage points (about +7.5% relative).

- **Frequentist read:** Z-test on two proportions. Test statistic ≈ 3.8. p ≈ 0.00014. 95% CI on the lift in percentage points ≈ [+0.29, +0.91]. Decision: reject the null; the effect is statistically distinguishable from zero. The CI does not tell you the probability the true lift is in that range.
- **Bayesian read (with a weakly-informative prior centered at 0% lift):** posterior on the lift has mean ≈ +0.6 pp, 95% credible interval ≈ [+0.29, +0.91], **P(true lift > 0) ≈ 99.99%**, P(true lift > 0.3pp) ≈ 95%. The credible interval *does* mean "given the data and prior, the true lift is in this range with 95% probability."

**Why the intervals look identical:** with this much data and a weak prior, the posterior is dominated by the likelihood — Bayesian and frequentist arrive at the same numerical interval. What differs is the **interpretation language** (probability statements about the parameter vs. probability statements about repeated sampling).

**Where they diverge — small sample:**

Same setup but only 1,200 users per arm. Control: 96 / 1,200 (8.0%). Treatment: 103 / 1,200 (8.6%). Lift +0.6 pp.

- **Frequentist:** p ≈ 0.61, 95% CI [-1.6%, +2.8%]. Decision: cannot reject the null. The data is consistent with no effect. Don't ship on this evidence.
- **Bayesian with a prior derived from past similar experiments** that suggests "small positive lifts are common, large negative lifts are rare": posterior tilts toward positive. P(lift > 0) ≈ 78%. Decision: still not enough to ship on 95%, but the qualitative signal is "more likely than not." Some teams ship at lower thresholds (90%, even 80%) when downside is bounded.

**The takeaway:** Bayesian shines when you have a defensible prior and sparse data. Frequentist shines when you want to defend a result without arguing about the prior. With enough data and a flat prior they give numerically identical intervals and just different sentences to say them with.

**When Bayesian is the explicit better choice in Statsig:**
- **Sequential / always-valid testing** (LO2) — the natural language of "what's the posterior probability now?" maps onto "I want to peek" without needing alpha-spending math.
- **Small N studies** (small startups, early-stage products) where the prior is informative.
- **Stakeholder communication** — "85% probability of positive lift" is easier to defend in a non-technical meeting than "p = 0.07, fail to reject the null."

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

**Worked example:**

You're running an experiment on revenue per user. Pre-experiment, you have each user's revenue from the prior 4 weeks.

Without CUPED:
- Measured metric: `Y` = revenue during the 2-week experiment per user.
- A few whales dominate Y. Variance is high. To detect a +2% lift, you need ~80,000 users per arm.

With CUPED:
- Adjusted metric: `Y_cuped = Y - θ × (X - X̄)`, where:
  - `X` = each user's pre-experiment revenue (the covariate)
  - `X̄` = the population mean of `X`
  - `θ` (the "CUPED coefficient") = `Cov(Y, X) / Var(X)`. In practice this is a regression coefficient — the platform estimates it from the pre-period data.
- For each user, you subtract the part of their experiment-period revenue that was predictable from their pre-period revenue.
- The mean of Y_cuped equals the mean of Y (the population-level shift `θ × X̄` is constant) — so the *estimate of the treatment effect is unchanged*.
- But Var(Y_cuped) < Var(Y) by a factor of (1 − ρ²), where ρ is the correlation between X and Y.
- If pre-period revenue correlates 0.7 with experiment-period revenue, variance drops by 1 − 0.49 = 51%. Required sample drops by ~half.

**The intuition again, with numbers:**
- A user spent $100 pre-period. They spend $110 during the experiment. Naïve metric: $110 (huge noise).
- CUPED: "we expected $100-ish based on pre-period. Actual is $110. Residual is +$10." That residual is what the treatment-effect estimator sees.
- Whales no longer overwhelm the metric, because the predictable-whale-part has been subtracted out.

**Edge case — when CUPED doesn't help:**
- **New users with no pre-period data:** `X` is undefined or 0. CUPED contributes nothing for them. Statsig falls back to the unadjusted metric for these users; precision improvement is concentrated on the returning-user subset.
- **Brand-new metric** the user hasn't generated pre-experiment data for (e.g., new event you just shipped). Same problem.
- **Metric with low temporal correlation:** if a user's pre-period and experiment-period values are nearly independent, ρ ≈ 0 and Var(Y_cuped) ≈ Var(Y). No benefit.

**Practical sanity check:** Statsig will tell you the variance reduction CUPED achieved on each metric. If it shows <10% variance reduction, the covariate isn't predictive enough to bother enabling on that metric (the small bias-amplification cost can dominate the gain).

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

### LO10. Correct for multiple comparisons (Bonferroni, Benjamini-Hochberg).

**Prompt:** *Your scorecard has 12 metrics and 3 test variants. A coworker celebrates: "look, metric #7 moved with p=0.04 on Variant B!" What's the issue, and what would Bonferroni or Benjamini-Hochberg do about it?*

**Canonical answer:**
**The issue:** every additional metric or variant is another opportunity for a false positive. With 12 metrics × 3 variants = 36 comparisons at α=0.05, the chance of *at least one* false positive jumps from 5% to ~84%. "Look, this one moved" is exactly what you'd expect by chance.

**Two standard corrections:**

- **Bonferroni correction** — divide α by the number of comparisons. With 36 tests at α=0.05, each comparison is judged at α=0.05/36 ≈ 0.0014. Strict. Controls the *Family-Wise Error Rate* (probability of any false positive). Easy to explain. Too conservative when you have many real effects.

- **Benjamini-Hochberg (BH) procedure** — controls the *False Discovery Rate* (expected fraction of false positives among the things you call significant). Less strict than Bonferroni; better statistical power. Statsig uses BH on top-line metrics when enabled.

**When to apply:**
- Multiple test variants (3+ arms): apply across variants.
- Many metrics in the scorecard: apply across metrics (often weighted — primaries get more α than secondaries).
- Both: apply both layers.

**Practical:** both Statsig and Amplitude Experiment have toggleable Bonferroni/BH corrections in experiment settings. **The right default is to enable BH** if you have >1 primary metric or >2 variants.

**The fix for the coworker's claim:** ask whether the scorecard applied any correction. If not, the p=0.04 result is probably noise.

**Worked example — Bonferroni:**

Suppose 36 comparisons (12 metrics × 3 variants), uncorrected α = 0.05.
- Probability *one* comparison is a false positive under the null: 0.05.
- Probability *all 36* are clean under the null: (1 − 0.05)^36 ≈ 0.158.
- Probability of *at least one* false positive: 1 − 0.158 ≈ **84.2%**.

Bonferroni-adjusted α = 0.05 / 36 ≈ **0.00139** per comparison.
- A p-value of 0.04 (the coworker's celebration) → 0.04 > 0.00139 → **fails** at Bonferroni-adjusted threshold. Not significant.
- For a metric to clear Bonferroni at this scorecard size, it needs p ≤ 0.00139 — roughly equivalent to a z-score around 3.2 instead of the unadjusted 1.96.

Bonferroni is provably conservative. With 36 tests and one true effect of moderate size, Bonferroni often misses it; you lose power proportional to the number of tests.

**Worked example — Benjamini-Hochberg (BH) at FDR = 0.05:**

Same 36 comparisons. Sort the p-values smallest to largest, rank them 1 to 36.

| Rank `i` | p-value | BH threshold = (i / 36) × 0.05 | Significant? |
|---|---|---|---|
| 1 | 0.0008 | 0.00139 | yes |
| 2 | 0.0017 | 0.00278 | yes |
| 3 | 0.0028 | 0.00417 | yes |
| 4 | 0.0091 | 0.00556 | no |
| 5 | 0.012 | 0.00694 | no |
| ... | ... | ... | ... |
| 12 | 0.04 | 0.01667 | no |
| ... | ... | ... | ... |

BH walks from the bottom up and finds the **largest `i` where p_i ≤ (i/36) × 0.05** — call that `k`. Then everything from rank 1 to `k` is called significant.

In this hypothetical: largest `i` where p_i ≤ threshold is `i = 3` (p = 0.0028 ≤ 0.00417). So the top 3 p-values are significant; ranks 4-36 are not.

The coworker's p = 0.04 sits at rank 12 (or wherever) — well above its BH threshold of 0.01667. Not significant under BH either.

**Why BH beats Bonferroni in practice:**
- Bonferroni controls *family-wise error rate*: "probability of any false positive in the family." Brutal when the family is large.
- BH controls *false discovery rate*: "expected fraction of false positives among the things we call significant." If you call 10 things significant under BH, you're saying "at most 0.5 of those are likely noise" — a calibrated, useful guarantee.
- BH gives strictly more power than Bonferroni when there are real effects. Use Bonferroni only when even one false positive is unacceptable (regulatory contexts).

**Per-family vs. across-family correction:**
- **Across primary metrics:** apply BH within primary tier (e.g., 3 primary metrics × 3 variants = 9 tests).
- **Across all metrics:** more conservative — apply BH to the union of primary + secondary + guardrails.
- Statsig's default is to correct primary tier separately from secondaries, on the reasoning that secondaries are exploratory and shouldn't compete with primaries for alpha.

---

### LO11. Use AA tests to validate the experimentation pipeline.

**Prompt:** *Your team is new to running experiments. What's an AA test, and why would you run one before your first real A/B?*

**Canonical answer:**
**An AA test is an A/B test where both variants serve the exact same experience.** Identical. No real treatment.

**What you should see:**
- Exposures flowing through to both arms in the configured split
- Roughly 5% of metrics flagging as "statistically significant" at α=0.05 — because that's literally what 5% false-positive rate means
- No Sample Ratio Mismatch
- No structural difference between the arms

**Why run one:**
- **Trust the pipeline before you trust the results.** If your AA shows SRM, broken exposure logging, or 20% of metrics flagging significant, something in the ingestion / assignment / instrumentation is wrong. Better to find that before you ship a "winner" you can't trust.
- **Calibrate your team.** New experimenters often panic when they see one metric flag significant — an AA test makes them feel the 5% false-positive rate.
- **Validate metric variance assumptions.** If a metric's actual variance differs wildly from what the platform assumes, your sample size calculations will be wrong.

**Online vs offline AA:** an online AA runs against real traffic. An offline AA queries historical data and randomly splits it post-hoc. Statsig runs simulated AA tests automatically in the background every day to monitor platform health.

---

### LO12. Decide when to call an experiment vs defer the decision.

**Prompt:** *An experiment has run for the planned duration. Primary metric is positive but the CI just barely excludes zero. Secondary metrics are mixed. The team is split on whether to ship. What's the framework?*

**Canonical answer:**

**Three legitimate paths:**

1. **Ship the variant** — primary cleared the bar (significance + meaningful magnitude); guardrails are clean; secondaries don't reveal anything alarming.
2. **Roll back / ship control** — primary went the wrong way OR a guardrail regressed badly.
3. **Conclude experiment, defer decision** — stop running, stop exposing new users, but don't ship either variant yet. Used when:
   - Results are inconclusive but you've already spent the budget you planned
   - You want to consult stakeholders before deciding
   - You want to lock the data in place while a follow-up experiment is designed
   - The metric improved but you suspect novelty effect — defer and watch

**The "conclude and defer" path matters.** Without it, teams get stuck: experiment is still running (wasting traffic), or they pick under-evidenced. Defer cleanly separates "stop the experiment" from "decide what to do."

**What to NOT do:**
- **Keep running indefinitely waiting for clarity.** That's just delaying the decision and costs traffic. If you didn't hit significance in the planned duration, you've already learned that the effect is smaller than you thought; running longer is selection bias.
- **Run a follow-up experiment "to confirm"** without changing anything. That's just a second chance to roll the dice. If you want to confirm, change something material (longer run, different segment, new variant).

**Both Statsig and Amplitude Experiment** support "conclude without shipping" as an explicit decision state — use it.

---

### LO13. Understand the delta method for ratio metrics.

**Prompt:** *You're measuring clicks-per-session in an experiment. Your tool flags this as a "ratio metric." Why does it need special handling?*

**Canonical answer:**
**A ratio metric** is one where the numerator and denominator both vary per user — like clicks/session, revenue/session, or conversion rate.

**Why it needs special handling:**
- For simple metrics (e.g., total revenue per user), variance is straightforward — each user contributes one observation.
- For ratio metrics, the numerator and denominator are **correlated** (a user with more sessions tends to have more clicks). Naïvely computing the variance of clicks/sessions as if they were independent **gives the wrong confidence interval** — usually wider than it should be, sometimes narrower.

**The delta method** is the standard statistical correction. It computes the variance of a ratio using a Taylor approximation that accounts for:
- The variance of the numerator
- The variance of the denominator
- The **covariance** between them

Result: confidence intervals on ratio metrics are accurate even though the underlying variables move together.

**Why you need to know:**
- **It runs automatically in Statsig and Amplitude Experiment** — you don't compute it yourself. But if you ever export raw data and compute confidence intervals by hand, you'll get wrong answers if you ignore covariance.
- **Recognize when a metric is a ratio.** Anything per-user, per-session, or per-event with a variable denominator. If the platform flags "delta method applied," that's correct behavior.

**For relative lifts** (e.g., "+5% relative to control"), platforms sometimes use a related approach called **Fieller intervals**, which the delta method approximates for large samples.

**Worked example — what goes wrong without the delta method:**

Metric: clicks per session. Each user has multiple sessions and multiple clicks. Suppose:
- Control: 10,000 users contributed 50,000 sessions and 2,500 clicks. Ratio = 2,500 / 50,000 = **0.050 clicks/session**.
- Treatment: 10,000 users contributed 50,000 sessions and 2,700 clicks. Ratio = 2,700 / 50,000 = **0.054 clicks/session**.
- Observed lift: +0.004 clicks/session (+8% relative).

**Naïve approach (wrong):** treat each *session* as an independent observation. Variance of clicks-per-session over the 100,000 sessions gives a tight standard error, suggesting the +0.004 lift is highly significant.

**The problem:** sessions from the same user are *not* independent. A user with 10 sessions and 5 clicks contributes 10 "observations" of 0.5 clicks/session, all driven by the same underlying user behavior. The effective sample size is closer to the number of *users* (10,000) than the number of *sessions* (50,000). The naïve standard error is too small by a factor proportional to √(sessions per user).

**Delta method correctly handles it:**
- Treat the metric as `R = mean(clicks_per_user) / mean(sessions_per_user)`.
- Compute `Var(R) ≈ (1 / mean(sessions))² × [Var(clicks) − 2 × R × Cov(clicks, sessions) + R² × Var(sessions)]`.
- The covariance term `Cov(clicks, sessions)` is typically positive (users who session more also click more), which the formula correctly accounts for.
- Result: a wider, accurate CI on R. Often the variance of a ratio metric ends up 1.5-4× larger than the naïve estimate.

**In our example:** the naïve CI might say [+0.0035, +0.0045], suggesting the +0.004 lift is locked in. The delta-method CI might say [+0.001, +0.007] — still positive, but with much more honest uncertainty. The decision changes from "obvious ship" to "ship but recognize the wider band."

**Two practical implications:**
1. **Don't compute ratio metric CIs by hand from row-level event data.** You need to either roll up to the user level first (and even then mind the per-user-session counts) or use a tool that applies the delta method automatically.
2. **Watch for "this metric got more significant when we increased the sample" with no other change.** That can mean the naïve method is over-counting independence. The delta-method-corrected significance grows more slowly than the naïve method, which is the correct behavior.

**When the delta method ISN'T enough:**
- Highly skewed numerators with rare events (e.g., revenue per user where most users have zero revenue). The Taylor approximation under the delta method assumes near-normality and breaks down. Use bootstrap or log-transformed metrics instead.
- Very small samples — the delta method's variance estimate has its own variance, which matters when N < ~100.

---

### LO14. Understand stratified sampling for variance reduction.

**Prompt:** *What is stratified sampling, when does it help, and how does it differ from CUPED?*

**Canonical answer:**

**Stratified sampling** divides the user population into mutually-exclusive strata (e.g., new vs. returning, country, plan tier) and assigns variants **within each stratum** at the configured allocation. Every stratum ends up with the same treatment:control ratio. This eliminates the chance that, say, 60% of your power users land in treatment by random allocation.

**How it works:**
- Define stratification dimensions before the experiment (e.g., `country × signup_cohort`).
- The bucketing algorithm splits users into strata and runs the 50/50 (or whatever) within each.
- Result: across the whole experiment, your strata are balanced — control and treatment have the same proportion of US-vs-EU users, new-vs-returning, etc.

**Why it reduces variance:**
When you compare control to treatment, you're no longer comparing groups that differ on stratification variables. Any *between-strata* difference (e.g., US users convert more than EU users) is removed from the noise. You only see *within-stratum* differences — which is the actual treatment effect.

Effect size on confidence intervals: typically 5-20% tighter CIs, depending on how predictive your strata are of the metric.

**Stratified sampling vs. CUPED — when to use which:**
| | Stratified sampling | CUPED |
|---|---|---|
| **What it controls for** | Categorical user attributes you specify | Each user's pre-experiment value of the metric |
| **When to use** | Known imbalanced segments (e.g., heavy users dominate the metric) | Any metric where pre-period behavior predicts post-period |
| **Setup cost** | Pick the right strata; too many = thin cells | None — automatic if pre-period data exists |
| **Stackable?** | Yes, combines with CUPED | Yes |

**Practical recommendation:** if you have an obvious dimension where the metric varies a lot (country, paying vs. free, mobile vs. web), stratify on it. CUPED on top is purely additive.

**Common pitfalls:**
- **Strata too thin:** if any stratum has fewer than ~100 users per arm, you get noisier estimates inside it, not less. Limit to 2-4 strata of meaningful size.
- **Stratifying on post-treatment attributes:** never stratify on something the experiment itself can change. Pre-experiment attributes only.

---

### LO15. Recognize heterogeneous treatment effects and use Differential Impact Detection.

**Prompt:** *What are heterogeneous treatment effects, and how does Statsig surface them?*

**Canonical answer:**

A **heterogeneous treatment effect (HTE)** is when the treatment effect varies across subgroups. The global lift might be +2%, but for new users it's +8% and for power users it's -3%. The global number hides both.

**Why this matters:**
- A non-zero global effect can mask a negative effect on a critical segment (regress on power users while a "+2% lift" ships).
- A null global result can hide a real effect that's positive for one group and negative for another that cancel out.
- Shipping decisions based on the global number alone are routinely wrong when effects are heterogeneous.

**The traditional fix:** manually segment after the fact. Re-run analysis sliced by country, cohort, plan tier, etc. The problem: every slice is a multiple-comparisons risk (see LO10). Slicing 20 ways and reporting the most extreme is p-hacking.

**Statsig's Differential Impact Detection (DID):** auto-surfaces segments where the treatment effect is significantly different from the global effect, with multiple-comparison correction applied. Rather than you manually picking 20 slices, the platform scans property dimensions and reports only segments where the difference is statistically defensible.

**How to read a DID result:**
- **Global lift:** +2% on conversion.
- **DID surfaces:** "Mobile users: -1.5% (significant). Desktop users: +4% (significant)."
- **Decision implication:** the change is good for desktop, bad for mobile. Don't ship as-is; consider gating to desktop only or fixing the mobile regression first.

**When to look for HTE:**
- New flows where you don't know how the change interacts with different audiences.
- Big visual changes (different cohorts react differently to UI shifts).
- Performance changes (mobile/desktop, slow-network/fast-network).
- Anything where you suspect segments might diverge.

**Amplitude counterpart:** Amplitude Experiment doesn't auto-detect HTE; analysts segment results manually post-hoc. Statsig's DID is the first-class equivalent of that manual workflow with stat correction baked in.

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
