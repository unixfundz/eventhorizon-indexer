# EventHorizon Indexer 🔭

![Django CI](https://github.com/unixfundz/eventhorizon-indexer/actions/workflows/django-ci.yml/badge.svg)
![Soroban CI](https://github.com/unixfundz/eventhorizon-indexer/actions/workflows/soroban-ci.yml/badge.svg)
![Security](https://github.com/unixfundz/eventhorizon-indexer/actions/workflows/security.yml/badge.svg)
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)

A production-grade, open-source event indexing platform for **Soroban smart contracts on Stellar**.

EventHorizon Indexer ingests contract events, stores them reliably, and exposes them through REST, GraphQL, and signed webhooks.

---

## Why this project exists

Running a complete event ingestion stack for Soroban can be expensive for each app team.
EventHorizon Indexer provides a reusable, self-hostable infrastructure layer so teams can:

- index events from one or many contracts
- query history with filters and pagination-friendly patterns
- receive push-based webhook notifications
- run in Docker locally and Kubernetes in production

---

## Naming and terminology (important)

- **Project name:** `EventHorizon Indexer`
- **Blockchain platform:** `Stellar`
- **Smart-contract runtime on Stellar:** `Soroban`

Folder names like `soroban-contracts/` are intentional and correct.
They describe the Soroban runtime target, **not** the previous project name.
There are no remaining `SoroScan`/legacy project-name references in this repository.

---

## Core features

- **Soroban-native contract module** with admin-controlled indexer authorization
- **Django REST API** for tracked contracts, events, and subscriptions
- **GraphQL API (Strawberry)** for flexible filtering across contract/event/ledger ranges
- **Webhook fanout** with HMAC signatures and Celery retry/backoff
- **PostgreSQL + Redis** operational stack for durability and async processing
- **Kubernetes manifests** for production deployment
- **CI/CD workflows** for backend, contract quality, docs, security, CodeQL, and release

---

## Architecture

```text
Soroban Contracts  ->  Ingestion Layer (Django mgmt/celery)  ->  PostgreSQL
                                            |                    
                                            +-> REST API
                                            +-> GraphQL API
                                            +-> Webhooks (HMAC)
```

Detailed architecture notes live in:
- `docs/ARCHITECTURE.md`

---

## Repository structure

```text
eventhorizon-indexer/
├── soroban-contracts/
│   └── eventhorizon_core/
│       ├── Cargo.toml
│       └── src/lib.rs
├── django-backend/
│   ├── eventhorizon/
│   │   ├── eventhorizon/      # settings, urls, celery, wsgi/asgi
│   │   └── ingest/            # models, views, schema, tasks, ingest command
│   ├── requirements.txt
│   ├── Dockerfile
│   └── .env.example
├── k8s/
├── .github/workflows/
├── docs/
├── docker-compose.yml
└── LICENSE
```

---

## Quick start (local)

### Prerequisites

- Docker
- Docker Compose

### Run

```bash
cp django-backend/.env.example django-backend/.env
docker compose up --build
```

Services:
- REST API: `http://localhost:8000/api/events/`
- GraphQL Playground: `http://localhost:8000/graphql/`
- Django Admin: `http://localhost:8000/admin/`

---

## Smart contract build (optional local dev)

```bash
cd soroban-contracts/eventhorizon_core
cargo build --target wasm32-unknown-unknown --release
```

---

## Production deployment (Kubernetes)

1. Build and push backend container image.
2. Create namespace + secrets/config.
3. Apply manifests in `k8s/`.
4. Verify backend, worker, and beat health.

```bash
kubectl apply -f k8s/
kubectl get pods -n eventhorizon
```

---

## CI/CD workflows included

- `django-ci.yml` (lint + test backend)
- `soroban-ci.yml` (contract build)
- `contract-quality.yml` (fmt + clippy + tests)
- `security.yml` (dependency audits)
- `codeql.yml` (static security analysis)
- `docs-ci.yml` (markdown + link checks)
- `release.yml` (tag-based release artifacts)

---

## Open-source readiness checklist

- MIT license
- Contributing guide
- Architecture docs
- Local/dev/prod deployment paths
- Typed/pinned dependencies
- CI + security workflows

---

## Contributing

See `CONTRIBUTING.md` for contribution workflow, coding standards, PR requirements, and quality gates.

## License

MIT — see `LICENSE`.
