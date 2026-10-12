# MoveInSync FDE Case Study

**Objective:** Diagnose public employee-app feedback, identify issues to validate, and recommend a measurable reliability-first plan.

## Start here

- [Case-study report (PDF)](report/MoveInSync_Case_Study.pdf)
- [Case-study presentation (PPTX)](MoveInSync_case_study_PPT.pptx)
- [Review collection and EDA notebook](notebook/Data_Collection_and_EDA.ipynb)
- [Primary review-analysis CSV (1,000 records)](evidence/MoveInSync_Public_Reviews_Combined.csv)
- [Public source log](evidence/Public_Web_Source_Log.csv)
- [Manual review audit template](evidence/Manual_Review_Audit_Template.csv)
- [Collection metadata](data/collection_metadata.json)
- [Findings summary](data/Findings_Summary.json)
- [Data documentation](data/README.md)
- [Corrections and QA notes](CORRECTIONS_AND_QA.md)

## Evidence and dataset scope

The report and its charts use the committed primary review-analysis CSV, which contains **1,000 unique records**. Rating counts: 5-star 640, 4-star 42, 3-star 26, 2-star 33 and 1-star 259. Thus 292 records (29.2%) in this analysis CSV are one- or two-star reviews.

**Important artifact boundary:** data/collection_metadata.json and data/Findings_Summary.json describe a later collection run that reports 1,167 unique records, including successful targeted one- and two-star requests. Those later-run counts are **not represented in the committed 1,000-row primary CSV and are not the dataset used for the report/PPT charts**. Do not combine those counts or describe the report as based on 1,167 reviews. To use the later run, export its complete review-level CSV, regenerate every dependent table/chart, and replace the report/PPT together.

The public listing source log records **4.6 stars and 1.15 lakh ratings**, captured on **11 October 2026 at 14:52:18.944 UTC**. This is a dated snapshot, not a live value. The listing rating and the mean of a recent review sample describe different populations; their difference does not establish that the overall rating is declining.

## Methodology

1. Capture public Google Play listing context for package com.moveinsync.ets, India storefront, English locale; retain URL, timestamp, status and excerpt.
2. Collect up to 1,000 accessible recent reviews across all ratings for the primary analysis.
3. Normalize fields, deduplicate, inspect rating/date distributions, and preserve collection metadata.
4. Apply provisional keyword-based multi-label theme tags. One review may receive multiple labels; manually audit before treating themes as findings.
5. Analyze and plot the committed 1,000-row primary CSV using the notebook. Regenerate quantitative charts from this exact file.
6. Validate proposed root causes against authorized booking, trip-state, GPS/ETA, notification, crash, no-show and support data before assigning engineering work.

This is not an official Google Play API integration. Third-party package behavior and public access can change.

## Findings: hypotheses, not proven causes

Rule-based theme labels suggest investigation areas including driver/vehicle operations, booking/scheduling, crash/performance/network and GPS/ETA. The other_unclear label is large and signals the need for manual audit. Public review text cannot establish technical cause, prevalence across all trips, or contribution to the overall Play Store score.

Monthly theme counts are multi-label assignments, not mutually exclusive review counts or incident rates. October is partial. Review volume must not be presented as a complaint rate without denominators such as trips or active users.

## Recommended next steps

1. Reconfirm the dated listing baseline and retain its exact capture time.
2. Manually audit a balanced sample across star ratings, dates and predicted themes.
3. Validate cases with authorized product and operations telemetry.
4. Prioritize by impact, verified frequency and diagnosis confidence; safety/financial consequences override.
5. Ship a small, high-confidence fix with regression tests, rollout guardrails and rollback criteria.

Candidate metrics: booking mismatch rate, substantiated false no-show rate, location freshness, ETA error, critical-notification latency, crash-free sessions and support-contact rate. Set numeric targets only after measuring the baseline.

## Repeatable review-to-action process

- Weekly intake: collect and timestamp accessible reviews, record errors, deduplicate and tag provisionally.
- Weekly audit/triage: manually audit a sample; review themes with Product, Engineering, Support and Operations; connect reported cases to authorized telemetry.
- Prioritized action log: each confirmed issue gets severity, evidence/confidence, owner, acceptance test, due date and status.
- Release follow-up: annotate releases and compare relevant operational metrics and low-star share with a documented baseline.
- Monthly review: revisit taxonomy quality, recurring issues, fix outcomes and unresolved hypotheses. Escalate safety or financial-harm reports immediately.

## Limitations and responsible use

Public reviews are self-selected and not representative of all employees or trips. The primary 1,000 records are a convenience sample of accessible recent reviews, not the full historical corpus. Theme tags are keyword-based, multi-label suggestions and require human validation. Monthly review counts are not normalized by trips or active users. Public pages cannot verify internal root causes. Minimize reviewer personal data and check applicable platform terms before collecting or republishing content.

**Goal:** establish a repeatable feedback-to-action process—not promise a rating increase without validated evidence.