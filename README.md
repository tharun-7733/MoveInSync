# MoveInSync FDE Case Study

**Objective:** Diagnose public employee-app feedback, identify issues to validate, and recommend a measurable reliability-first plan.

> **Evidence-status note (12 October 2026):** The source log contains a Play Store listing snapshot of **4.6 stars and 1.15 lakh reviews captured on 11 October 2026 at 14:52:18 UTC**. This is a dated snapshot, not a live rating. The earlier 4.3/5 figure from 10 October conflicted with this source-log snapshot and was replaced in the corrected local PDF/PPT files with the dated 4.6-star baseline. The repository binaries must still be replaced with the corrected versions linked in the submission handoff.

## Start here

- **[Case-study report (PDF)](report/MoveInSync_Case_Study.pdf)**
- **[Case-study presentation (PPTX)](MoveInSync_case_study_PPT.pptx)**
- [Review collection and EDA notebook](notebook/Data_Collection_and_EDA.ipynb)
- [Collected public reviews (CSV)](evidence/MoveInSync_Public_Reviews_Combined.csv)
- [Public source log (CSV)](evidence/Public_Web_Source_Log.csv)
- [Manual review audit template (CSV)](evidence/Manual_Review_Audit_Template.csv)
- [Collection metadata (JSON)](data/collection_metadata.json)
- [Findings summary (JSON)](data/Findings_Summary.json)
- [Data documentation and limitations](data/README.md)
- [Corrections and reproducibility notes](CORRECTIONS_AND_QA.md)

## Evidence at a glance

The saved review CSV contains **1,000 unique review records**, collected on **11 October 2026 (UTC)** from accessible recent reviews.

| Rating | Records | Share of collected sample |
|---|---:|---:|
| 5 stars | 640 | 64.0% |
| 4 stars | 42 | 4.2% |
| 3 stars | 26 | 2.6% |
| 2 stars | 33 | 3.3% |
| 1 star | 259 | 25.9% |
| **Total** | **1,000** | **100%** |

The 292 one- or two-star reviews are a subset of the all-rating sample. **They are not the result of a successful targeted low-star pull.** Separate targeted requests for one- and two-star reviews failed: the scraper call used unsupported argument `filter_score`; the error suggested `filter_score_with`. Each targeted request returned zero records.

The Play Store listing source log records **4.6 stars / 1.15 lakh reviews**, fetched on **11 October 2026 at 14:52:18 UTC**. These listing values were not captured in `Findings_Summary.json` and must be cited to the source log, not described as live or as fields independently confirmed by the review collector.

## Methodology and tools

1. Capture the public Google Play listing for package `com.moveinsync.ets` using India (`in`) and English (`en`) settings; save URL, fetch time, status and excerpt.
2. Collect up to 1,000 accessible recent reviews across all ratings with the third-party `google-play-scraper` Python package.
3. Normalize fields, deduplicate, inspect rating/date distributions, and preserve collection metadata and errors.
4. Apply keyword-based multi-label theme tags. Treat them as provisional; one review may receive multiple labels.
5. Use Python/pandas and plotting libraries in the linked notebook to analyze and visualize the collected sample. Use the manual audit template to check tag quality.
6. Validate any proposed root cause against authorized internal booking, location/ETA, notification, crash, no-show and support data before assigning engineering work.

This is not an official Google Play API integration. Package behavior and public access can change. See the notebook and metadata for reproducibility details.

## Findings: hypotheses, not proven causes

Rule-based theme labels suggest investigation areas including driver/vehicle operations, booking/scheduling, crash/performance/network and GPS/ETA. The `other_unclear` label is large and signals the need for manual audit. Public review text cannot establish prevalence, technical cause or contribution to the overall Play Store score.

**Monthly theme table regenerated:** `evidence/low_star_theme_by_month.csv` now contains 50 month × theme rows for June–October 2026, computed from the 292 one- or two-star records in the saved review CSV using the existing rule-based multi-label tags. Counts are review-theme assignments, so one review can contribute to multiple themes. October is partial. The monthly theme chart has now been regenerated from the same review CSV and visually checked in the corrected local PDF/PPT deliverables. The repository PDF/PPT files still need to be replaced with those corrected binaries before submission. Monthly review counts are not complaint rates without denominators such as trips or active users.

## Recommended next steps

1. Reconfirm the dated listing baseline and keep the exact capture time.
2. Manually audit a balanced sample across star ratings, dates and predicted themes.
3. Validate cases with authorized product and operations telemetry.
4. Prioritize by impact, verified frequency and diagnosis confidence, with safety/financial consequences as overrides.
5. Ship a small, high-confidence fix with regression tests, rollout guardrails and rollback criteria.

Candidate metrics: booking mismatch rate, substantiated false no-show rate, location freshness, ETA error, critical-notification latency, crash-free sessions and support-contact rate. Set numeric targets only after the baseline is measured.

## Recurring review-to-action process

- **Weekly intake:** collect new accessible reviews, record collection time and failures, deduplicate, and tag provisionally.
- **Weekly audit/triage:** manually audit a sample; review themes with Product, Engineering, Support and Operations; connect reported cases to authorized telemetry.
- **Prioritized action log:** each confirmed issue gets severity, evidence/confidence, owner, acceptance test, due date and status.
- **Release follow-up:** annotate releases and compare relevant operational metrics and low-star share with a documented baseline.
- **Monthly review:** revisit taxonomy quality, recurring issues, fix outcomes and unresolved hypotheses. Escalate safety or financial-harm reports immediately rather than waiting for the weekly cycle.

## Limitations and responsible use

- Public reviews are self-selected and not representative of all employees or trips.
- The 1,000 records are a convenience sample of recent accessible reviews, not the full historical corpus.
- Targeted one- and two-star requests failed in the recorded run.
- Keyword labels require human validation and can misclassify text.
- Theme tags are provisional, multi-label and require manual audit. The monthly theme CSV has been regenerated; theme assignments are not mutually exclusive review counts.
- The listing score and review count are dated source-log observations, not live values.
- Minimize reviewer personal data and check applicable platform terms before collecting or republishing content.

**Goal:** establish a repeatable feedback-to-action process—not promise a rating increase without validated evidence.
