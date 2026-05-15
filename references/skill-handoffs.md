# Skill Handoffs Map

Canonical "what to recommend next" map. Each skill's end-of-workflow `AskUserQuestion` offers two sibling skills + "Done for now" — pick the most natural follow-ups from this table.

## Per-skill handoffs

| Current skill | Best next (Recommended) | Alt next |
|---|---|---|
| `learn-statsig` | `statsig-ask` (jump into Q&A) | `statsig-study-plan` (structured ramp) |
| `statsig-ask` | `statsig-take-quiz` (test retention on this topic) | `statsig-watch-this` (see the source video) |
| `statsig-glossary` | `statsig-ask` (deeper explanation) | `statsig-compare-to-amplitude` (Amplitude equivalent) |
| `statsig-compare-to-amplitude` | `statsig-ask` (go deeper on the concept) | `statsig-watch-this` (see how it works in practice) |
| `statsig-watch-this` | `statsig-ask` (follow-up Q&A on what they watched) | `statsig-take-quiz` (test understanding) |
| `statsig-generate-quiz` | `statsig-take-quiz` (take it interactively instead) | `statsig-study-plan` (structured prep) |
| `statsig-take-quiz` | `statsig-study-plan` (close gaps the quiz revealed) | `statsig-generate-quiz` (another round, static) |
| `statsig-study-plan` | `statsig-take-quiz` (verify retention after) | `statsig-watch-this` (start the first lesson) |
| `setup-my-statsig-notebook` | (terminal — opens NotebookLM, no in-workspace next) | `statsig-ask` (compare experiences) |

## Format for the AskUserQuestion call

After the skill's primary output, render one `AskUserQuestion`:

- **question**: short — "What now?" or a context-specific framing like "What would help next?"
- **header**: `Next` (under 12 chars)
- **multiSelect**: `false`
- **options** (3):
  1. `<Best next skill action>` with `(Recommended)` suffix and a 1-line description
  2. `<Alt next skill action>` with a 1-line description
  3. `Done for now` (no further action)

The option *label* should describe the action in plain English ("Take a quiz on what you just learned"), NOT name the skill ("Run statsig-take-quiz"). The user shouldn't need to know the skill names.

## When the user picks an option

Translate the click into a natural-language prompt that fires the right skill:

| Clicked label | Natural-language prompt to act on |
|---|---|
| "Take a quiz on this topic" | "Quiz me interactively on `<topic just discussed>`" → fires `statsig-take-quiz` |
| "Watch the lesson" | "What should I watch for `<topic>`?" → fires `statsig-watch-this` |
| "Build a study plan based on what I missed" | "Build me a Statsig study plan focused on `<missed topics>`" → fires `statsig-study-plan` |
| "Define a term" | Open conversation; next user message naturally triggers `statsig-glossary` |
| "Compare to Amplitude" | "What's the Amplitude equivalent of `<concept>`?" → fires `statsig-compare-to-amplitude` |
| "Done for now" | Wrap up. Don't push further. |

## Style

Handoff prompts should feel like "here's a natural next step", not "click here to use another tool." Frame them around the user's intent, not the system's mechanics.
