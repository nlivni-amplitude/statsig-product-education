# Audit Gaps Lookup

Normalized lookup of topics the LXD audit flagged as introduced-but-not-deeply-explained in the validated Statsig content. Skills consult this before answering or recommending content on a flagged topic.

Source: `${CLAUDE_PLUGIN_ROOT}/data/synthesized/audit-findings.md` (canonical, may have nuance beyond this table)

## Known gaps

| Topic | Surface area | Gap | Recommended mitigation |
|---|---|---|---|
| **CUPED** | Experiments | Treated as a toggle. Variance-reduction mechanics not explained. | Tell user the content treats it as a UI toggle; for the underlying math, recommend outside variance-reduction reading. Quiz at toggle-level only. |
| **Multi-arm bandits** | Experiments | Mentioned as a Statsig capability. No depth on when/how/why. Amplitude has no direct equivalent. | When user asks how it works, be honest about shallow coverage. For Amplitude comparison, note no equivalent (`statsig-compare-to-amplitude` table flags this). |
| **Session Replay deep dive** | Session Replay | Surface-level explanation; not enough on PII rules, sampling strategies, or replay-experiment integration. | Quiz on what's there. For deeper questions, suggest user check Statsig's docs. |
| **Target Apps setup** | Statsig architecture | Concept introduced but the setup flow isn't covered in depth. No Amplitude equivalent so comparison is awkward. | Flag this when comparing or migrating. Recommend hands-on Statsig docs for setup specifics. |
| **CUPED interaction with holdouts** | Experiments | Mentioned in passing; no clear guidance. | Be candid about coverage. |
| **Warehouse Native vs Cloud differences (deep)** | Architecture | Both are described; the *implications* of choosing one over the other aren't fully unpacked. | For comparison and migration questions, work from the comparison table; flag the comparison depth limit. |

## How skills use this

1. Parse the user's question for topic keywords.
2. Cross-reference the table above.
3. If a match: surface the gap with the standard disclosure language from `skill-conventions.md`, plus the recommended mitigation.
4. Continue answering with what *is* covered.

## When to update this file

When new audit findings are added to `${CLAUDE_PLUGIN_ROOT}/data/synthesized/audit-findings.md`, mirror the high-level entries here as a normalized lookup. This file is intentionally shorter than the audit doc — it's a quick-reference index, not the full analysis.
