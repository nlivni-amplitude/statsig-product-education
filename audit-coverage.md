# Statsig Coverage Audit

Source content scanned:
- Docs mirror: 775 pages
- Course MDs: 3
- Lesson captions: 41
- Topic files: 15

## Concept coverage matrix

Legend:
- **Docs**  = pages in `docs.statsig.com` mirror that mention the concept
- **DocW**  = approximate word count of doc paragraphs mentioning it
- **Cour**  = course MD files that mention it
- **Caps**  = caption files that mention it
- **LOs**   = topic LOs that mention it
- **LearnW**= total words of learning content (courses + captions + topic LO bodies)
- **Gap**   = DocW / LearnW. >5 = docs much deeper than our content. `none` = no learning content at all

| Concept | Docs | DocW | Cour | Caps | LOs | LearnW | Gap |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| Statsig CLI | 375 | 15,555 | 2 | 0 | 0 | 110 | **141.41** |
| Lifecycle analysis | 51 | 4,070 | 1 | 0 | 0 | 93 | **43.76** |
| Web Analytics / autocapture | 200 | 4,065 | 0 | 0 | 1 | 229 | **17.75** |
| Multiple comparisons / Bonferroni / BH | 40 | 13,874 | 0 | 0 | 2 | 877 | **15.82** |
| Target Apps | 358 | 5,384 | 1 | 0 | 2 | 401 | **13.43** |
| Local Metrics | 32 | 3,198 | 0 | 0 | 1 | 263 | **12.16** |
| Release Pipeline | 460 | 2,651 | 0 | 0 | 1 | 262 | **10.12** |
| Stratified sampling | 56 | 2,680 | 0 | 0 | 1 | 361 | **7.42** |
| CUPED variance reduction | 56 | 13,329 | 1 | 0 | 6 | 2,241 | **5.95** |
| Multi-Arm Bandits / Autotune | 411 | 9,880 | 0 | 1 | 2 | 1,695 | **5.83** |
| Pulse / Scorecard | 251 | 43,479 | 2 | 5 | 15 | 8,872 | 4.9 |
| Bayesian analysis | 51 | 7,773 | 0 | 1 | 3 | 1,602 | 4.85 |
| Dynamic Configs | 534 | 25,298 | 2 | 2 | 5 | 5,451 | 4.64 |
| Overrides | 189 | 22,664 | 2 | 5 | 1 | 5,177 | 4.38 |
| Delta method (ratio metrics) | 31 | 5,963 | 0 | 0 | 2 | 1,447 | 4.12 |
| Geo-tests | 113 | 1,068 | 0 | 0 | 1 | 269 | 3.97 |
| Layers | 634 | 36,734 | 3 | 3 | 6 | 9,776 | 3.76 |
| Holdouts | 473 | 23,038 | 1 | 4 | 2 | 6,181 | 3.73 |
| Switchback tests | 25 | 2,952 | 0 | 0 | 3 | 955 | 3.09 |
| Aggregated Impact | 18 | 1,302 | 0 | 1 | 0 | 440 | 2.96 |
| AI Evals | 193 | 1,284 | 0 | 0 | 2 | 557 | 2.31 |
| Sequential testing | 52 | 6,459 | 1 | 1 | 5 | 2,887 | 2.24 |
| Session Replay | 200 | 3,357 | 1 | 0 | 9 | 1,578 | 2.13 |
| Feature Gates | 590 | 50,907 | 3 | 14 | 10 | 25,861 | 1.97 |
| Warehouse-Native experimentation | 775 | 15,026 | 1 | 3 | 5 | 7,730 | 1.94 |
| Topline Alerts | 21 | 870 | 0 | 0 | 2 | 585 | 1.49 |
| Frequentist analysis | 43 | 3,378 | 0 | 1 | 2 | 2,364 | 1.43 |
| SSO / RBAC | 122 | 19,308 | 2 | 6 | 2 | 13,560 | 1.42 |
| Scheduled rollouts | 20 | 639 | 1 | 0 | 2 | 449 | 1.42 |
| Heterogeneous treatment effects | 22 | 2,297 | 0 | 1 | 2 | 1,707 | 1.35 |
| Retention | 55 | 11,294 | 2 | 5 | 11 | 8,668 | 1.3 |
| Power analysis / sample size | 46 | 8,180 | 0 | 2 | 9 | 7,721 | 1.06 |
| Custom DAU | 9 | 326 | 0 | 0 | 1 | 319 | 1.02 |
| Metric Drilldown | 14 | 2,779 | 2 | 3 | 3 | 2,891 | 0.96 |
| Funnels | 63 | 11,357 | 2 | 7 | 16 | 11,944 | 0.95 |
| Metric Dimensions | 7 | 689 | 0 | 1 | 1 | 780 | 0.88 |
| SCIM | 31 | 3,263 | 1 | 1 | 0 | 3,920 | 0.83 |
| CDN edge testing | 10 | 294 | 0 | 0 | 1 | 386 | 0.76 |
| Distribution Charts | 3 | 386 | 0 | 2 | 1 | 533 | 0.72 |
| Experiment Diagnostics | 114 | 6,909 | 2 | 10 | 6 | 12,671 | 0.55 |
| User journeys / Paths | 33 | 4,268 | 3 | 6 | 8 | 8,782 | 0.49 |
| Targeting rules | 18 | 2,411 | 1 | 2 | 4 | 4,893 | 0.49 |
| Segments | 54 | 7,001 | 3 | 8 | 5 | 15,444 | 0.45 |
| AA tests | 32 | 3,040 | 0 | 2 | 1 | 8,032 | 0.38 |
| Decision framework / Defer | 57 | 1,291 | 1 | 1 | 1 | 3,561 | 0.36 |
| Metric Catalog | 4 | 604 | 1 | 1 | 6 | 2,025 | 0.3 |
| Sample Ratio Mismatch (SRM) | 22 | 2,477 | 0 | 5 | 5 | 9,710 | 0.26 |
| SEO tests | 0 | 0 | 0 | 0 | 2 | 683 | 0.0 |
| Stratified metrics | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

