# MoveInSync FDE Case Study

A practical, evidence-led case study on improving the employee experience in the MoveInSync app. The report identifies public-review themes, proposes hypotheses to validate with internal data, and outlines a prioritized 30-day execution plan.

## Deliverables

- `report/MoveInSync_FDE_Case_Study_Tharun_Teja.pdf` — main case-study report.
- `evidence/MoveInSync_Review_Evidence_Log_Verified.csv` — public-review evidence log used to support qualitative examples.
- `notebooks/MoveInSync_Low_Rating_Reviews_Collector.ipynb` — Google Colab notebook for collecting and preparing a sample of public low-rating reviews.
- `src/collect_moveinsync_low_star_reviews.py` — standalone Python collector.
- `figures/` — charts used in the report.
- `data/` — generated analysis outputs, if collected and checked.

## Problem

Understand recurring issues reported by employees, identify which journey failures deserve investigation first, and recommend fixes that Product, Engineering, Support, and Operations can validate and execute.

## Approach

1. Review public app-store feedback and official support documentation.
2. Organize low-rating reviews into provisional issue themes such as booking/scheduling, GPS/ETA, notifications, driver/vehicle operations, performance, usability, access, and support.
3. Treat themes as signals and hypotheses—not confirmed root causes.
4. Prioritize work by employee impact, observed frequency, confidence in the diagnosis, and potential safety or financial consequences.
5. Validate hypotheses against internal booking events, trip-state changes, GPS/ETA timestamps, notification events, support tickets, and no-show disputes.
6. Propose a 30-day cycle: establish a baseline, trace incidents, implement a focused fix, roll it out safely, and measure outcomes.

## Review collection method

The notebook and script target the Google Play listing for package `com.moveinsync.ets`. They request the India storefront (`country=in`) and English locale (`lang=en`), inspect the newest accessible source frame (up to 15,000 reviews before filtering), retain written 1- or 2-star reviews, deduplicate records, and randomly sample up to 500 eligible reviews without replacement using seed `42`.

The target is **up to 500**, not a guarantee. If fewer than 500 eligible unique reviews are available, the collector writes a shortfall CSV rather than presenting it as a 500-review sample. It also writes a metadata JSON file describing the collection run. Review availability and scraper behaviour may change over time.

The output is a sample from the newest accessible records, not a representative probability sample of every historical review, every language, or every employee. The collection uses the third-party `google-play-scraper` package, not an official Google Play reviews API. Check applicable platform terms and organizational requirements before running or reusing it.

## Run the notebook

1. Open `notebooks/MoveInSync_Low_Rating_Reviews_Collector.ipynb` in [Google Colab](https://colab.research.google.com/).
2. Choose **Runtime → Run all**.
3. Wait for collection and export to finish.
4. Download the generated CSV and its matching metadata JSON.
5. Check the actual row count, rating values, dates, duplicates, and source references before using statistics in a report.

For local execution, install the dependency and run the script:

```bash
python -m pip install google-play-scraper
python src/collect_moveinsync_low_star_reviews.py
```

Run the command from the directory where you want the output files to be written. The script's output paths are relative to the current working directory.

## Outputs and data handling

Depending on the number of eligible reviews, the collector creates either:

- `MoveInSync_500_Low_Rating_Reviews.csv` when the target sample is reached, or
- `MoveInSync_Low_Rating_Candidates_NOT_500.csv` when fewer than 500 eligible records are available,

along with `MoveInSync_500_Low_Rating_Reviews_metadata.json`.

The collector intentionally excludes reviewer names/profile URLs and full review text from its CSV output. Review text is used transiently for eligibility, deduplication fallback, and rule-based theme tagging. Keep the metadata JSON with the CSV so the collection window and counts remain traceable.

## How to interpret the results

- Counts describe the collected sample, not the whole app user base.
- One- and two-star reviewers are self-selected; their experiences may not represent all journeys.
- Rule-based tags can be wrong or overlap. Audit a sample manually before making decisions.
- Review counts by month are not normalized by trip volume, total active users, or total reviews.
- Public evidence alone cannot prove the underlying technical or operational cause.
- Do not claim a dataset size or chart statistic unless it matches the actual exported data.

## Recommended validation metrics

- Booking mismatch rate between employee intent and persisted booking.
- Stale-location rate and ETA error at defined journey checkpoints.
- Notification latency from event trigger to the available delivery milestone.
- Substantiated false no-show rate after audit.
- Crash-free sessions and support contacts by app version.
- One- and two-star review share, interpreted alongside total reviews and trip volume.

Define each metric, data source, time window, exclusions, owner, and action threshold before comparing results. Set numerical targets only after a reliable baseline exists.

## Repository structure

```text
moveinsync-fde-case-study/
├── README.md
├── report/
│   └── MoveInSync_FDE_Case_Study_Tharun_Teja.pdf
├── evidence/
│   └── MoveInSync_Review_Evidence_Log_Verified.csv
├── notebooks/
│   └── MoveInSync_Low_Rating_Reviews_Collector.ipynb
├── src/
│   └── collect_moveinsync_low_star_reviews.py
├── figures/
│   ├── common_complaint_themes.png
│   ├── monthly_and_seasonal_trends.png
│   └── ratings_and_character_counts.png
└── data/
    └── README.md
```

Only add generated data after checking that it is valid and that its values match the report. Do not commit secrets, personal information, or unnecessary reviewer identifiers.

## Limitations

This is an external-evidence case study, not an internal production audit. The hypotheses and proposed priorities must be validated with authorized, privacy-safe internal data before implementation. The goal is to make the process repeatable and the next decision clearer—not to promise a rating increase without evidence.
