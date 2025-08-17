# DataBridge

**DataBridge** is a lightweight Python product that **moves business tables from MS SQL Server to Snowflake** on a schedule, with **data quality checks** and a **simple dashboard** showing:
- last load time,
- rows moved,
- validation status.

It’s designed to be **deployable in a day** and extensible in weeks.

## Who it’s for
- Data teams who need a reliable path from **SQL Server → Snowflake**.
- Analysts who want **fresh, validated data** without chasing pipelines.
- Engineers who want a **clear, testable Python codebase** to extend.

## What it does (v1 scope)
1. **Extract**: Read a configured table from SQL Server.
2. **Transform**: Clean types, normalize values, compute derived fields.
3. **Validate**: Run basic quality checks (not-null, allowed sets, ranges).
4. **Load**: Upsert into Snowflake target table.
5. **Observe**: Serve a tiny **dashboard** (web UI) with freshness and counts.

## Non-goals (for v1)
- Full-blown orchestration platform.
- Complex CDC. (We’ll add simple incremental keys later.)
- Secret managers and enterprise identity (use env vars or config file).

## Why this exists
- Most teams need a **minimum viable bridge** between legacy SQL Server and Snowflake.
- Hiring panels want a **working product** that maps directly to daily tasks, not a demo toy.

## Roadmap
- v1 (MVP): single-table sync + page for freshness/row counts + config file.
- v1.1: incremental loads (updated_at or watermark key).
- v1.2: multiple tables via YAML list + per-table DQ rules.
- v1.3: email/slack alerts on DQ failure or zero-row loads.

## Milestone Acceptance Criteria (v1)
- `make run:etl` loads data to Snowflake.
- `make run:dashboard` serves a page with:
  - Last load timestamp
  - Row count in Snowflake
  - Latest validation status (pass/fail)
- Setup requires only a YAML config + drivers.

## Quickstart (will be expanded later)
- Copy `config/settings.example.yaml` → `config/settings.yaml` and fill creds.
- Install deps with `uv` (or pip). Run `make run:etl` then `make run:dashboard`.