## Bucketed action list

### B. Heavily under-taught (gap ≥ 10x) (7 concepts)

Docs go 10× deeper than our learning content. Likely candidates for a new topic LO or feature page expansion.

- **Statsig CLI** — 15,555 doc words vs. 110 learning words (gap 141.41x)
- **Lifecycle analysis** — 4,070 doc words vs. 93 learning words (gap 43.76x)
- **Web Analytics / autocapture** — 4,065 doc words vs. 229 learning words (gap 17.75x)
- **Multiple comparisons / Bonferroni / BH** — 13,874 doc words vs. 877 learning words (gap 15.82x)
- **Target Apps** — 5,384 doc words vs. 401 learning words (gap 13.43x)
- **Local Metrics** — 3,198 doc words vs. 263 learning words (gap 12.16x)
- **Release Pipeline** — 2,651 doc words vs. 262 learning words (gap 10.12x)

### C. Moderately under-taught (gap 5-10x) (3 concepts)

- **Stratified sampling** — 2,680 doc words vs. 361 learning words (gap 7.42x)
- **CUPED variance reduction** — 13,329 doc words vs. 2,241 learning words (gap 5.95x)
- **Multi-Arm Bandits / Autotune** — 9,880 doc words vs. 1,695 learning words (gap 5.83x)


### D. Statistical / methodology concepts — drill-down

Specific call-out: stats methodology is likely thin because the courses focus on product surfaces, not statistical foundations.

- **Multiple comparisons / Bonferroni / BH** — DocW 13,874, LearnW 877, gap 15.82x — covered in 2 topic LO(s)
- **Stratified sampling** — DocW 2,680, LearnW 361, gap 7.42x — covered in 1 topic LO(s)
- **CUPED variance reduction** — DocW 13,329, LearnW 2,241, gap 5.95x — covered in 6 topic LO(s)
- **Bayesian analysis** — DocW 7,773, LearnW 1,602, gap 4.85x — covered in 3 topic LO(s)
- **Delta method (ratio metrics)** — DocW 5,963, LearnW 1,447, gap 4.12x — covered in 2 topic LO(s)
- **Sequential testing** — DocW 6,459, LearnW 2,887, gap 2.24x — covered in 5 topic LO(s)
- **Frequentist analysis** — DocW 3,378, LearnW 2,364, gap 1.43x — covered in 2 topic LO(s)
- **Heterogeneous treatment effects** — DocW 2,297, LearnW 1,707, gap 1.35x — covered in 2 topic LO(s)
- **Power analysis / sample size** — DocW 8,180, LearnW 7,721, gap 1.06x — covered in 9 topic LO(s)
- **AA tests** — DocW 3,040, LearnW 8,032, gap 0.38x — covered in 1 topic LO(s)
- **Sample Ratio Mismatch (SRM)** — DocW 2,477, LearnW 9,710, gap 0.26x — covered in 5 topic LO(s)
