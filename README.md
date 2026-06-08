# Enterprise Retail ETL & Data Preprocessing Pipeline

[![Python Version](https://img.shields.io/badge/python-3.10%20%7C%203.11%20%7C%203.12-blue)](https://www.python.org)
[![Pandas](https://img.shields.io/badge/library-pandas-violet)](https://pandas.pydata.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A robust, production-ready **Extract, Transform, Load (ETL)** pipeline architected to ingest, sanitize, and normalize structurally compromised retail datasets. This framework resolves schema drift, missing relational keys, and data-type anomalies, transforming raw transactional logs into high-fidelity, analytics-ready structures optimized for downstream Data Warehouses (e.g., Snowflake, BigQuery) or BI tooling.

---

## 🛠️ Core Engineering Highlights

* **Schema Drift & Variation Resilience:** Implemented zero-dependency position-based header targeting (`columns[0]`, `columns[1]`). This shields the pipeline from upstream column renaming and eliminates volatile `KeyError` exceptions.
* **Defensive String Tokenization:** Formulated a safe, conditional string-splitting mechanism with structural fallbacks to handle variable token lengths without triggering index boundary crashes.
* **Strict Type-Safety & Standardization:** Enforced structural data integrity by normalizing mixed floating-point artifacts into discrete integers (`int`) and casting time-series fields to explicit categorical string objects (`str`).
* **Environment-Agnostic Execution:** Engineered absolute runtime portability using OS-independent filesystem pathing boundaries (`os.path`), ensuring seamless cross-platform execution (Linux/macOS/Windows).

---

## 📐 Data Architecture & Cleaning Logic

The pipeline processes four relational business datasets through a decoupled execution flow:

### 1. Inventory / Products Stream
* **Primary Key Imputation:** Programmatically calculates downstream index gaps and infuses sequential surrogates (`1, 2, 3...`) into null identifier fields.
* **Feature Extraction:** Parses and tokenizes unformatted string records into separate, discrete attributes (`type` and `colour`).
* **Lexical Standardization:** Normalizes regional string permutations (e.g., maps `Gray` to standard `Grey`) to optimize string matching for downstream analytics.

### 2. Fulfillment / Shipping Stream
* **Business Rule Imputation:** Mitigates risk from missing fields by dynamically injecting categorical fallbacks (`Expedited`) into null records.
* **Relational Integrity Alignment:** Forces composite key structures (`orderid`) to pure integers, stripping accidental float padding (`.0`).

### 3. Entity / Stores Stream
* **Null Record Pruning:** Purges operational rows missing critical structural primary keys (`store_id`) to prevent Referential Integrity failures in target databases.
* **Index Realignment:** Re-indexes the underlying structural array post-deletion to preserve sequential memory addressing.

### 4. Ledger / Transactions Stream
* **Data Deduplication:** Executes an identity-based evaluation across the feature space to drop duplicated ledger entries, ensuring data **idempotency**.
* **Dimensional Segmentation:** Isolates and casts temporal metrics (`year`, `month`, `day`) into discrete string categories to prevent math operations on date parts.

---

## 📁 Repository Structure

```text
pandas-data-preprocessing/
│
├── data/                      <-- Local Source Data Ingestion Landing Zone
│   ├── products.csv
│   ├── Shipping.csv
│   ├── Stores.csv
│   └── Transactions.csv
│
├── data_cleaning.py           <-- Modularized Functional ETL Pipeline Engine
└── README.md                  <-- Technical Pipeline Documentation

git clone [https://github.com/ihamidch/pandas-data-preprocessing.git](https://github.com/ihamidch/pandas-data-preprocessing.git)
cd pandas-data-preprocessing

python data_cleaning.py
👨‍💻 Author
 (Ihamidch) - Data Engineering & Preprocessing Architect

GitHub: @ihamidch
