---
topic: session-replay
source_modules:
  - Statsig 2 / Module 1 — Introduction to Statsig (mentioned)
  - Statsig 2 / Module 6 — referenced in lifecycle context
amplitude_counterpart: "Amplitude Session Replay"
audit_note: "Validated content treats Session Replay shallowly. Deep mechanics, sampling strategy, and PII handling are not deeply explained in the migration corpus."
---

# Session Replay

Record-and-replay of user sessions. The "why" half of the analytics loop — see what users actually did, not just what the events say they did.

## Learning Objectives

### LO1. Identify when Session Replay adds value over Product Analytics alone.

**Prompt:** *Product Analytics tells you what users did. When does Session Replay add something Analytics can't, and when is it overkill?*

**Canonical answer:**
**Adds value when:**
- A funnel reveals a drop-off but the events don't explain *why* (users see a confusing modal? a button isn't clickable? a layout issue on a specific device?)
- A bug is hard to reproduce — replay shows the actual sequence of clicks and inputs that triggered it
- UX qualitative feedback contradicts the metrics — replay grounds the debate
- An experiment loser is surprising — watching sessions of the losing arm reveals friction the metrics didn't capture

**Overkill when:**
- The funnel question is "how big is the drop-off" (Analytics already answers)
- The metric is at a population scale where individual sessions are noise
- The signal is statistical (correlations, segmentation) rather than experiential

**Rule of thumb:** if the question starts with "why did they..." or "what happened when...", Session Replay is the tool. If it starts with "how many..." or "what %...", stay in Analytics.

---

### LO2. Reason about sampling strategy.

**Prompt:** *You can't record every session — too much data, too much cost, too many privacy concerns. How do you decide what to sample?*

**Canonical answer:** **Strategy: sample by what answers your question.**
- **Funnel-based** — record sessions that hit a specific funnel state (e.g., started checkout but didn't complete). Yields the highest-signal sessions for diagnosing the dropoff.
- **Error-triggered** — record any session that hit a JS error or API failure. Diagnostic-rich.
- **Cohort-based** — record sessions from new users, or paid users, or a specific country. Useful for understanding a segment.
- **Random %** — baseline (e.g., 1-5% of all sessions) gives a representative sample for general health monitoring.

**Avoid 100% sampling** unless you have a specific need — cost scales linearly and privacy exposure scales with it.

**Note:** the validated Statsig corpus treats Session Replay shallowly. Specific sampling configuration details are best verified against current Statsig docs.

---

### LO3. Handle PII in replays.

**Prompt:** *Session Replay records what the user sees. That can include PII (names, emails, payment fields, addresses). How do you handle this?*

**Canonical answer:**
- **Mask sensitive elements at the recording layer.** Statsig (and Amplitude Session Replay) supports CSS class or attribute-based masking — mark sensitive fields as "do not record" and the recording shows them as redacted/blocked.
- **Default to mask** — credit card fields, password fields, anything in a `[data-private]` block. Opt-in to record sensitive data only with explicit reason.
- **Don't record full-page screenshots of pages with PII** even if individual fields are masked — combination data (a name plus an address visible together) is still PII.
- **Compliance** — if you're under GDPR/CCPA, document your replay retention policy and provide deletion on request.

The audit corpus doesn't deeply cover Statsig-specific PII configuration, so confirm specific selectors and defaults against current Statsig docs.

---

### LO4. Contrast Statsig Session Replay with Amplitude Session Replay.

**Prompt:** *Statsig Session Replay and Amplitude Session Replay both record sessions. Where do they differ?*

**Canonical answer:** **Mapping is close at the basic level** — both record DOM mutations + interactions, both play back, both let you filter by user/event/cohort.

**Differences (subject to evolution as both products develop):**
- **Integration depth** — Statsig integrates Session Replay tightly with its experiments (watch replays of users in the losing arm). Amplitude integrates with Analytics charts (jump from a funnel drop-off to the replays of users who dropped). Different anchor points for the same underlying capability.
- **Pricing/sampling model** — both meter on recorded session volume; specifics vary.

The validated Statsig corpus is light on Session Replay mechanics — when going deeper with a customer, check current docs for both products.
