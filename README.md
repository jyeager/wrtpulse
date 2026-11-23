# wrtpulse

OpenWRT network monitoring dashboard and alerting web application.

> **Status:** Early planning & scaffolding phase. Features, collection architecture, and implementation details are being defined iteratively via [PRDs](docs/prd/README.md).

## Overview

`wrtpulse` is a lightweight, self-hosted monitoring website and alerting service for OpenWRT routers. It is designed to run in a **single Docker container on Linux**, serving a React/TypeScript web dashboard from a Go backend with a mounted host volume for configuration and persistent data.

## Planned Tech Stack

- **Deployment:** Single Docker container on Linux (Docker / Docker Compose, mounted volume for data & config)
- **Backend:** Go (HTTP server serving the web UI, REST/WebSocket API, OpenWRT collector, storage, and alerting engine)
- **Frontend:** React + TypeScript web dashboard

## Repository Structure

```text
wrtpulse/
├── AGENTS.md           # Instructions & guardrails for AI coding agents
├── cmd/wrtpulse/       # Go web server entrypoint
├── internal/           # Private Go packages (collectors, storage, alerting, API, config)
├── web/                # React + TypeScript web dashboard
├── deploy/             # Dockerfile, docker-compose.yml, and Linux deployment configs
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
