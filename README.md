# wrtpulse

OpenWRT network monitoring dashboard and alerting tool.

> **Status:** Early planning & scaffolding phase. Features, collection architecture, and implementation details are being defined iteratively via [PRDs](docs/prd/README.md).

## Overview

`wrtpulse` aims to provide a lightweight, self-hosted monitoring dashboard and alerting service tailored for OpenWRT routers—designed to ship as a single Go binary with an embedded React/TypeScript web UI and ready-to-run Docker images.

## Planned Tech Stack

- **Backend:** Go (single lightweight binary, embedded frontend assets)
- **Frontend:** React + TypeScript
- **Packaging:** Docker / single static binary

## Repository Structure

```text
wrtpulse/
├── cmd/wrtpulse/       # Go application entrypoint
├── internal/           # Private Go packages (collectors, storage, alerting, API, config)
├── web/                # React + TypeScript frontend
├── deploy/             # Docker, Docker Compose, and deployment manifests
├── docs/
│   ├── architecture.md # High-level living architecture plan
│   └── prd/            # Product Requirements Documents (PRDs)
├── LICENSE             # MIT License
└── README.md
```

## Documentation & Workflow

- **[Architecture Plan](docs/architecture.md):** High-level system structure and open design decisions.
- **[PRDs](docs/prd/README.md):** Feature specifications and design proposals driving implementation.

## License

This project is licensed under the [MIT License](LICENSE).
