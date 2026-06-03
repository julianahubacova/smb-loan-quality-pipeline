# Data Mapping Document / Document de correspondance des données

## Overview / Aperçu

This document describes how each field transforms as it flows through the medallion pipeline layers (Bronze → Silver → Gold).

---

## Table: loan_applications

| Field | Source (Raw CSV) | Bronze | Silver | Gold (province) | Gold (industry) | Transformation Notes |
|---|---|---|---|---|---|---|
| application_id | application_id | application_id | application_id | — | — | No transformation |
| company_name | company_name | company_name | company_name | — | — | No transformation |
| province | province | province | province (uppercased, trimmed) | province (group by) | — | `trim(upper())` applied in Silver |
| industry_sector | industry_sector | industry_sector | industry_sector | — | industry_sector (group by) | No transformation |
| loan_amount | loan_amount | loan_amount (string) | loan_amount (decimal 15,2) | avg_loan_amount, total_loan_volume | avg_loan_amount | Cast to decimal in Silver, aggregated in Gold |
| loan_purpose | loan_purpose | loan_purpose | loan_purpose | — | — | No transformation |
| application_date | application_date | application_date (string) | application_date (date) | — | — | Cast to date format `yyyy-MM-dd` in Silver |
| employee_count | employee_count | employee_count (long) | employee_count (integer) | — | — | Cast to integer in Silver |
| years_in_business | years_in_business | years_in_business (long) | years_in_business (integer) | — | — | Cast to integer in Silver |
| annual_revenue | annual_revenue | annual_revenue (long) | annual_revenue (long) | — | — | No transformation |
| credit_score | credit_score | credit_score (double) | credit_score (integer) | — | avg_credit_score | Cast to integer in Silver, aggregated in Gold |
| status | status | status | status (trimmed) | approved, rejected, under_review | — | Split into separate count columns in Gold |

---

## Metadata Fields Added in Pipeline

| Field | Added At | Description |
|---|---|---|
| _ingested_at | Bronze | Timestamp when record was ingested |
| _source_file | Bronze | Name of the source file |
| _layer | Bronze/Silver/Gold | Which layer the record belongs to |

---

## Data Quality Issues Identified

| Field | Issue | Layer Detected | Resolution |
|---|---|---|---|
| loan_amount | Null value in 1 record (LN-0013) | Silver (DQ check) | Flagged in dq_results table |
| credit_score | Null value in 1 record (LN-0015) | Silver (DQ check) | Flagged in dq_results table |

---

## Pipeline Execution Order

1. `01_medallion_pipeline` — Ingests raw CSV, builds Bronze, Silver, Gold layers
2. `02_data_quality` — Runs DQ checks against Silver layer, logs results to `dq_results` table