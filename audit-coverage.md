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
| Multiple comparisons / Bonferroni / BH | 40 | 13,874 | 0 | 0 | 2 | 383 | **36.22** |
| Delta method (ratio metrics) | 31 | 5,963 | 0 | 0 | 1 | 260 | **22.93** |
| Web Analytics / autocapture | 200 | 4,065 | 0 | 0 | 1 | 229 | **17.75** |
| Target Apps | 358 | 5,384 | 1 | 0 | 2 | 401 | **13.43** |
| Local Metrics | 32 | 3,198 | 0 | 0 | 1 | 263 | **12.16** |
| CUPED variance reduction | 56 | 13,329 | 1 | 0 | 5 | 1,099 | **12.13** |
| Release Pipeline | 460 | 2,651 | 0 | 0 | 1 | 262 | **10.12** |
| Multi-Arm Bandits / Autotune | 411 | 9,880 | 0 | 1 | 2 | 1,087 | **9.09** |
| Stratified sampling | 56 | 2,680 | 0 | 0 | 1 | 361 | **7.42** |
| Bayesian analysis | 51 | 7,773 | 0 | 1 | 3 | 1,179 | **6.59** |
| Pulse / Scorecard | 251 | 43,479 | 2 | 5 | 15 | 7,364 | **5.9** |
| Dynamic Configs | 534 | 25,298 | 2 | 2 | 5 | 5,451 | 4.64 |
| Overrides | 189 | 22,664 | 2 | 5 | 1 | 5,177 | 4.38 |
| Sequential testing | 52 | 6,459 | 1 | 1 | 3 | 1,499 | 4.31 |
| Geo-tests | 113 | 1,068 | 0 | 0 | 1 | 269 | 3.97 |
| Layers | 634 | 36,734 | 3 | 3 | 6 | 9,282 | 3.96 |
| Holdouts | 473 | 23,038 | 1 | 4 | 2 | 6,181 | 3.73 |
| Switchback tests | 25 | 2,952 | 0 | 0 | 3 | 955 | 3.09 |
| Aggregated Impact | 18 | 1,302 | 0 | 1 | 0 | 440 | 2.96 |
| Heterogeneous treatment effects | 22 | 2,297 | 0 | 1 | 1 | 951 | 2.42 |
| AI Evals | 193 | 1,284 | 0 | 0 | 2 | 557 | 2.31 |
| Session Replay | 200 | 3,357 | 1 | 0 | 9 | 1,578 | 2.13 |
| Feature Gates | 590 | 50,907 | 3 | 14 | 10 | 25,861 | 1.97 |
| Warehouse-Native experimentation | 775 | 15,026 | 1 | 3 | 5 | 7,730 | 1.94 |
| Frequentist analysis | 43 | 3,378 | 0 | 1 | 2 | 1,941 | 1.74 |
| Retention | 55 | 11,294 | 2 | 5 | 11 | 7,469 | 1.51 |
| Topline Alerts | 21 | 870 | 0 | 0 | 2 | 585 | 1.49 |
| SSO / RBAC | 122 | 19,308 | 2 | 6 | 2 | 13,560 | 1.42 |
| Scheduled rollouts | 20 | 639 | 1 | 0 | 2 | 449 | 1.42 |
| Power analysis / sample size | 46 | 8,180 | 0 | 2 | 8 | 6,150 | 1.33 |
| Custom DAU | 9 | 326 | 0 | 0 | 1 | 319 | 1.02 |
| Funnels | 63 | 11,357 | 2 | 7 | 16 | 11,558 | 0.98 |
| Metric Drilldown | 14 | 2,779 | 2 | 3 | 3 | 2,891 | 0.96 |
| Metric Dimensions | 7 | 689 | 0 | 1 | 1 | 780 | 0.88 |
| SCIM | 31 | 3,263 | 1 | 1 | 0 | 3,920 | 0.83 |
| CDN edge testing | 10 | 294 | 0 | 0 | 1 | 386 | 0.76 |
| Distribution Charts | 3 | 386 | 0 | 2 | 1 | 533 | 0.72 |
| Experiment Diagnostics | 114 | 6,909 | 2 | 10 | 5 | 11,915 | 0.58 |
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

### B. Heavily under-taught (gap ≥ 10x) (9 concepts)

Docs go 10× deeper than our learning content. Likely candidates for a new topic LO or feature page expansion.

- **Statsig CLI** — 15,555 doc words vs. 110 learning words (gap 141.41x)
- **Lifecycle analysis** — 4,070 doc words vs. 93 learning words (gap 43.76x)
- **Multiple comparisons / Bonferroni / BH** — 13,874 doc words vs. 383 learning words (gap 36.22x)
- **Delta method (ratio metrics)** — 5,963 doc words vs. 260 learning words (gap 22.93x)
- **Web Analytics / autocapture** — 4,065 doc words vs. 229 learning words (gap 17.75x)
- **Target Apps** — 5,384 doc words vs. 401 learning words (gap 13.43x)
- **Local Metrics** — 3,198 doc words vs. 263 learning words (gap 12.16x)
- **CUPED variance reduction** — 13,329 doc words vs. 1,099 learning words (gap 12.13x)
- **Release Pipeline** — 2,651 doc words vs. 262 learning words (gap 10.12x)

### C. Moderately under-taught (gap 5-10x) (4 concepts)

- **Multi-Arm Bandits / Autotune** — 9,880 doc words vs. 1,087 learning words (gap 9.09x)
- **Stratified sampling** — 2,680 doc words vs. 361 learning words (gap 7.42x)
- **Bayesian analysis** — 7,773 doc words vs. 1,179 learning words (gap 6.59x)
- **Pulse / Scorecard** — 43,479 doc words vs. 7,364 learning words (gap 5.9x)


### D. Statistical / methodology concepts — drill-down

Specific call-out: stats methodology is likely thin because the courses focus on product surfaces, not statistical foundations.

- **Multiple comparisons / Bonferroni / BH** — DocW 13,874, LearnW 383, gap 36.22x — covered in 2 topic LO(s)
- **Delta method (ratio metrics)** — DocW 5,963, LearnW 260, gap 22.93x — covered in 1 topic LO(s)
- **CUPED variance reduction** — DocW 13,329, LearnW 1,099, gap 12.13x — covered in 5 topic LO(s)
- **Stratified sampling** — DocW 2,680, LearnW 361, gap 7.42x — covered in 1 topic LO(s)
- **Bayesian analysis** — DocW 7,773, LearnW 1,179, gap 6.59x — covered in 3 topic LO(s)
- **Sequential testing** — DocW 6,459, LearnW 1,499, gap 4.31x — covered in 3 topic LO(s)
- **Heterogeneous treatment effects** — DocW 2,297, LearnW 951, gap 2.42x — covered in 1 topic LO(s)
- **Frequentist analysis** — DocW 3,378, LearnW 1,941, gap 1.74x — covered in 2 topic LO(s)
- **Power analysis / sample size** — DocW 8,180, LearnW 6,150, gap 1.33x — covered in 8 topic LO(s)
- **AA tests** — DocW 3,040, LearnW 8,032, gap 0.38x — covered in 1 topic LO(s)
- **Sample Ratio Mismatch (SRM)** — DocW 2,477, LearnW 9,710, gap 0.26x — covered in 5 topic LO(s)
