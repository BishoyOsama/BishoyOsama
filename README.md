<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&size=22&duration=3000&pause=1000&color=58A6FF&center=true&vCenter=true&width=700&lines=Data+Engineer;Building+reliable+data+infrastructure;From+raw+ingestion+to+analytics-ready+datasets" alt="Bishoy Osama" />

<br/>

**Bishoy Osama** &nbsp;·&nbsp; Alexandria, Egypt

BSc. Computers & Data Science, Alexandria University

<br/>

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/bishoy-osama-58693b215/)
[![Email](https://img.shields.io/badge/osamabisho77@gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:osamabisho77@gmail.com)


</div>

---

Grounded in Medallion architecture, Kimball modeling, and modern orchestration. I build data platforms that are maintainable, well-documented, and honest about their trade-offs.

---

## Stack

<table>
<tr>
<td><b>Languages</b></td>
<td>

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=postgresql&logoColor=white)

</td>
</tr>
<tr>
<td><b>Processing</b></td>
<td>

![PySpark](https://img.shields.io/badge/PySpark-E25A1C?style=flat-square&logo=apachespark&logoColor=white)
![dbt](https://img.shields.io/badge/dbt-FF694B?style=flat-square&logo=dbt&logoColor=white)
![Kafka](https://img.shields.io/badge/Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white)

</td>
</tr>
<tr>
<td><b>Platforms</b></td>
<td>

![Microsoft Fabric](https://img.shields.io/badge/Microsoft_Fabric-0078D4?style=flat-square&logo=microsoft&logoColor=white)
![Snowflake](https://img.shields.io/badge/Snowflake-29B5E8?style=flat-square&logo=snowflake&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonaws&logoColor=white)

</td>
</tr>
<tr>
<td><b>Orchestration & BI</b></td>
<td>

![Airflow](https://img.shields.io/badge/Airflow-017CEE?style=flat-square&logo=apacheairflow&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=flat-square&logo=powerbi&logoColor=black)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)

</td>
</tr>
</table>

---

## Projects

### Olist E-Commerce Lakehouse

> Multi-source lakehouse on Microsoft Fabric — real Brazilian e-commerce data, synthetic Kafka event stream, Kimball star schema, and CI/CD via GitHub Actions.

<table>
<tr>
<td width="120"><b>Goal</b></td>
<td>Build an end-to-end data platform ingesting historical data from AWS Aurora and a continuous synthetic event stream from Kafka, unified at a clean silver layer, and served via a Kimball star schema to Power BI.</td>
</tr>
<tr>
<td><b>Code</b></td>
<td><a href="https://github.com/BishoyOsama/olist-lakehouse">→ View repository</a></td>
</tr>
<tr>
<td><b>Description</b></td>
<td>

The Olist dataset (99k real Brazilian e-commerce orders, 2016–2018) lives in Amazon Aurora behind a private VPC. A Windows Server EC2 instance runs the Microsoft On-Premises Data Gateway inside the same VPC — no public database exposure. Fabric's Data Pipeline connects through the gateway to extract all source tables into a Bronze Lakehouse.

A second EC2 instance (Amazon Linux) runs a stateful Python generator as a systemd service, producing realistic Kafka order lifecycle events from 2019 onward — timing distributions derived from the actual historical data. Fabric Eventstream consumes two Kafka topics (order events and review events) into a separate Bronze Lakehouse.

The generated stream required three silver sub-layers before it could meet historical data: parse raw JSON events, flatten nested item and payment arrays, then reconstruct full order records from events arriving across multiple days using window functions and conditional aggregation.

Gold implements a Kimball star schema with three fact tables and six dimensions. dim_geography was dropped — the source geolocation data spans multiple cities and states per zip prefix and could not support a clean dimension. A separate customer resolution table handles the two-hop lookup needed for generated orders, which must always resolve to the current customer version regardless of which historical customer ID was sampled.

</td>
</tr>
<tr>
<td><b>Skills</b></td>
<td>Multi-source ingestion · Medallion architecture · Kimball dimensional modelling · SCD Type 2 · Delta Lake MERGE · Accumulating snapshot fact · Event stream reconstruction · CI/CD</td>
</tr>
<tr>
<td><b>Technology</b></td>
<td>

![Microsoft Fabric](https://img.shields.io/badge/Microsoft_Fabric-0078D4?style=flat-square&logo=microsoft&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonaws&logoColor=white)
![Kafka](https://img.shields.io/badge/Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white)
![PySpark](https://img.shields.io/badge/PySpark-E25A1C?style=flat-square&logo=apachespark&logoColor=white)
![Delta Lake](https://img.shields.io/badge/Delta_Lake-00ADD8?style=flat-square&logo=delta&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=flat-square&logo=powerbi&logoColor=black)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)

</td>
</tr>
<tr>
<td><b>Key decisions</b></td>
<td>

- dim_geography dropped — source data could not support a clean dimension at zip prefix grain; customer and seller dims carry sufficient location data
- Review fact grain dropped — Olist reviews are order-level; forcing them onto a product or seller grain required approximations that would mislead
- Payment type excluded from order items fact — multi-method orders make item-level attribution an approximation; payment analysis belongs in the payment fact
- Generated orders use two-hop customer resolution: `customer_id` → `customer_unique_id` → `customer_key` where `is_current = True`
- CI/CD via `microsoft-fabric-cicd` library — deploys Notebooks, Spark Job Definitions, and Pipelines to Fabric on every merge to main with environment-specific GUID replacement via `parameter.yml`

</td>
</tr>
<tr>
<td><b>Results</b></td>
<td>

- Two independent ingestion pipelines converging at a single clean silver layer
- Three fact tables and six dimensions with full referential integrity and surrogate key determinism via SHA-256 hashing
- Stateful Kafka generator producing realistic order lifecycle events with timing derived from real historical distributions
- Full CI/CD — lint, unit tests, and Fabric deployment on every merge to main

</td>
</tr>
</table>

---

### AML Transaction Monitoring Pipeline

> Production-grade incremental pipeline on Snowflake — 32M transactions through a four-layer Medallion architecture with a Kimball star schema and slim CI/CD.

<table>
<tr>
<td width="120"><b>Goal</b></td>
<td>Transform 32M synthetic banking transactions into a Kimball star schema with full CI/CD, conformed dimensional modelling, and a Power BI semantic layer that never touches the raw fact table.</td>
</tr>
<tr>
<td><b>Code</b></td>
<td><a href="https://github.com/BishoyOsama/AML.git">→ View repository</a></td>
</tr>
<tr>
<td><b>Description</b></td>
<td>

Ingests IBM's HI-Medium AML dataset through Bronze → Silver → Gold → Marts on Snowflake. The Patterns source file is a non-tabular text format — a local pre-processor parses its BEGIN/END block structure into a flat CSV before ingestion. Silver cleans and types all three sources. Gold implements a star schema with `fct_transactions` (incremental by `run_date`) and five conformed dimensions built via a shared surrogate key macro that prevents FK mismatches across layers. Seven aggregated Marts and six conformed dimension views form the exclusive Power BI import boundary. A custom DAX HTML heatmap with log-scaled colour bucketing surfaces hourly transaction patterns.

</td>
</tr>
<tr>
<td><b>Skills</b></td>
<td>Incremental pipeline design · Kimball dimensional modelling · Medallion architecture · dbt macro authoring · Airflow orchestration · Slim CI/CD · Power BI semantic layer design · Data quality testing</td>
</tr>
<tr>
<td><b>Technology</b></td>
<td>

![Snowflake](https://img.shields.io/badge/Snowflake-29B5E8?style=flat-square&logo=snowflake&logoColor=white)
![dbt](https://img.shields.io/badge/dbt-FF694B?style=flat-square&logo=dbt&logoColor=white)
![Airflow](https://img.shields.io/badge/Airflow-017CEE?style=flat-square&logo=apacheairflow&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=flat-square&logo=powerbi&logoColor=black)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)

</td>
</tr>
<tr>
<td><b>Key decisions</b></td>
<td>

- `run_date` filters unconditionally — no `{% if is_incremental() %}` guard — so the first table creation loads one day, not all 32M rows
- Surrogate key lives in a shared macro called in both Silver and Gold — the FK join can never silently drift between layers
- Amount columns excluded from any mart whose grain does not include currency — cross-currency sums are never computed
- `cd.yml` runs `dbt compile --target prod` only — Airflow owns all pipeline execution, keeping CI/CD and orchestration concerns cleanly separated

</td>
</tr>
<tr>
<td><b>Results</b></td>
<td>

- 32M transactions processed incrementally across a four-layer Medallion pipeline on Snowflake Free Tier
- 20+ dbt models with data quality tests at every layer
- 8 Cosmos task groups with enforced dependency ordering
- 3 GitHub Actions workflows with slim CI reducing PR test surface to changed models and their dependents only

</td>
</tr>
</table>

---

### Customer Segmentation (RFM)

> Unsupervised segmentation on 500k+ retail transactions using K-Means clustering.

<table>
<tr>
<td width="120"><b>Goal</b></td>
<td>Turn a raw transactional dataset into behavioral customer cohorts that marketing and product teams can act on directly.</td>
</tr>
<tr>
<td><b>Code</b></td>
<td><a href="https://github.com/BishoyOsama/OnlineRetail-Customer-Segmentation">→ View repository</a></td>
</tr>
<tr>
<td><b>Description</b></td>
<td>Cleaned and transformed 500k+ retail transactions in pandas, computed RFM (Recency, Frequency, Monetary) scores per customer, and applied K-Means clustering to group customers into distinct behavioral segments. Segments were profiled and labeled for business interpretability.</td>
</tr>
<tr>
<td><b>Skills</b></td>
<td>Feature engineering · Unsupervised ML · Customer analytics · Data wrangling</td>
</tr>
<tr>
<td><b>Technology</b></td>
<td>

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?style=flat-square&logo=pandas&logoColor=white)

</td>
</tr>
<tr>
<td><b>Results</b></td>
<td>

- 500k+ transactions distilled into clearly separated, business-labeled customer cohorts
- Actionable segments surfaced for direct use in targeting and retention strategy

</td>
</tr>
</table>

---

## Certifications

<table>
<tr>
<td>

[![AZ-900](https://img.shields.io/badge/AZ--900_Azure_Fundamentals-0078D4?style=flat-square&logo=microsoft&logoColor=white)](https://learn.microsoft.com/api/credentials/share/en-us/BishoyOsama-3506/B1DE6ADCD050C948?sharingId=ADDBBCBAFBA067B1)

</td>
<td>

[![DP-900](https://img.shields.io/badge/DP--900_Azure_Data_Fundamentals-0078D4?style=flat-square&logo=microsoft&logoColor=white)](https://learn.microsoft.com/api/credentials/share/en-us/BishoyOsama-3506/F8D7DE7A60CD77F1?sharingId=ADDBBCBAFBA067B1)

</td>
<td>

[![DP-700](https://img.shields.io/badge/DP--700_Fabric_Data_Engineer_Associate-0078D4?style=flat-square&logo=microsoft&logoColor=white)](https://learn.microsoft.com/api/credentials/share/en-us/BishoyOsama-3506/BE889466F0B2666D?sharingId=ADDBBCBAFBA067B1)

</td>
</tr>
</table>

---

<div align="center">

[![Email](https://img.shields.io/badge/osamabisho77@gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:osamabisho77@gmail.com)
&nbsp;·&nbsp;
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/bishoy-osama-58693b215/)

</div>
