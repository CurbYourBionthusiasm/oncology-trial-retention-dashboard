# Oncology Trial Analytics: Retention & Safety Signaling

This repository contains an end-to-end data pipeline and Power BI dashboard built to monitor patient retention and adverse events (AEs) in Phase III clinical trials.

## The Problem
Patient attrition (dropouts) and severe drug toxicity are major bottlenecks in oncology trials. When patients leave a study early, it compromises statistical power and costs sponsors millions. I built this project to provide a clear analytics solution that tracks *who* is dropping out, *when*, and *if* it correlates with severe adverse events.

## Data Source & Scope
* **Source:** Project Data Sphere (PDS)
* **Trial:** Phase III NSCLC (Non-Small Cell Lung Cancer) by Eli Lilly.
* **Clinical Domains:** Patient-level data mapped roughly to standard CDISC SDTM domains (Demographics, Disposition, Adverse Events).

## Tech Stack & Architecture (ELT)
I chose an ELT approach to push the heavy transformation logic to the cloud:
* **Python & Pandas:** Parsing legacy `.sas7bdat` files and initial data discovery.
* **Apache Parquet:** Compressing raw data locally to optimize cloud ingress and storage costs.
* **Google BigQuery (SQL):** The core transformation engine. I used CTEs to denormalize 25k+ toxicity records into a single, flat `Gold` reporting table.
* **Power BI:** Serving the semantic model and interactive visualizations (with push-down compute ensuring no DAX performance bottlenecks).

## Repository Structure
```text
├── dashboards/         # Power BI exports and templates (.pbit)
├── docs/               # Data dictionaries and clinical definitions
├── notebooks/          # Local Python ingestion & profiling scripts
├── src/sql/            # BigQuery SQL transformations
└── README.md
