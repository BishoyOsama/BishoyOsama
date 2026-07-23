# Bishoy Osama · Data Engineer

> Building reliable data infrastructure — from raw ingestion to analytics-ready datasets.
> Grounded in Medallion architecture, Kimball modeling, and modern orchestration.

📍 Alexandria, Egypt &nbsp;·&nbsp; 🎓 BSc. Computers & Data Science, Alexandria University

---

## Stack

`Python` &nbsp;`SQL` &nbsp;`PySpark` &nbsp;`Kafka` &nbsp;`Microsoft Fabric` &nbsp;`dbt` &nbsp;`Airflow` &nbsp;`Snowflake` &nbsp;`Power BI` &nbsp;`Docker` &nbsp;`Git`

---

## Projects

<details>
<summary><b>01 &nbsp;·&nbsp; AML Transaction Monitoring Pipeline</b> &nbsp;—&nbsp; <i>end-to-end fintech data engineering on Snowflake</i></summary>
<br>

**Goal:**
&nbsp;&nbsp;Build a production-grade incremental pipeline that transforms 32M synthetic banking transactions into a Kimball star schema — with full CI/CD, conformed dimensional modelling, and a Power BI semantic layer that never touches the raw fact table.

**Code:**
&nbsp;&nbsp;[→ View repository](https://github.com/BishoyOsama/AML.git)

**Description:**
&nbsp;&nbsp;Ingests IBM's HI-Medium AML dataset through a four-layer Medallion architecture (Bronze → Silver → Gold → Marts) on Snowflake. The Patterns source file is a non-tabular text format — a local pre-processor parses its BEGIN/END block structure into a flat CSV before ingestion. Silver cleans and types all three sources. Gold implements a star schema with `fct_transactions` (incremental by `run_date`) and five conformed dimensions built via a shared surrogate key macro that prevents FK mismatches across layers. Seven aggregated Marts and six conformed dimension views form the exclusive Power BI import boundary. A custom DAX HTML heatmap with log-scaled colour bucketing surfaces hourly transaction patterns. Three GitHub Actions workflows enforce slim CI with `state:modified+` and `--defer` against a production manifest artifact, `astro dev parse` DAG validation, and two-environment Snowflake promotion (AML → AML_PROD).

**Skills:**
&nbsp;&nbsp;Incremental pipeline design · Kimball dimensional modelling · Medallion architecture · dbt macro authoring · Airflow orchestration · Slim CI/CD · Power BI semantic layer design · Data quality testing

**Technology:**
&nbsp;&nbsp;`Snowflake` &nbsp;`dbt Core` &nbsp;`Airflow` &nbsp;`Astro CLI` &nbsp;`Cosmos` &nbsp;`Power BI` &nbsp;`GitHub Actions` &nbsp;`Python`

**Key decisions:**
- `run_date` filters unconditionally — no `{% if is_incremental() %}` guard — so the first table creation loads one day, not all 32M rows
- Surrogate key lives in a shared macro called in both Silver and Gold — the FK join can never silently drift between layers
- Amount columns are excluded from any mart whose grain does not include currency — cross-currency sums are never computed
- `cd.yml` runs `dbt compile --target prod` only — Airflow owns all pipeline execution, keeping CI/CD and orchestration concerns cleanly separated

**Results:**
- 32M transactions processed incrementally across a four-layer Medallion pipeline on Snowflake Free Tier
- 20+ dbt models with data quality tests at every layer — Silver, Gold, and Marts each have independent test suites
- 8 Cosmos task groups with enforced dependency ordering — dims before fct, full-refresh before incremental, views last
- 3 GitHub Actions workflows with slim CI reducing PR test surface to changed models and their dependents only

<br>
</details>

---

<details>
<summary><b>02 &nbsp;·&nbsp; Logistics Lakehouse Pipeline</b> &nbsp;—&nbsp; <i>end-to-end streaming + batch on Delta Lake</i></summary>
<br>

**Goal:**
&nbsp;&nbsp;Design and deliver a unified lakehouse that handles both real-time logistics event streams and batch historical loads, with a clean serving layer ready for BI consumption.

**Code:**
&nbsp;&nbsp;[→ View repository](https://github.com/BishoyOsama/LogisticsLakehouse)

**Description:**
&nbsp;&nbsp;Ingests logistics events via Kafka producers, lands them into a Bronze Delta Lake layer on Databricks, and processes them with PySpark through Silver cleansing and Gold aggregation stages. dbt models the Gold layer into analytics-ready tables, and Airflow schedules and monitors the full pipeline end to end.

**Skills:**
&nbsp;&nbsp;Streaming ingestion · Batch processing · Medallion architecture · Delta Lake · Pipeline orchestration

**Technology:**
&nbsp;&nbsp;`Kafka` &nbsp;`PySpark` &nbsp;`Databricks` &nbsp;`dbt` &nbsp;`Airflow`

**Results:**
- Unified streaming and batch ingestion under a single Medallion architecture
- Full pipeline from raw Kafka events to BI-ready Gold tables with zero manual intervention

<br>
</details>

---

<details>
<summary><b>03 &nbsp;·&nbsp; Customer Segmentation (RFM)</b> &nbsp;—&nbsp; <i>unsupervised segmentation on 500k+ transactions</i></summary>
<br>

**Goal:**
&nbsp;&nbsp;Turn a raw transactional dataset into behavioral customer cohorts that marketing and product teams can act on directly.

**Code:**
&nbsp;&nbsp;[→ View repository](https://github.com/BishoyOsama/OnlineRetail-Customer-Segmentation)

**Description:**
&nbsp;&nbsp;Cleaned and transformed 500k+ retail transactions in pandas, computed RFM (Recency, Frequency, Monetary) scores per customer, and applied K-Means clustering to group customers into distinct behavioral segments. Segments were profiled and labeled for business interpretability.

**Skills:**
&nbsp;&nbsp;Feature engineering · Unsupervised ML · Customer analytics · Data wrangling

**Technology:**
&nbsp;&nbsp;`Python` &nbsp;`scikit-learn` &nbsp;`pandas`

**Results:**
- 500k+ transactions distilled into clearly separated, business-labeled customer cohorts
- Actionable segments surfaced for direct use in targeting and retention strategy

<br>
</details>

---

## Certifications

- [**AZ-900** · Azure Fundamentals](https://learn.microsoft.com/api/credentials/share/en-us/BishoyOsama-3506/B1DE6ADCD050C948?sharingId=ADDBBCBAFBA067B1) — Microsoft
- [**DP-900** · Azure Data Fundamentals](https://learn.microsoft.com/api/credentials/share/en-us/BishoyOsama-3506/F8D7DE7A60CD77F1?sharingId=ADDBBCBAFBA067B1) — Microsoft
- [**DP-700** · Fabric Data Engineer Associate](https://learn.microsoft.com/api/credentials/share/en-us/BishoyOsama-3506/BE889466F0B2666D?sharingId=ADDBBCBAFBA067B1) — Microsoft

---

## Let's connect

[![Email](https://img.shields.io/badge/osamabisho77@gmail.com-EA4335?style=flat&logo=gmail&logoColor=white)](mailto:osamabisho77@gmail.com) <br/>
[LinkedIn](https://www.linkedin.com/in/bishoy-osama-58693b215/)
