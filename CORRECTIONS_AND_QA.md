# Corrections and QA notes

Updated: 12 October 2026

## Rating baseline

The source log records the Play Store page fetch at **2026-10-11 14:52:18.944 UTC**, HTTP 200, with excerpt **4.6 stars / 1.15L reviews**. This is a dated snapshot, not a live value. The report/PPT use this timestamped baseline. The recent review sample and overall listing score describe different populations; the difference alone is not evidence of a rating decline.

## Analysis dataset boundary

The report and presentation use evidence/MoveInSync_Public_Reviews_Combined.csv, containing 1,000 unique records (640 five-star, 42 four-star, 26 three-star, 33 two-star and 259 one-star). Its 292 one-/two-star reviews are the low-star subset used in the report.

The current data/collection_metadata.json and data/Findings_Summary.json describe a later run with 1,167 unique records and successful targeted low-star requests. That later-run dataset is **not** the committed 1,000-row CSV and is **not** the basis for the current report/PPT. Do not mix those counts. If the later run is selected as the final analysis, export its full review-level CSV and regenerate all dependent charts and deliverables as a single update.

## Method and limitations

The workflow uses a third-party Google Play scraper, Python/pandas for normalization and aggregation, and keyword-based multi-label rules for provisional themes. Theme tags require human audit, and technical causes require authorized internal telemetry. Monthly theme values are multi-label assignments, not mutually exclusive review counts or incident rates; October is partial.

## Final QA checklist

- [ ] PDF and PPT linked in GitHub are the exact final versions attached to the submission.
- [ ] All quantitative charts use the committed 1,000-row primary CSV, unless the entire project has been regenerated from another declared dataset.
- [ ] Rating snapshot includes capture timestamp and is not called live.
- [ ] Report distinguishes sample statistics from listing-level rating context.
- [ ] Hypotheses are not presented as proven root causes.
- [ ] Monthly multi-label theme counts are not described as incident rates.
- [ ] Links open and the notebook documents dependencies, collection settings and limitations.

The primary CSV/report scope is now documented, but binary files must still be replaced manually in GitHub if the local final PDF/PPT differ from the repository versions.