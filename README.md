# Retail ETL Data Cleaning Pipeline

A Python-based data cleaning and extraction pipeline designed to transform raw, structurally compromised retail CSV files into clean datasets ready for relational database engines or analytics.

## Technical Highlights & Features
- **Dynamic Structural Adaptability:** Built resilient schema mappings targeting headers by data matrix positions, eliminating explicit `KeyError` restrictions.
- **Relational Integrity Mapping:** Handled string splits for unformatted description fields with fallbacks to avoid text length boundary exceptions.
- **Type Safety Realignment:** Evaluated dataset schemas to convert mixed floating numbers down to analytical standard integers and text elements.
- **Relative Path Environment Syncing:** Implemented `os.path` file-loading boundaries to guarantee execution compatibility across Linux, Mac, and Windows deployment setups.

## Pipeline Architecture & Transformations
1. **Products Dataset:** Imputes missing primary keys using sequential ranges, isolates product taxonomy through tokenized string splits, and eliminates regional naming variations (`Gray` vs `Grey`).
2. **Shipping Dataset:** Standardizes missing category fields with a default business fallback (`Expedited`) and enforces data format uniformity on unique order tags.
3. **Stores Dataset:** Automatically purges operational records that do not contain valid structural identifiers.
4. **Transactions Dataset:** Identifies and drops exact matching data duplicates while converting time elements into discrete categorical string entities.

## Execution
Ensure you maintain your source datasets within a local directory named `./data/`. Run the module using the terminal wrapper command:
```bash
python data_cleaning.py