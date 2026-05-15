# Statsig Topics — Learning Objectives + Canonical Answers

Per-topic learning files used by the interactive course experience. Each file contains:
- **Frontmatter** — source modules (which Statsig U courses cover the topic), Amplitude counterpart, and audit notes (where the content is shallow)
- **Learning Objectives** — application-level (not recall-level) objectives the learner should hit
- **Prompts** — free-text questions for explanation LOs, scenarios for application LOs
- **Canonical answers** — what to grade against

These files are the source of truth for:
- The interactive course flow (`statsig-take-quiz`, `learn-statsig`)
- Test-out-of-section logic (use the LO list to design pass/fail questions)
- Quiz generation (`statsig-generate-quiz` pulls from the canonical answers)

## Topic index

| # | Topic | Source modules | Amplitude counterpart |
|---|---|---|---|
| 01 | Introduction to Statsig | Statsig 2 / Module 1 | Spans Amplitude Analytics + Experiment + Session Replay |
| 02 | SDKs — Setup and Initialization | Statsig 2 / M2, Statsig 3 / M2 | Amplitude SDKs + Amplitude Experiment SDK |
| 03 | Feature Flags / Feature Gates | Statsig 1 / M3, Statsig 2 / M3 | Amplitude Experiment (flag side) |
| 04 | Dynamic Configs | Statsig 2 / M3 | Payloads in Amplitude Experiment |
| 05 | Experiments | Statsig 1 / M2, Statsig 2 / M4 | Amplitude Experiment |
| 06 | Product Analytics | Statsig 1 / M4, Statsig 2 / M5 | Amplitude Analytics |
| 07 | Session Replay | Statsig 2 / M1 (mentioned) | Amplitude Session Replay |
| 08 | Data and Metrics | Statsig 3 / M3 | Amplitude event taxonomy + Custom Metrics |
| 09 | Org and Project Settings | Statsig 3 / M4 | Amplitude Org / Workspace / Project |
| 10 | Build → Ship → Measure → Learn | Statsig 2 / M6 | Same loop, split across Amplitude products |
| 11 | Best Practices | Statsig 1 / M5 | Same principles apply |

## How to use these files

**For learners:** these aren't read end-to-end. They're question banks the interactive skills pull from. A learner runs `statsig-take-quiz` and the skill picks the LOs relevant to the chosen topic.

**For LXD / Ampliteers maintaining the plugin:** when content drifts (new Statsig features, deprecated concepts, changed Amplitude mapping), update the relevant topic file's LOs and canonical answers. The skills that read from this directory will pick up the changes automatically.

**Format conventions:**
- LO statement starts with an action verb (Bloom's apply/analyze level, not recall)
- Prompt is free-text where explanation is required, scenario-based where categorical
- Canonical answer is the standard to grade against — should be tight enough to compare a learner response to, not encyclopedic
