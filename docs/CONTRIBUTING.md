# Contributing to EventHorizon Indexer

## Development Standards

- Open an issue for non-trivial changes before implementation.
- Follow Conventional Commits.
- Add tests for all behavior changes.
- Keep PRs small and focused.

## Local Setup

```bash
cp django-backend/.env.example django-backend/.env
docker compose up --build
```

## Code Quality

Backend checks:

```bash
ruff check django-backend
pytest
```

Contract checks:

```bash
cd soroban-contracts/eventhorizon_core
cargo fmt --check
cargo clippy -- -D warnings
```
