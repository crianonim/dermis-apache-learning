# dermis-apache-learning

**Purpose:** Local data-lakehouse sandbox for learning Apache Iceberg / data-engineering tooling. No custom application code — it is a `docker-compose` stack wiring together off-the-shelf services.

## Stack
- **Nessie** (`projectnessie/nessie`) — Iceberg catalog server, RocksDB-backed, API on `19120`.
- **MinIO** (`minio/minio`) — S3-compatible object storage (`9000` API, `9001` console); entrypoint auto-creates buckets `datalake`, `datalakehouse`, `warehouse`, `seed` and copies `./minio-data/*` into `seed`.
- **Spark** (`alexmerced/spark35nb`) — Spark 3.5 + JupyterLab (`8888`, no token), master/worker/history UIs on `8080`/`8081`/`18080`.
- **Dremio** (`dremio/dremio-oss`) — query engine, UI on `9047`.

All services share the `intro-network` Docker network. Credentials are hardcoded dev defaults (`admin`/`password`).

## Run
```bash
docker compose up -d      # start all services in background
docker compose down       # stop and remove containers
```
Then open Jupyter at http://localhost:8888, MinIO console at http://localhost:9001, Dremio at http://localhost:9047.

## Structure
- `docker-compose.yml` — the whole stack.
- `readme.md` — detailed service/port docs.
- `nessie-data/`, `minio-data/`, `notebook-seed/` — mounted persistence / seed dirs.

## Status/Notes
Sandbox / learning project (Sep 2024). Follows the "alexmerced" data-lakehouse tutorial pattern. Not for production.
