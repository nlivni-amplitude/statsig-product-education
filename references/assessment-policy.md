# Assessment Policy

The rules every assessment skill (`statsig-take-quiz`, test-out flows in `learn-statsig`, future post-tests) follows.

## Structure overview

For any topic in `data/topics/*.md`:

```
PRE-TEST  →  (test out or take the lesson)  →  POST-TEST  →  (mastered or review)
                                                              ↓
                                  (after all chosen topics)
                                                              ↓
                                                       CUMULATIVE EXAM
                                                              ↓
                                                  (passed or review missed)
```

## Question generation rules

- **Source:** primary question bank is `data/topics/*.md`. Each LO produces at least one question.
- **Coverage:** every LO in scope must have ≥1 question on the pre-test, ≥1 on the post-test, and is eligible for the cumulative exam.
- **Question types:** scenario-based or compare/contrast preferred over recall. Use the LO's prompt as-is when it's a free-text explanation; convert it to a clickable scenario when it's categorical.
- **Distractors:** for multiple-choice, use plausible-but-wrong options drawn from common misconceptions (e.g., for "client vs server SDK", a distractor might be "client SDKs are paid, server SDKs are free" — clearly wrong but tempting if the learner is fishing).

## Pre-test (test-out logic)

**Purpose:** let a learner skip a topic they already know.

**Length:** one question per LO in the topic (4-9 questions depending on topic depth).

**Cut score for testing out:** **miss ≤2 questions** = tested out, advance to next topic.

**If they miss >2 questions:** stop the pre-test immediately, do NOT let them continue testing out, and route them into the lesson covering the LOs they missed. They can still skip LOs they got right.

**Behavior on miss-3:** when the third miss happens mid-test, surface the rationale:
> *"You've missed 3 questions on this topic. Test-out won't apply — I'll walk you through the lesson instead. The LOs you missed: [list]. Ready to start?"*

Don't grade the rest of the pre-test; don't punish them with more questions they don't have context for yet.

## Lesson (between pre- and post-test)

Teach the LOs the learner missed on the pre-test. If they missed >2, teach all the LOs they got wrong (not necessarily all LOs in the topic — keep it focused).

**Hard sequencing rule:** the lesson must be fully rendered as visible content **before** any post-test question fires. No placeholder text ("Working on it...", "Loading...", etc.) stands in for the lesson. Render the full canonical-answer text for each missed LO, end with an explicit "Ready for the post-test?" checkpoint via `AskUserQuestion`, and only proceed to the post-test on affirmative click.

**Anti-pattern to avoid:** announcing the test-out stop and immediately scheduling post-test questions in the same turn. The learner needs the lesson on screen first. If you find yourself queueing the next question before the lesson is rendered, stop and render the lesson.

## Post-test

**Purpose:** confirm mastery before advancing.

**Length:** at least one question per LO covered in the lesson (same coverage as pre-test for the relevant LOs).

**Cut score:** **80%**.
- Pass (≥80%) → topic marked mastered in `state.json` (`topics_mastered`), advance.
- Fail (<80%) → stop the assessment, prompt review of missed answers (see "Review prompt" below).

## Cumulative exam

**Purpose:** confirm cross-topic application after the learner has finished multiple topics.

**Length:** roughly 1 question per LO across topics in scope (or a subset weighted toward harder/critical LOs).

**Cut score:** **80%**.

**Adaptive stopping rule:** if it becomes mathematically impossible to reach 80%, stop the exam.

- Formula: if `missed > 0.20 × total_questions`, stop.
- Example: 20-question exam. Threshold = 20 × 0.20 = 4. If learner misses the **5th** question, stop (max possible = 15/20 = 75%).
- Example: 10-question exam. Threshold = 2. If learner misses the **3rd** question, stop.

**On adaptive stop:** surface honestly:
> *"You've missed [N] questions out of [k] so far. Even a perfect score on the remaining [N-k] couldn't get you to 80%. Stopping here so we can review the topics you struggled with."*

Then route into review for the topics where the missed questions came from.

## Review prompt

When the learner fails any assessment (post-test or cumulative), don't just re-ask the same questions. Surface the missed concepts and offer routes:

1. **Re-teach the specific LOs** — pull the canonical answer from the relevant topic file, present it clearly, let the learner re-attempt
2. **Watch the source video** — route to `statsig-watch-this` for the relevant lesson
3. **Dive deeper** — route to `statsig-ask` for free-form Q&A on the concept
4. **Skip and come back** — mark the topic as "needs review" in `state.json` for spaced repetition

Use `AskUserQuestion` with header `Review`.

## State tracking

Every assessment writes to `${CLAUDE_PLUGIN_ROOT}/state.json` (or `${CLAUDE_PLUGIN_ROOT}/state.json`):
- `topics_mastered` — list of `{topic, mastered_at}` for topics where the learner passed post-test or cumulative
- `topics_missed` — list of `{topic, lo, missed_at}` for individual LOs the learner missed (drives spaced repetition)
- `quiz_history` — append-only log of `{assessment_type, topic, score, total, timestamp}`
- `confidence_ratings` — optional learner self-rating after a topic completes

## Why these specific numbers

- **Test-out at "miss ≤2"** — leaves room for one careless answer plus one genuine knowledge gap without forcing a re-do. Tighter than that frustrates legitimate learners; looser lets people skip topics they don't actually know.
- **80% cut score** — standard threshold for "demonstrated mastery" in most assessment frameworks. Aligns with how Skilljar and other LMS platforms grade.
- **Adaptive stop on cumulative** — protects learner time. There's no value in finishing an exam you can't pass; better to refocus on review immediately. Also surfaces the "stuck" topics faster.

## Honesty conventions

- Always tell the learner the cut score *before* the assessment starts ("You'll need 80% to pass this section").
- Always tell them the test-out threshold *before* the pre-test ("Miss more than 2 and we'll cover the material together").
- After any stop (adaptive or post-test fail), explicitly name the LOs they missed. No vague "review the section" — point at the exact concepts.
- Self-explanation before reveal: for any question marked `requires_explanation: true`, prompt the learner to explain their reasoning *before* you reveal right/wrong. Effect size d≈0.6 for retention.
