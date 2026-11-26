# Project charter: S2C Azure landing + Airflow orchestration

## Goal
Move file landing from Snowflake internal stages to Azure ADLS Gen2 and run the
whole pipeline from one Airflow DAG, without changing any data result.

## In scope
- ADLS Gen2 landing zone (landing / archive / quarantine) with lifecycle rules
- Event Grid + Snowpipe auto-ingest for the risk stream
- GitHub Actions upload to ADLS with OIDC (no stored secrets)
- ADF pipeline that archives loaded files (watermark)
- Airflow DAG: load -> checks -> gate -> dbt build -> archive -> Power BI refresh
- Azure dashboard, cost guardrails, runbook

## Out of scope
- Changes to dbt models or KPIs
- Spark/Databricks, Kafka/Event Hubs, Terraform
- A production environment (dev only)

## Success criteria
1. 12 existing waves + 2 new waves: 0 missed
2. Row counts and totals equal docs/baseline_v1
3. Azure cost under EUR 1 for the project
4. One command tears everything down (azure_down.sh)
5. Gate PASS and CI green on S2C_DEV after cutover

## Timeline
Start 2026-11-26 - Phase 0-2 by 2026-11-30 - Phase 3-5 by 2026-12-05 - Test by 2026-12-08 - Cutover 2026-12-10

## Roles
Data owner: Procurement (fictional) | Builder and reviewer: Diponkar Sinha

## Risks and mitigation
- Unexpected Azure cost -> budget + anomaly alerts, policy limits, teardown script
- Double scheduling -> Airflow is the only scheduler; Snowflake tasks suspended
- Missed Event Grid events -> F05 check + ALTER PIPE REFRESH (wave 13)
- Breaking the working pipeline -> test in S2C_AZ, tag v1.0-snowflake-only for rollback
