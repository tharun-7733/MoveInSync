# MoveInSync FDE Case Study — Review Rating Diagnosis

This repository contains the case-study report and a reproducible public-review analysis workflow for investigating the employee experience in the MoveInSync app.

## Case-study objective

Understand the current Play Store rating context, identify recurring problems reported in public reviews, recommend which issues to investigate first, and define how Product, Engineering, Support, and Operations can validate fixes.

The analysis separates:
- **Listing-level context:** the Play Store's displayed rating and total ratings, when successfully retrieved.
- **Collected review sample:** records actually returned by the public review collector.
- **Root-cause hypotheses:** potential explanations that require validation against authorized internal data.

## Repository structure

```text
moveinsync-fde-case-study/
├── README.md
|–– MoveInSync_case_study_PPT.pptx
├── report/
│   └── MoveInSync_FDE_Case_Study_Final_Updated.pdf
├── evidence/
│   └── Public_Web_Source_Log.csv
├── notebooks/
│   └── MoveInSync_Review_Collection_and_Analysis.ipynb
├── figures/
│   ├── low_star_theme_counts.png
│   └── monthly_review_counts_sample.png
└── data/
    ├── README.md
    ├── MoveInSync_Public_Reviews_Combined.csv
    ├── collection_metadata.json
    ├── Findings_Summary.json
    ├── low_star_theme_by_month.csv
    └── Manual_Review_Audit_Template.csv
```

Adjust filenames and folders to match the files actually committed. Do not include generated files that have not been checked.

## Recorded sample

The saved collection metadata records:
- 1,000 unique review records.
- 640 five-star, 259 one-star, 42 four-star, 33 two-star, and 26 three-star reviews.
- 292 one- or two-star reviews in this sample.
- Collection run: 11 October 2026 (UTC).

These figures describe this specific recent accessible-review sample only. They are not estimates of all MoveInSync employees, all trips, or all historical reviews.

**Important collection limitation:** the additional targeted one-star and two-star requests failed because the notebook used an unsupported argument name (`filter_score`). The installed package's error suggested `filter_score_with`. Therefore, the 292 low-star reviews came from the all-rating sample; the additional targeted low-star sample was not collected in that run.

The saved listing metadata did not contain the displayed Play Store score, total ratings, or update date. Verify those values from the listing or rerun the listing query successfully before stating them as current facts.

## Methodology

1. Query public Google Play listing metadata for package `com.moveinsync.ets`, using the India storefront and English locale.
2. Request up to 1,000 newest accessible reviews across all star ratings.
3. Attempt additional one-star and two-star retrieval for focused diagnosis.
4. Normalize review dates and ratings, deduplicate by review ID (with a fallback fingerprint), and export the combined CSV.
5. Apply transparent keyword-based, multi-label theme rules.
6. Generate rating distribution, low-star theme and monthly-count charts.
7. Fetch selected public MoveInSync Help Center pages and save the URL, retrieval status and text excerpt.
8. Export a manual-audit template so a human can check automated theme labels.

The notebook uses the third-party `google-play-scraper` package, not an official Google Play reviews API. Access and package behaviour can change. The collected sample is a convenience sample of accessible recent reviews, not a representative probability sample of all historical reviews.

## Main signals and interpretation

The rule-based theme chart shows `other_unclear` as the largest category, followed by driver/vehicle operations and booking/scheduling. Crash/performance/network and GPS/ETA also appear in the sample.

These are **investigation leads, not confirmed root causes**. The large `other_unclear` category should be manually reviewed and the taxonomy refined. Theme counts are multi-label, so a single review can count toward more than one theme.

Monthly counts are affected by source coverage and the collection window. October 2026 is incomplete in the recorded data. Counts are not normalized by trip volume, active users or total reviews and should not be interpreted as evidence that service quality rose or fell in a particular month.

## How to run

1. Open `notebooks/MoveInSync_Review_Collection_and_Analysis.ipynb` in [Google Colab](https://colab.research.google.com/).
2. Choose **Runtime → Run all**.
3. Review the listing snapshot, collection logs and source log.
4. Check the actual CSV row count, rating values, date range, duplicates and source URLs.
5. Manually audit a sample of theme labels before using findings in the report.
6. Regenerate charts and report values from the current run.

Before rerunning, fix the targeted rating filter to use the parameter supported by the installed `google-play-scraper` version (the recorded error suggested `filter_score_with`). Test that section and confirm returned star ratings before treating the targeted sample as successful.

## Recommended next steps

1. Verify the current listing-level rating and total ratings count.
2. Audit 50–100 reviews across ratings, dates and theme labels.
3. Discuss reported cases with Product, Support and Operations.
4. Validate hypotheses against authorized booking-state events, GPS/ETA timestamps, notification logs, support cases and no-show dispute outcomes.
5. Prioritize confirmed high-impact issues; do not rank solely by raw review-theme count.
6. Define baselines and owners for booking mismatch, stale location, ETA error, notification latency, substantiated false no-show rate, crash-free sessions and support contacts.
7. Ship a focused fix with acceptance tests and a safe rollout, then compare results with the baseline.

## Limitations and responsible use

- Public reviews are self-selected and may not represent the overall user population.
- Keyword tags can be inaccurate and must be manually checked.
- Public reviews and Help Center pages cannot establish internal root causes.
- Review counts are not normalized by trips or active users.
- Do not claim the additional low-star collection succeeded in the recorded run.
- Do not claim the listing score was captured in the recorded metadata.
- Keep reviewer information to the minimum necessary; do not commit unnecessary personal details, credentials or data you are not authorized to share.
- Check applicable platform terms and organizational requirements before collecting or republishing public content.

The goal is a repeatable feedback-to-action process—not a promise of a rating increase without validated evidence.
