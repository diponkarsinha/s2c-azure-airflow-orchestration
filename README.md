# S2C Azure + Airflow orchestration

Azure landing (ADLS Gen2, Event Grid, ADF) and Airflow orchestration for the
S2C data platform.

Part of a three-repo project:
- [s2c-snowflake-data-source](https://github.com/diponkarsinha/s2c-snowflake-data-source): source data, ingestion, 27 data quality checks
- [s2c-dbt-analytics](https://github.com/diponkarsinha/s2c-dbt-analytics): dbt models, tests, KPIs
- **s2c-azure-airflow-orchestration** (this repo): Azure infrastructure and the Airflow DAG

## Status
In progress: Phase 0 (preparation)

## Documents
- [Project charter](docs/project_charter.md)
- [Baseline v1 numbers](docs/baseline_v1/)
- [Requirements](docs/requirements.md)
- [Cost estimate](docs/cost_estimate.md)
