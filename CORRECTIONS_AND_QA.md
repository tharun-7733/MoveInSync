# Corrections and QA notes

Updated: 12 October 2026

## Rating baseline

The authoritative saved source log, `evidence/Public_Web_Source_Log.csv`, records the Play Store page fetch at **2026-10-11 14:52:18.944 UTC**, HTTP 200, with excerpt **4.6 star / 1.15L reviews**. This is a dated snapshot, not a live value. The report's earlier 4.3/5 figure dated 10 October conflicts with that source-log observation and has not been independently reconciled. Do not state both as if they agree; use the 11 October timestamped snapshot or capture a fresh one and update all deliverables consistently.

## Failed targeted low-star collection

The all-rating collection succeeded for 1,000 unique records: 259 one-star and 33 two-star records (292 combined). Separate targeted one-star and two-star calls both failed before returning records because the code passed unsupported `filter_score`; the exception suggested `filter_score_with`. The 292 records are only the low-star subset of the all-rating sample, not an additional targeted sample. Fix the argument in the notebook, rerun both requests, and update metadata only with actual successful counts.

## Monthly theme artifact

The committed `evidence/low_star_theme_by_month.csv` had no theme-count values (only a month field/list), so it did not support a monthly-theme chart. Treat that artifact as invalid for analysis. Recompute low-star multi-label theme counts by month directly from the review-level CSV, verify totals against the rows and tagging rules, then regenerate the chart. Until that is done, do not make month-over-month theme claims.

## Tools and method

The documented workflow uses the third-party Python `google-play-scraper` package to collect public listing/review data; Python/pandas for normalization, deduplication and summary tables; keyword-based multi-label rules for provisional themes; and plotting tools for charts. Listing context and review sample are separate evidence sources. Theme tags require human audit, and technical causes require authorized internal telemetry.

## Repeatable review process

Run a weekly cycle: (1) collect and timestamp new accessible reviews and record errors; (2) deduplicate and apply provisional tags; (3) manually audit a balanced sample; (4) triage with Product, Engineering, Support and Operations; (5) link complaints to booking, GPS/ETA, notification, crash, no-show and support data; (6) assign owner, severity, acceptance test and target date to confirmed issues; (7) annotate releases and compare outcomes against a documented baseline. Conduct a monthly taxonomy/outcome review and escalate safety or financial-harm signals immediately.

## Deliverable QA status

- README relative paths to the report PDF and presentation PPTX match the repository paths.
- The report and presentation are stored in GitHub and linked from the README. Their existence/path can be checked in the repository, but binary open/render validation has not been independently completed in this correction pass.
- The report/PPT still need a final binary revision so the inconsistent 4.3/5 headline and unsupported monthly-theme visual are removed/replaced consistently. This note is explicit rather than claiming those binary edits have already been made.
