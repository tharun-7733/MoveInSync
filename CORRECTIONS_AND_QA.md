# Corrections and QA notes

Updated: 12 October 2026

## Rating baseline

The source log, `evidence/Public_Web_Source_Log.csv`, records the Play Store page fetch at **2026-10-11 14:52:18.944 UTC**, HTTP 200, with excerpt **4.6 stars / 1.15L reviews**. This is a dated snapshot, not a live value. The report's earlier 4.3/5 figure dated 10 October conflicted with the source-log observation. The PDF and PPT have not yet been revised together. Use the dated 4.6-star baseline and timestamp in both, then verify both exports before submission.

## Failed targeted low-star collection

The all-rating collection returned 1,000 unique records: 259 one-star and 33 two-star records (292 combined). Separate targeted one-star and two-star requests both failed before returning records because the code passed unsupported `filter_score`; the exception suggested `filter_score_with`. The 292 records are only the low-star subset of the all-rating sample, not an additional targeted sample. This failure is documented in README and collection metadata. The notebook still needs the argument corrected and the targeted requests rerun if an additional low-star sample is required.

## Monthly theme table and chart

The original `evidence/low_star_theme_by_month.csv` contained no counts. It has now been regenerated from the 1,000-row review CSV: low-star records (ratings 1–2) are grouped by `review_month` and split by existing semicolon-separated rule-based theme tags. The CSV now contains 50 rows (5 months × 10 theme labels), including zero counts where a theme was absent. Counts are multi-label assignments, not unique reviews per month, and October is partial. The existing chart has **not** been regenerated/visually checked against this corrected CSV, so the old chart must not be treated as validated until rebuilt.

## Tools and method

The workflow uses the third-party Python `google-play-scraper` package for public listing/review data; Python/pandas for normalization, deduplication and aggregation; keyword-based multi-label rules for provisional themes; and plotting tools for charts. Listing context and the review sample are distinct evidence sources. Theme tags require human audit, and technical causes require authorized internal telemetry.

## Repeatable review process

Run a weekly cycle: (1) collect and timestamp accessible reviews and record errors; (2) deduplicate and apply provisional tags; (3) manually audit a balanced sample; (4) triage with Product, Engineering, Support and Operations; (5) link complaints to booking, GPS/ETA, notification, crash, no-show and support data; (6) assign owner, severity, acceptance test and due date to confirmed issues; (7) annotate releases and compare outcomes against a documented baseline. Conduct a monthly taxonomy/outcome review and escalate safety or financial-harm reports immediately.

## Deliverable QA status

- README relative paths point to existing repository paths for the PDF, PPTX, notebook, CSVs and metadata.
- The PDF and PPTX files are present at the README-linked paths. I have not independently rendered/open-tested these binary files in this correction pass, so their internal rendering is not certified.
- The README and data documentation have been corrected, and a separate correction/QA note has been added.
- Before submission, revise the PDF and PPT themselves to remove/reconcile the 4.3/5 baseline, update the monthly-theme chart from the corrected CSV, and ensure the methodology/recurring workflow appears in both deliverables.
