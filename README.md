# 📊 State of the Data Job Market — an Automated dbt Pipeline
[![📖 dbt Docs](https://img.shields.io/badge/📖_dbt_docs-live-blue)](https://lukebarousse.github.io/basic_testing/)

A tested, documented dbt + DuckDB pipeline over 692k real job postings —
rebuilt and republished automatically by GitHub Actions on every push.

<- the badge is the front door: one click from the README into the full docs site
   (2.13 adds the Actions "passing" badge right next to it)

(dbt docs DAG screenshot — sources → diamond → your marts)

## 🧾 Executive Summary (For Hiring Managers)
- ✅ **dbt pipeline:** 8 models from declared sources to insight marts — zero hardcoded paths
- ✅ **Dependency graph:** models chained with ref()/source(); dbt orders + parallelizes the build
- ✅ **Data tests:** every mart's grain covered by unique/not_null — dbt build fails on bad data
- ✅ **Documentation:** every model + column described in YAML, rendered by dbt docs
- ✅ **Automation:** GitHub Actions rebuilds, tests, and PUBLISHES the warehouse on push + weekly

If you only have a minute, review these:
1. [models/monthly_summary.sql](...) — the two-branch join (ref() dependencies)
2. [models/schema.yml](...) — tests + docs for every model
3. [.github/workflows/dbt_build.yml](...) — the pipeline that runs itself

## 📈 Headline Findings
- Meta posted 32,855 jobs — 2x the #2 employer             <- THEIR numbers,
- Remote is under 7% for every data role                   <- from THEIR models
- Only 21.3% of postings show pay — and it's text ("100K-186K a year")

## 🛠️ dbt Skills in This Repo
| Skill | Where to look |
| --- | --- |
| Sources (no hardcoded paths) | models/sources.yml — external_location per table |
| Model dependencies | ref() in every downstream model; source() at the roots |
| Materializations | dbt_project.yml default + per-model config() overrides |
| Data tests | schema.yml — grain tests on every mart |
| Documentation | descriptions throughout; dbt docs generate renders the site |
| Environments | dev (local scratch) vs prod (the published warehouse) targets |

## 🤖 The Pipeline Runs Itself
On every push (and each Monday), GitHub Actions: downloads the raw data →
rebuilds all models → runs every test → publishes the warehouse.
(2.13 adds: status badge + the "Query it live" ATTACH block)

## 🚀 How to Run
uv sync
python scripts/download_data.py
dbt build