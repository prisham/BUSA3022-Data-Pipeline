# BUSA3022-Data-Pipeline
S&amp;P 500 and FRED data ingestion, validation and storage pipeline
# BUSA3022 — Financial Data Pipeline

## 1. Project Overview

This repository contains a Python-based data pipeline developed for the BUSA3022 Business Analytics group assessment at Macquarie University.

The pipeline collects, validates and stores financial data from two sources:

- **Yahoo Finance:** S&P 500 market index (`^GSPC`).
- **Federal Reserve Economic Data (FRED):** Effective Federal Funds Rate (`DFF`).

The implementation demonstrates repeatable data ingestion, separation of raw and curated datasets, data-quality validation, error handling, logging and backup safeguards.

## 2. Technologies Used

- Python
- Google Colab
- Pandas
- yfinance
- FRED CSV download endpoint
- GitHub for version control and reproducibility

## 3. Pipeline Architecture

The pipeline follows these stages:

1. **Data ingestion:** Retrieve S&P 500 and FRED observations using Python.
2. **Raw storage:** Save downloaded datasets in `data/raw/`.
3. **Validation:** Check missing values, invalid values, duplicate dates and date ordering.
4. **Curated storage:** Save accepted records in `data/curated/`.
5. **Logging:** Record execution outcomes, API failures and data-quality issues in `logs/`.
6. **Backup and recovery:** Maintain dataset backups and SHA-256 checkpoints in `data/backups/`.
7. **Downstream handoff:** Provide validated datasets for date alignment and metric calculations in Part 2.

## 4. Repository Files

| File | Description |
|---|---|
| `BUSA3022_Data_Pipeline.ipynb` | Python pipeline notebook, validation logic and testing |
| `sp500_validated.csv` | Validated S&P 500 market observations |
| `fred_validated.csv` | Validated FRED interest-rate observations |
| `README.md` | Project documentation |

The notebook creates additional raw data, logging and backup files during execution. These generated files are not all included in the repository.

## 5. How to Run the Pipeline

1. Download or open `BUSA3022_Data_Pipeline.ipynb` in Google Colab.
2. Connect to a Python runtime.
3. Run the notebook cells in order, starting with the dependency installation.
4. Ensure the Python libraries, including `yfinance` and `pandas`, are available.
5. Execute the integrated pipeline.
6. Review the printed pipeline summary and generated CSV files.
7. Inspect quality and API failure logs for any issues.

The notebook uses publicly accessible data sources and does not require credentials for its documented download methods.

**Important:** Google Colab runtime storage is temporary. Download or persist important outputs before disconnecting.

## 6. Data Validation

The pipeline checks:

- Missing or invalid S&P 500 closing prices.
- Missing or non-numeric FRED interest-rate observations.
- Duplicate dates.
- Date ordering and relevant data types.

Records failing validation are excluded from curated outputs and recorded separately for investigation.

The pipeline also includes simulated missing-value tests to demonstrate the detection of problematic records.

## 7. Error Handling and Logging

Retry-enabled download functions help manage temporary API failures.

The pipeline records API errors, retry outcomes, execution results and data-quality issues.

An inaccessible API endpoint was used to simulate a download failure and test error logging.

Backup copies, staged saving and SHA-256 checkpoints provide additional safeguards. Recovery is best-effort and does not guarantee fully atomic updates.

## 8. Proof-of-Concept Results

The latest successful integrated pipeline run produced:

| Dataset | Valid records | Invalid records |
|---|---:|---:|
| S&P 500 | 128 | 0 |
| FRED DFF | 26,419 | 0 |

These results demonstrate successful ingestion and validation for the tested run. Record counts may change when the pipeline is executed again.

## 9. Scheduling and Repeatability

**Implemented:** The notebook supports manually repeatable execution in Google Colab.

**Proposed enhancement:** GitHub Actions could automate execution after US market close, subject to source publication delays, weekends and market holidays.

Automated scheduling and failure notifications have not been implemented in this proof of concept.

## 10. Handoff to Part 2

The validated datasets are provided to the group member responsible for data curation and metrics.

The next stage involves:

- Aligning S&P 500 trading dates with FRED observation dates.
- Handling different dataset coverage periods and missing dates.
- Calculating the required financial and macroeconomic metrics.
- Preparing transformed data for dashboard development.

The datasets should be aligned over their common relevant date range rather than assuming that every FRED observation corresponds to a market trading day.

## 11. Limitations

This is an academic proof of concept rather than a production deployment.

Current limitations include manual execution, temporary Colab storage, dependence on external data-source availability, unequal source date ranges and limited recovery testing.

Future improvements could include automated scheduling, persistent cloud storage, monitoring, notifications and more comprehensive end-to-end testing.

## 12. Academic Purpose

Developed for the BUSA3022 Business Analytics group assessment at Macquarie University, Semester 2, 2026.
