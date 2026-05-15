# Statsig Product Education — Content Repository

Public content corpus for the `statsig-learn` Claude skills published by the Amplitude Learning Experience Design (LXD) team.

**This repo holds reference material derived from publicly-accessible sources.** It exists so the LXD skills can `WebFetch` the content at query time rather than bundling it.

## What's here

| Directory | Contents | Source |
|---|---|---|
| `topics/` | 11 LXD-curated topic files with learning objectives + canonical answers | LXD synthesis of public Statsig content |
| `corpus/courses/` | 3 Statsig Academy course MDs | [academy.amplitude.com](https://academy.amplitude.com/statsig-101) |
| `corpus/captions/` | 41 lesson video captions | Publicly-streamed Wistia videos on academy.amplitude.com |
| `corpus/captions-combined/` | 3 combined-by-course caption files (one per Statsig U course) | Same as `captions/`, just grouped |
| `indexes/` | Cross-reference indexes: Academy course map, Wistia, YouTube, docs sitemaps, feature comparison inventory | Generated from public sources |

## Sources (all public)

- **Statsig Academy courses** — [academy.amplitude.com](https://academy.amplitude.com)
- **Lesson video captions** — derived from publicly-streamed Wistia videos
- **Statsig docs sitemap** — [docs.statsig.com](https://docs.statsig.com/sitemap.xml)
- **Amplitude docs sitemap** — [amplitude.com/docs](https://amplitude.com/docs/sitemap-docs.xml)
- **Feature comparison inventory** — LXD-curated mapping of features between the two products

## How the LXD skills consume this

Skills published in [`amplitude/learning-experience-internal`](https://github.com/amplitude/learning-experience-internal) reference these files via GitHub Pages URLs (`https://nlivni-amplitude.github.io/statsig-product-education/...`) at query time. That way:

- Skills are small (one `.md` file each, distributable as a Slack-friendly attachment)
- Content updates here propagate immediately on the next `WebFetch` — no plugin re-install
- The corpus stays in one place under version control

## Refresh cadence

- **Doc sitemaps** — refresh weekly via [`scripts/refresh-sitemaps.py`](https://github.com/amplitude/learning-experience-internal/blob/main/plugins/statsig-learn/scripts/refresh-sitemaps.py) in the skills repo
- **Topic files** — updated as LXD identifies content gaps or product changes
- **Course MDs and captions** — re-pulled when the source Academy courses change

## License

MIT — see [LICENSE](LICENSE).

## Maintainers

Amplitude Learning Experience Design (LXD). Contact: Nathan Livni (`nathan.livni@amplitude.com`).
