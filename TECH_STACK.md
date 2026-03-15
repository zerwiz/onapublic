# Ona & Ona Sphere — Technical Stack

**Last updated (UTC): 2026-03-15**

This document gives a high-level overview of the technologies Ona and Ona Sphere are built with. It is for anyone who wants to know what’s “under the hood” without reading the main (private) codebase. For what Ona and Sphere *are* and how they connect, see [WHAT_IS_ONA_AND_SPHERE.md](WHAT_IS_ONA_AND_SPHERE.md).

```mermaid
flowchart TB
  subgraph runtime["Core runtime"]
    Rust[Rust]
    Tokio[Tokio]
    Axum[Axum]
    CLI[Ona CLI]
  end
  subgraph front["Web & desktop"]
    Astro[Astro]
    Electron[Electron]
  end
  subgraph data["Data"]
    SQL[(SQLite)]
    Files[Files]
  end
  subgraph ai["AI"]
    LLM[Ollama / llama.cpp / APIs]
  end
  Rust --> Tokio
  Rust --> Axum
  Rust --> CLI
  runtime --> front
  runtime --> data
  runtime --> ai
```

---

## Core runtime

| Layer | Technology | Role |
|-------|------------|------|
| **Language** | **Rust** (edition 2021) | Core services and CLI are written in Rust. Single workspace with multiple crates (libraries and binaries). |
| **Async runtime** | **Tokio** | Async I/O, HTTP, and concurrency across services. |
| **HTTP & APIs** | **Axum** | Web framework for REST and WebSocket endpoints. |
| **CLI** | **Ona CLI** (Rust) | Main entry point for install, start, stop, jobs, memory, models, and all commands. Built as part of the Rust workspace. |

---

## Main services (Ona)

The main Ona deployment runs a small set of services that work together:

| Service | Purpose |
|---------|---------|
| **event-handler** | Ingests webhooks (web, Telegram, WhatsApp, Signal, Discord), creates jobs, routes to orchestration, and streams responses back to channels. |
| **agent-runtime** | Executes the agent loop: calls the LLM, runs tools, uses memory and RAG, and coordinates specialist sub-agents. |
| **orchestration-service** | (Used by event-handler) Job lifecycle, routing, and coordination. |
| **comms-web** | Web UI for chat, onboarding, and mission control. Served as static/site. |

All of the above are Rust binaries (except the web UI). The web UI is built separately and served by a small web server or in Docker.

```mermaid
flowchart LR
  subgraph channels["Channels"]
    Web[Web]
    TG[Telegram]
    WA[WhatsApp]
    Other[Signal, Discord]
  end
  subgraph ona_services["Ona services"]
    EH[event-handler]
    AR[agent-runtime]
  end
  subgraph ui["UI"]
    CW[comms-web]
  end
  subgraph llm["LLM backends"]
    Ollama[Ollama]
    LlamaCpp[llama.cpp]
    API[OpenAI-compatible APIs]
  end
  Web --> EH
  TG --> EH
  WA --> EH
  Other --> EH
  CW --> EH
  EH --> AR
  AR --> Ollama
  AR --> LlamaCpp
  AR --> API
  AR --> EH
  EH --> CW
  EH --> channels
```

---

## Web & desktop

| Component | Technology | Role |
|-----------|------------|------|
| **Web UI** | **Astro** | Frontend for chat, onboarding, and settings. Static build; CodeMirror for in-app code/docs. |
| **Desktop app** | **Electron** | Wraps the web UI so you can run Ona as a desktop app (e.g. mission control, chat). |

---

## Data & storage

| Use | Technology | Notes |
|-----|------------|--------|
| **Primary database** | **SQLite** | Jobs, state, and app data. Single file; no separate DB server by default. |
| **Optional database** | **PostgreSQL** | Supported for scale or existing infra; not required for typical self-host. |
| **Vectors / RAG** | **Embeddings + vector store** | Stored in project data (e.g. SQLite-based or dedicated vector DB) for memory and knowledge search. |
| **Workspace & memory** | **Files (e.g. Markdown)** | Persistent memory and workspace content live as files under a configurable data directory. |

```mermaid
flowchart TB
  subgraph app["Ona services"]
    EH[event-handler]
    AR[agent-runtime]
  end
  subgraph storage["Storage"]
    SQL[(SQLite)]
    VEC[(Vectors / RAG)]
    FS[(Workspace & memory files)]
  end
  EH --> SQL
  AR --> SQL
  AR --> VEC
  AR --> FS
```

