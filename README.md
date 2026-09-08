# BenchworksAI — Outbound

FastAPI backend for an AI-assisted outbound sales pipeline: ingest webhooks from
messaging and CRM providers, enrich and score leads through AI pipelines, and
orchestrate multi-step outbound sequences. Exposes an MCP server so an AI agent can
drive the same operations a human operator would.

## Stack

Python · FastAPI · PostgreSQL · Model Context Protocol (MCP) server · Docker

## Layout

```
backend/app/
  routes/        HTTP endpoints and webhook receivers
  services/      business logic — enrichment, scoring, sequencing
  models/        database models
  db/            migrations and session management
  mcp/           MCP server exposing operations as agent-callable tools
  middleware/    auth, logging, request handling
  dependencies/  shared FastAPI dependency injection
  scripts/       operational tooling
```

## What's interesting here

- **MCP as a first-class interface.** Rather than bolting an agent onto the app,
  the same service layer is exposed both as HTTP routes for the dashboard and as
  MCP tools for an AI agent, so both paths share validation and business rules.
- **Webhook ingestion is separated from AI processing** (`phase-02a-webhooks` vs
  `phase-02b-ai-pipelines`), so provider callbacks return fast and slow model calls
  happen out of band.

## Development

```bash
make install
cp .env.example .env
make dev
```

See `Makefile` for the full task list. Build documentation lives in the
`benchworks-outbound-phase-*.md` files, which specify each phase before it was built.
