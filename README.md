# MoveInSync FDE Case Study

**Objective:** Investigate employee experiences reported in MoveInSync's public Play Store reviews, identify issues worth validating, and recommend a measurable plan for improving reliability and satisfaction.

This repository contains the case-study report, presentation, review evidence, collection metadata, source log, charts, and analysis notebook.

## Start here

- **[Case-study report (PDF)](report/MoveInSync_Case_Study.pdf)**
- **[Case-study presentation (PPTX)](MoveInSync_case_study_PPT.pptx)**
- [Review collection and EDA notebook](notebook/Data_Collection_and_EDA.ipynb)
- [Collected public reviews (CSV)](evidence/MoveInSync_Public_Reviews_Combined.csv)
- [Public source log (CSV)](evidence/Public_Web_Source_Log.csv)
- [Manual review audit template (CSV)](evidence/Manual_Review_Audit_Template.csv)
- [Collection metadata (JSON)](data/collection_metadata.json)
- [Findings summary (JSON)](data/Findings_Summary.json)
- [Data documentation](data/README.md)

## What this analysis covers

The workflow separates three kinds of evidence:

- **Listing-level context:** rating and total-review figures visible on the Play Store listing at a specific time.
- **Collected sample:** reviews actually returned by the scraper.
- **Root-cause hypotheses:** possible explanations that require validation with authorized internal product and operations data.

## Repository structure

```text
.
├── README.md
├── MoveInSync_case_study_PPT.pptx
├── report/
│   └── MoveInSync_Case_Study.pdf
├── notebook/
│   └── Data_Collection_and_EDA.ipynb
├── evidence/
│   ├── MoveInSync_Public_Reviews_Combined.csv
│   ├── Public_Web_Source_Log.csv
│   ├── Manual_Review_Audit_Template.csv
│   └── low_star_theme_by_month.csv
├── data/
│   ├── README.md
│   ├── collection_metadata.json
│   └── Findings_Summary.json
└── figures/
    ├── barplot.png
    ├── graph_analysis.png
    ├── low_star_theme_counts.png
    └── monthly_review_counts_sample.png
```

## Collected sample

The saved review CSV contains **1,000 unique review records** from a collection run on **11 October 2026 (UTC)**.

| Rating | Reviews | Share of sample |
|---|---:|---:|
| 5 stars | 640 | 64.0% |
| 4 stars | 42 | 4.2% |
| 3 stars | 26 | 2.6% |
| 2 stars | 33 | 3.3% |
| 1 star | 259 | 25.9% |
| **Total** | **1,000** | **100%** |

There are **292 one- or two-star reviews** in this collected sample. These came from the all-rating collection. The separate targeted requests for additional one- and two-star reviews failed because the scraper call used an unsupported parameter (`filter_score`; the error indicated `filter_score_with`). Do not describe the targeted low-star collection as successful.

The source log records a Play Store listing snapshot showing **4.6 stars and 1.15 lakh reviews on 11 October 2026**. Treat this as a dated snapshot, not a live rating. The saved listing metadata did not independently capture those listing-level values.

## Methodology

1. Retrieve public Play Store listing context and accessible reviews for package `com.moveinsync.ets`, using the India storefront and English locale.
2. Request up to 1,000 newest accessible reviews across all ratings.
3. Normalize review dates and ratings and deduplicate collected records.
4. Apply keyword-based, multi-label theme tags.
5. Generate rating, theme and monthly summary charts.
6. Save the URLs and retrieval details for selected public sources.
7. Provide a manual-audit template for checking whether assigned themes match the text.

The collection used the third-party `google-play-scraper` package, not an official Google Play reviews API. Package behavior and public access may change. To reproduce the work, open the linked notebook, inspect its collection limitations, and run the steps after verifying the scraper parameters for the installed package version.

## Findings: signals, not proven causes

The rule-based theme summaries show `other_unclear` as the largest category, followed by driver/vehicle operations and booking/scheduling. Crash/performance/network and GPS/ETA themes also appear.

These categories are **investigation leads, not confirmed root causes**. A review can receive multiple theme labels, and keyword rules can misclassify text. The large `other_unclear` category makes manual review and refinement of the theme taxonomy important.

Monthly counts are not normalized by trip volume, active users or total reviews. October 2026 is incomplete in the recorded data, so the charts should not be interpreted as definitive changes in service quality over time.

## Recommended next steps

1. **Verify the baseline.** Recheck the listing rating and total ratings and record the date of the snapshot.
2. **Audit review labels.** Manually inspect a balanced sample across ratings, dates and predicted themes; refine the rules where needed.
3. **Validate reported cases.** Work with Product, Support and Operations to compare complaints with authorized booking-state events, GPS/ETA timestamps, notification logs, crash data and no-show dispute outcomes.
4. **Prioritize confirmed problems.** Rank by impact, frequency and confidence, not raw theme counts alone.
5. **Ship and measure a focused fix.** Define an owner, acceptance tests, rollout guardrails and rollback criteria, then compare with a documented baseline.

Candidate metrics include booking mismatch rate, stale-location incidence, ETA error, notification latency, substantiated false no-show rate, crash-free sessions and support-contact rate. Select metrics that match the problem confirmed during validation.

## Limitations and responsible use

- Public reviews are self-selected and may not represent the overall user population.
- A reviewer report does not prove the underlying technical cause.
- Keyword theme classifications need human validation.
- Monthly counts are not complaint rates without an appropriate denominator.
- The targeted additional low-star collection failed in the recorded run.
- The listing rating and review total are dated source-log observations, not live values.
- Keep reviewer information to the minimum needed, avoid committing unnecessary personal details or credentials, and check applicable platform terms before collecting or republishing public content.

**Goal:** establish a repeatable feedback-to-action process—not promise a rating increase without validated evidence.
