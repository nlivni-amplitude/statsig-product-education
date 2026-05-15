# Footnote Format Reference

Every answer cite-block should use markdown footnote syntax with at least one canonical source URL plus the raw file path. Templates by source type:

## Lesson video (Wistia)

Look up the lesson by name in `${CLAUDE_PLUGIN_ROOT}/data/index/wistia-cross-reference.json`. Use the `wistia_url` field for the player link and the `wistia_player_html` field if embedding.

```markdown
[^N]: **Statsig 1.3 — Overrides** · [Watch on Wistia](https://amplitude.wistia.com/medias/hu72riryrj) · [Academy lesson](https://academy.amplitude.com/statsig-product-onboarding) · raw: `${CLAUDE_PLUGIN_ROOT}/data/raw/captions/Statsig 1.3 - Overrides.txt`
```

## Course-level reference (Academy)

Look up the course in `${CLAUDE_PLUGIN_ROOT}/data/index/academy-course-map.json` to get the slug → URL.

```markdown
[^N]: **Statsig 101 (full course)** · [Open in Academy](https://academy.amplitude.com/statsig-101) · raw: `${CLAUDE_PLUGIN_ROOT}/data/raw/courses/statsig-2-statsig-101.md`
```

## Live training session (Zoom)


```markdown
```

## YouTube video

Look up the video by ID in `${CLAUDE_PLUGIN_ROOT}/data/index/youtube-source-map.json`. Use the `url` field.

```markdown
[^N]: **"<video title>"** (YouTube product walkthrough) · [Watch](https://www.youtube.com/watch?v=<id>)
```

## Synthesized doc only (no original source)

When citing an LXD-authored synthesized doc (audit findings, persona views), cite the doc directly — no Wistia/Academy/Zoom URL.

```markdown
[^N]: **LXD Content Audit Findings** (May 2026) · `${CLAUDE_PLUGIN_ROOT}/data/synthesized/audit-findings.md`
```

## Combined citation when multiple sources support one statement

```markdown
[^N]: **Targeting rules + conditions** — covered in: Wistia lesson [Targeting rules and conditions](https://amplitude.wistia.com/medias/b9evmxhgua) · Live discussion in [Statsig 101 enablement session](https://amplitude.zoom.us/clips/share/QAhZ-fRqTT-XmOJvaUmnZw) · Course module: [Statsig Product Onboarding M3](https://academy.amplitude.com/statsig-product-onboarding)
```

## Rules

- **One footnote per claim.** Don't lump all sources into a single footnote at the end of the response.
- **Always one clickable URL minimum.** File-path-only citations don't help the learner watch the actual content.
- **Order URLs by depth** — link to the video/clip first (richest source), then the course context, then the raw file path.
- **Include "live session" or "YouTube" or "Wistia" labels** so the learner knows what kind of source they're about to open.
- **Don't fabricate URLs.** If you can't find the lesson in the index files, cite the raw file path only and note "(no canonical URL found in index)".
