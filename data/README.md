# Data directory — MoveInSync review analysis

This folder contains collection metadata and a compact summary. The review CSV, source log, manual-audit template and analysis artifacts are in `evidence/`; the notebook is `notebook/Data_Collection_and_EDA.ipynb`.

## Files

| File | Purpose |
|---|---|
| `collection_metadata.json` | Collection timestamps, request counts, errors, actual sample size and limitations. |
| `Findings_Summary.json` | Sample counts and listing-context fields returned by the review collection run. |

## Recorded collection run

The run on 11 October 2026 (UTC) produced 1,000 unique records: 1 star 259, 2 stars 33, 3 stars 26, 4 stars 42 and 5 stars 640. Thus 292 one- or two-star records occur in the all-rating sample.

The separate one-star and two-star diagnostic requests failed because the installed scraper rejected `filter_score` and suggested `filter_score_with`. Both targeted requests returned zero records. Do not describe them as successful or count them as additional records.

The listing metadata fields in `Findings_Summary.json` are null. The separately timestamped source log contains the public listing snapshot: 4.6 stars and 1.15 lakh reviews at 2026-10-11 14:52:18.944 UTC. It is a dated snapshot, not a live value.

## Reproduce and validate

1. Open `notebook/Data_Collection_and_EDA.ipynb`.
2. Check the installed `google-play-scraper` version and correct/test the targeted filter argument.
3. Rerun collection and inspect request errors before updating metadata.
4. Check deduplication, rating values, dates, missing fields and row counts.
5. Regenerate theme aggregations from the review-level CSV and check chart totals against the aggregation.
6. Manually audit a balanced selection of predicted theme labels.
7. Keep every chart aligned to a committed, reproducible table.

The current `evidence/low_star_theme_by_month.csv` did not contain actual theme counts and is not valid evidence for a monthly-theme chart. Do not use it until regenerated.

## Interpretation and privacy

The sample is a convenience sample of accessible recent reviews, not a representative historical sample. Theme tags are keyword-based, multi-label suggestions; a public complaint does not prove a technical root cause. Monthly review counts are not complaint rates without a denominator such as trips or active users. Minimize personal information and check applicable platform terms before sharing collected data.
