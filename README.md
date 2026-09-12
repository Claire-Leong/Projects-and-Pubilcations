# PaySim Fraud Analysis

Analyzed synthetic financial transactions to identify fraud patterns and behavioral risk signals.

## Overview

This project analyzes the PaySim synthetic mobile money transaction dataset using DuckDB SQL. The goal is to identify transaction patterns associated with fraud and understand which account behaviors appear most risky.

## Dataset

- **Source:** PaySim synthetic transaction data
- **File:** `PaySim/PS_data.csv`
- **Scale:** Over 6.3 million transactions
- **Target label:** `isFraud`

## Key Findings

- Fraud is extremely rare, representing about **0.13%** of all transactions.
- Fraud is concentrated in **TRANSFER** and **CASH_OUT** transactions.
- Fraudulent transactions are strongly associated with:
  - `newbalanceOrig = 0`
  - `amount = oldbalanceOrg`
  - destination accounts with little or no prior transaction history
- The `isFlaggedFraud` indicator has **perfect precision** on the flagged cases, but extremely low recall.
- A notable number of fraudulent transactions occur at exactly **$10,000,000**, suggesting a synthetic fraud pattern in the dataset.

## Analysis Performed

- Transaction type distribution
- Fraud rate by type
- Fraud rate by time step buckets
- Origin and destination account history analysis
- Balance consistency checks
- Amount vs. balance ratio analysis
- Fraud patterns around extreme transaction amounts

## Tools Used

- DuckDB
- SQL
- PaySim dataset

## Notes

Some patterns in this dataset likely reflect the synthetic rules used to generate PaySim and may not generalize directly to real-world fraud detection.

## How to Run

Run the SQL file in DuckDB against the `PaySim/PS_data.csv` dataset:

```sql
.read paysim.duckdb.sql
```

## Summary

This analysis highlights how transaction behavior, balance depletion, and account history can reveal useful fraud-risk signals in synthetic payment data.
