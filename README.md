# SMB Loan Quality Pipeline / Pipeline de qualité des prêts PME

## Overview / Aperçu

**EN:** An end-to-end data pipeline simulating a small business lending platform. Ingests raw loan application data, applies a medallion architecture (Bronze → Silver → Gold), runs automated data quality checks, and surfaces results in a Power BI dashboard.

**FR:** Un pipeline de données de bout en bout simulant une plateforme de prêts aux petites et moyennes entreprises. Ingère des données brutes de demandes de prêt, applique une architecture médaillon (Bronze → Argent → Or), exécute des contrôles automatisés de qualité des données et présente les résultats dans un tableau de bord Power BI.

---

## Architecture

```
Raw Source (CSV)
      ↓
  [Bronze Layer] — Raw ingestion, no transformations
      ↓
  [Silver Layer] — Cleaned, typed, deduplicated
      ↓
  [Gold Layer]   — Aggregated, business-ready
      ↓
  [Data Quality] — Completeness, freshness, consistency checks
      ↓
  [Power BI Dashboard] — DQ monitoring + business view
```

---

## Tech Stack

| Tool | Purpose |
|---|---|
| Databricks | Pipeline orchestration & transformation |
| PySpark / SQL | Data processing |
| Delta Lake | Storage format |
| Power BI | Dashboard & visualization |
| GitHub | Version control |

---

## Project Structure

```
smb-loan-quality-pipeline/
├── data/
│   ├── raw/          # Simulated raw source files
│   └── sample/       # Sample datasets for development
├── notebooks/        # Databricks notebooks
├── sql/
│   ├── bronze/       # Raw ingestion queries
│   ├── silver/       # Cleaning & transformation queries
│   └── gold/         # Aggregation queries
├── docs/             # Data dictionary, mapping docs, lineage
└── dashboard/        # Power BI screenshots & .pbix file
```

---

## Data Quality Checks

- **Completeness** — No nulls in critical fields
- **Freshness** — Data arrived within expected window
- **Consistency** — Valid ranges, valid province codes
- **Uniqueness** — No duplicate records per batch

---

## Documentation

- [Data Dictionary](docs/data_dictionary.md)
- [Data Mapping](docs/data_mapping.md)
- [Lineage Diagram](docs/lineage.md)

---

## Author

Juliana Hubacova — [GitHub](https://github.com/julianahubacova)