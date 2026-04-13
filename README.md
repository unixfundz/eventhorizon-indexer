# EventHorizon Indexer 🔭

![Rust](https://img.shields.io/badge/Rust-Soroban-orange)
![Django](https://img.shields.io/badge/Django-Backend-green)
![GraphQL](https://img.shields.io/badge/GraphQL-Strawberry-E10098)
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)

**The Graph for Soroban** — index, query, and subscribe to smart contract events.

EventHorizon Indexer is a production-ready, open-source indexing platform for Soroban smart contract events on Stellar. It combines a Rust smart contract with a Django + Celery backend to provide:

- Real-time event ingestion
- REST + GraphQL query APIs
- HMAC-signed webhook subscriptions
- PostgreSQL persistence
- Docker and Kubernetes deployment support

## Repository Layout

```text
eventhorizon-indexer/
├── soroban-contracts/
│   └── eventhorizon_core/
├── django-backend/
│   ├── eventhorizon/
│   │   ├── eventhorizon/
│   │   └── ingest/
│   ├── scripts/
│   └── requirements.txt
├── k8s/
├── .github/workflows/
└── docs/
```

## Quick Start

```bash
cp django-backend/.env.example django-backend/.env
docker compose up --build
```

- REST: `http://localhost:8000/api/events/`
- GraphQL: `http://localhost:8000/graphql/`
- Admin: `http://localhost:8000/admin/`

## Core Features

- Soroban-native event contract with admin/indexer authorization
- Django REST Framework endpoints for contracts/events/subscriptions
- Strawberry GraphQL schema with flexible filtering
- Celery worker for reliable webhook dispatch and retries
- Backfill + polling command for Stellar/Soroban event ingestion
- CI with linting, tests, and build validation

## License

MIT License.
