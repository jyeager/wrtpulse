# AGENTS.md

Instructions for AI coding agents working on **wrtpulse** (OpenWRT network monitoring dashboard and alerting web application).

## Project Overview

- **Goal:** Lightweight, self-hosted web dashboard and alerting service for OpenWRT routers, running in a **single Docker container on Linux** (Go backend serving a React/TypeScript website, with a mounted volume for config and persistent data).
- **Key Docs:**
  - `README.md` — High-level overview and repo structure
  - `docs/architecture.md` — Living system architecture plan and deferred design decisions
  - `docs/prd/README.md` — PRD index, naming rules, and status lifecycle

## PRD-First Workflow

This repository is built iteratively from Product Requirements Documents:

1. **No speculative features:** Do not scaffold or implement application code for a new feature without an approved PRD in `docs/prd/` (unless the user explicitly asks to prototype or bypass).
2. **Creating PRDs:** Copy `docs/prd/TEMPLATE.md` to `docs/prd/XXXX-short-slug.md` (zero-padded sequential ID) and add an entry to the index table in `docs/prd/README.md`.
3. **Keeping docs in sync:** When a PRD changes architecture decisions or adds build/test commands, update `docs/architecture.md` and this `AGENTS.md` in the same change.

## Repository Layout

- `cmd/wrtpulse/` — Go web server entrypoint (flags, env config, graceful `SIGTERM` shutdown)
- `internal/` — Private Go packages (`config`, `collector`, `store`, `alert`, `api`)
- `web/` — React + TypeScript web dashboard
- `deploy/` — Multi-stage `Dockerfile`, `docker-compose.yml`, and Linux deployment configs
- `docs/` — Architecture docs and PRDs (`docs/prd/`)

## Tech Stack & Coding Standards

- **Runtime Target (Docker on Linux):**
  - Build as a single Linux container (multi-stage `Dockerfile`, `amd64`/`arm64`) where the Go server serves the compiled React/TS website alongside the API.
  - Keep container state cleanly separated onto a mounted volume (e.g., `/data`) and support environment-variable configuration and graceful `SIGTERM` shutdown.
- **Backend (Go):**
  - Keep code idiomatic (`gofmt`), wrap errors with context (`fmt.Errorf("...: %w", err)`), avoid hidden global state, and write table-driven unit tests for core logic.
- **Frontend (React + TypeScript):**
  - Use TypeScript strict mode; avoid `any` and `@ts-ignore`.
  - Keep components small, accessible, and decoupled from raw transport details.
- **OpenWRT Constraints:**
  - `wrtpulse` runs off-router on a Linux Docker host; keep any router-side interaction lightweight and respectful of low CPU/RAM/flash routers.

## Build, Test & Lint Commands

> **Status:** Application code has not been scaffolded yet. Update this section with exact commands as soon as `go.mod`, `web/package.json`, `Dockerfile`, or a `Makefile` is introduced.

- **Backend:** *(TBD — e.g. `go test ./...`, `go vet ./...`)*
- **Frontend:** *(TBD — e.g. lint, typecheck, build, test)*
- **Docker (Linux):** *(TBD — e.g. `docker compose build`, `docker compose up`)*
- **Full verification:** *(TBD)*

## Operational Guardrails

### Allowed Without Prompting
- Reading any repository file and searching the codebase
- Drafting or updating documentation and PRDs when requested
- Running local linters, formatters, typechecks, and unit tests

### Require Explicit Approval First
- Adding, upgrading, or removing external Go or npm dependencies
- Deleting files or directories
- Creating commits, pushing to remote branches, or opening/merging PRs
- Changing Docker/deployment configs, exposed ports, or router-side scripts

### Never Do
- Never commit secrets, `.env` files, router passwords, API tokens, SSH keys, or real LAN/WAN captures/IPs.
- Never run destructive Git commands (`git push --force`, `git reset --hard`) without explicit confirmation.
- Never claim a task is complete without running relevant checks/tests (once configured) and reporting any failures honestly.

## Git & Maintenance Conventions

- **Commits:** Use [Conventional Commits](https://www.conventionalcommits.org/) (`feat:`, `fix:`, `docs:`, `chore:`, `refactor:`, `test:`).
- **Keep `AGENTS.md` lean:** Treat this file like source code. As `internal/` and `web/` grow, move language-specific details into scoped `internal/AGENTS.md` and `web/AGENTS.md` files, and put multi-step runbooks into `.agents/skills/<name>/SKILL.md`.
