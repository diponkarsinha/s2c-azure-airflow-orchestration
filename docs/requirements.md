# Requirements: S2C Azure landing + Airflow orchestration

## Functional (what it must do)
| ID | Requirement |
|----|-------------|
| F1 | Source files land in ADLS `landing/<batch|stream>/<source>/<entity>/<yyyy>/<mm>/<dd>/` |
| F2 | Stream files load into RAW automatically (Event Grid + Snowpipe auto-ingest) |
| F3 | Batch files load into RAW when the Airflow DAG runs |
| F4 | The 27 data quality checks run after every load |
| F5 | dbt runs only when the gate is PASS |
| F6 | Loaded files move from `landing` to `archive` (ADF, incremental by watermark) |
| F7 | Every file is traceable: upload, load, checks, archive |

## Non-functional (how well it must do it)
| ID | Area | Requirement |
|----|------|-------------|
| N1 | Freshness | Batch data in the marts by 08:00 on delivery days; stream data within 5 minutes |
| N2 | Security | No stored passwords or keys in code; OIDC for GitHub, managed identity for ADF, Key Vault for secrets |
| N3 | Least privilege | Each identity gets only the role it needs (reader / contributor on one container) |
| N4 | Cost | Under EUR 1 for the whole project; budget and anomaly alerts on |
| N5 | Reliability | Every step safe to re-run; retries and timeouts on every Airflow task |
| N6 | Monitoring | Failures alert by email; one Azure dashboard; Snowflake health views |
| N7 | Recoverability | Original files archived; any day can be re-run (backfill) |
| N8 | Rollback | Return to tag v1.0-snowflake-only within 30 minutes |
