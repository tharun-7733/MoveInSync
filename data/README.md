# Data directory — MoveInSync review analysis

This folder contains collection metadata and a compact summary. The primary report dataset and source log are in evidence/; the notebook is notebook/Data_Collection_and_EDA.ipynb.

## Critical scope distinction

The report and presentation use the committed evidence/MoveInSync_Public_Reviews_Combined.csv, containing **1,000 unique records**: 1 star 259, 2 stars 33, 3 stars 26, 4 stars 42 and 5 stars 640. The 292 one- or two-star records are a subset of that file.

The current data/collection_metadata.json and data/Findings_Summary.json report a later run with 1,167 unique records and successful targeted one- and two-star requests. Those later-run results have not been exported into the committed primary CSV and are not used by the current report/PPT charts. Do not combine these totals. To use the later run, export its complete review-level CSV and regenerate every dependent table, chart, report and presentation together.

The source log separately records a Play Store listing snapshot of 4.6 stars and 1.15 lakh ratings at 2026-10-11 14:52:18.944 UTC. It is a dated observation, not a live value. The listing rating is not directly comparable to the mean rating of a recent review sample.

## Reproduce and validate

1. Open the notebook and confirm which run is being reproduced and its output directory.
2. Inspect request errors, row counts, date ranges, rating values, missing fields and deduplication.
3. Regenerate theme aggregations from the exact review-level CSV used in the report.
4. Check chart totals against source tables and manually audit a balanced sample of provisional theme labels.
5. Keep the PDF, PPT, charts, CSV and metadata aligned to one declared analysis dataset.

## Interpretation and privacy

The primary sample is a convenience sample of accessible recent reviews, not a representative historical sample. Theme tags are keyword-based, multi-label suggestions; public complaints do not prove technical root causes. Monthly review counts are not complaint rates without a denominator such as trips or active users. Minimize personal information and check applicable platform terms before sharing collected data.