---

## AI & models

| Area | Technology | Role |
|------|------------|------|
| **Local inference** | **Ollama** | Easiest local LLM backend; auto-discovery of installed models. |
| **Local inference** | **llama.cpp** (GGUF) | OpenAI-compatible server for GGUF models; can run on host or in containers. |
| **APIs** | **OpenAI-compatible** | Cloud or local endpoints (OpenAI, Claude, Groq, Gemini, or local servers) via a single API shape. |
| **Routing** | **Per-agent** | Different agents (e.g. main Solin vs customer-service) can use different models and backends. |

```mermaid
flowchart LR
  subgraph agents["Agents"]
    Solin[Solin]
    CS[Customer Service]
  end
  subgraph backends["LLM backends"]
    Ollama[Ollama]
    LlamaCpp[llama.cpp]
    Cloud[Cloud APIs]
  end
  Solin --> LlamaCpp
  Solin --> Ollama
  Solin --> Cloud
  CS --> Ollama
  CS --> Cloud
```

---

## Deployment & ops

| Area | Technology | Role |
|------|------------|------|
| **Containers** | **Docker** (or **Podman**) | Default way to run Ona: one Compose file for event-handler, agent-runtime, comms-web, and optional model containers. |
| **Orchestration** | **Docker Compose** | Defines services, networks, and volumes. Optional profile for extra model containers (e.g. GGUF servers). |
| **Host / bare metal** | **Rust binaries + scripts** | You can run the same Rust binaries and web build on the host (no Docker) for development or lightweight installs. |
| **Package** | **Debian (.deb)** | Optional; build and install Ona as a system package. |

```mermaid
flowchart TB
  subgraph deploy["Deployment options"]
    Docker[Docker / Podman]
    Compose[Docker Compose]
    Host[Host binaries]
    Deb[.deb package]
  end
  subgraph stack["Ona stack"]
    EH[event-handler]
    AR[agent-runtime]
    CW[comms-web]
  end
  Docker --> Compose
  Compose --> EH
  Compose --> AR
  Compose --> CW
  Host --> EH
  Host --> AR
  Host --> CW
  Deb --> stack
```

---

## Ona Sphere (optional)

When many people (each with their own Ona) connect through Sphere:

| Component | Technology | Role |
|-----------|------------|------|
| **Gateway** | **Rust (Axum)** | Sphere gateway service: identity, routing, and policy at the edge. |
| **Sphere runtime** | **Rust** | Agent runtime and governance logic for the shared layer. |
| **Web** | **Static + small server** | Optional web UI for Sphere (e.g. Python or Node server for static assets). |

Sphere is a separate deployable; Ona works fully without it.

```mermaid
flowchart TB
  subgraph users["People"]
    U1[Person 1]
    U2[Person 2]
    U3[Person 3]
  end
  subgraph onas["Each has own Ona"]
    O1[Ona + Solin]
    O2[Ona + Solin]
    O3[Ona + Solin]
  end
  subgraph sphere["Sphere"]
    GW[Gateway]
    RT[Runtime]
    ID[Identity & policy]
  end
  U1 --> O1
  U2 --> O2
  U3 --> O3
  O1 --> GW
  O2 --> GW
  O3 --> GW
  GW --> RT
  RT --> ID
```

---

## Development & tooling

| Area | Tool / tech | Notes |
|------|-------------|--------|
| **Build** | **Cargo** | `cargo build`, workspace with shared dependencies and release profiles. |
| **Scripts** | **Bash, PowerShell** | Install, start, stop, doctor, update; cross-platform where possible. |
| **CI** | **GitHub Actions** | Build, test, and optional checks (e.g. memory leak detection). |

---

## Summary

- **Backend:** Rust (Tokio, Axum), SQLite (or Postgres), file-based memory/workspace.
- **Frontend:** Astro (web), Electron (desktop).
- **AI:** Ollama, llama.cpp, and any OpenAI-compatible API; per-agent routing.
- **Deploy:** Docker Compose (or Podman), optional .deb; host binaries for dev/simple installs.
- **Sphere:** Optional Rust-based gateway and runtime that connect multiple Onas.

For community, contributing, and policies, see [README.md](README.md) and [CONTRIBUTING.md](CONTRIBUTING.md).
