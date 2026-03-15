# What Are Ona and Ona Sphere?

**Last updated (UTC): 2026-03-15**

This document explains, in plain language, what **Ona** and **Ona Sphere** are and how they fit together. Think of it as the “what is this?” guide for the project.

---

## In one sentence

- **Ona** is your private AI layer: you talk to your agent (Solin), who gets work done with a squad of specialists. It runs on your machine or your server. Everyone has their own Ona and their own Solin.
- **Ona Sphere** is what **connects the Onas**: when many people (each with their own Ona) need to work together, they connect their Onas to Sphere. Sphere adds identity, permissions, and governance so that shared intelligence does not mean shared private data.

**Together:** Ona = “get it done”; Sphere = “what connects the Onas when many people need to work together.” Sphere is optional; Ona works fully on its own.

---

## The big picture

Most AI products stop at chat. **Ona is built for execution.** You give it a mission; it breaks the work into tasks, assigns specialist agents, uses memory and tools, and returns real outcomes. That can happen on the web, in the terminal, or through channels like Telegram and WhatsApp.

**Everyone has their own Ona and their own Solin.** When those people need to work together or share a governed space, their Onas **connect to a Sphere**. **Sphere is what connects the Onas**: identity, roles, private vs shared zones, and server-level governance so one user’s data and actions don’t leak into another’s.

```mermaid
flowchart TB
  subgraph user1["Person 1"]
    O1[Ona]
    S1[Solin + squad]
  end
  subgraph user2["Person 2"]
    O2[Ona]
    S2[Solin + squad]
  end
  subgraph user3["Person 3"]
    O3[Ona]
    S3[Solin + squad]
  end
  subgraph sphere["Ona Sphere — connects the Onas"]
    Identity[Identity & roles]
    Policy[Policy & audit]
    Zones[Private / shared zones]
  end
  O1 --> S1
  O2 --> S2
  O3 --> S3
  O1 --> sphere
  O2 --> sphere
  O3 --> sphere
```

---

## What is Ona?

Ona is the **execution layer** and the **daily experience**. It is the private, personal AI system you interact with.

### In plain words

- You talk to **Solin** (your main agent).
- Solin coordinates a **squad of specialists** (Writer, Researcher, Developer, Marketer, etc.) to do the work.
- Work is organized as **missions** and **jobs**: not one-off prompts, but tasks with memory, tools, and follow-up.
- You can use it from **web, terminal, Telegram, WhatsApp, Signal, Discord** — same mission system everywhere.
- It runs **locally or on your own server** (VPS). Self-hosted; you can use local models (Ollama, llama.cpp) or cloud APIs. No vendor lock-in.

### What Ona does

| Area | What it does |
|------|----------------|
| **Missions** | Turns your message into a real plan: understand intent, break into tasks, assign to specialists, combine results. |
| **Squad** | One lead (Solin) + specialists (Writer, Researcher, Developer, Marketer, etc.) so complex work is done by the right “role.” |
| **Channels** | Web app, desktop app, CLI, Telegram, WhatsApp, Signal, Discord — one system, many ways in. |
| **Memory & knowledge** | Persistent memory, RAG (search over your docs), so context carries across conversations. |
| **Tools & safety** | Connects to real tools and services; uses a lockbox for secrets; can ask for human approval for sensitive actions. |

So: **Ona is the part people use every day** — the agent, the missions, the memory, the channels. It is the “private personal layer.”

---

## What is Ona Sphere?

Ona Sphere is the **layer that connects the Onas**. Everyone has their own Ona (and their own Solin); when they need to work together or share a governed space, their Onas connect to Sphere. Sphere provides identity, boundaries, and shared zones so one person’s data and actions don’t leak into another’s.

### In plain words

- **Ona** = your brain and workflow (missions, agents, memory). Each person has their own.
- **Sphere** = what connects the Onas: identity, roles, and boundaries so many people (each with their own Ona) can share a governed space without seeing each other’s private data or overstepping permissions.

Sphere is built for cases where you need:

- **Shared infrastructure** — one server for family, team, or company.
- **Strict isolation** — your data stays yours; others don’t see it.
- **Roles and permissions** — not everyone has the same power (e.g. admins vs members).
- **Audit and policy** — who did what, and enforcement of rules.

So: **Sphere is what connects the Onas — the trust boundary and control plane when many people (each with their own Ona) need to work together.**

### What Sphere adds

| Area | What it adds |
|------|--------------|
| **Identity** | Tenant, user, session, role — operations need valid context or they can be denied. |
| **Roles** | Who can do what (personal vs shared vs admin actions). |
| **Data zones** | Private (per user), shared (group/company), system (operations) — no accidental cross-user leakage. |
| **Server agents** | Dedicated governance agents (e.g. gateway, lockbox, guardian) for policy and security, not task execution. |
| **Audit** | Record of allow/deny and sensitive events so admins can see what happened and why. |

Sphere runs **standalone**: it can be up when individual Onas are down, and vice versa. When Sphere is enabled, each Ona connects to it for cross-user and policy-sensitive operations; when Sphere is unreachable, each Ona still runs and only skips those Sphere-backed features.

---

## How they work together

```mermaid
flowchart TB
  subgraph ona1["Your Ona"]
    You[You]
    Solin[Solin + squad]
    Missions[Missions, jobs, memory]
    Channels[Web, Telegram, etc.]
  end
  subgraph ona2["Another person's Ona"]
    Them[Them]
    Solin2[Solin + squad]
  end
  subgraph sphere["Sphere — connects the Onas"]
    Identity[Identity & roles]
    Policy[Policy & audit]
    Zones[Private / shared zones]
  end
  You --> Channels
  Channels --> Solin
  Solin --> Missions
  ona1 --> sphere
  ona2 --> sphere
  Identity --> Policy
  Policy --> Zones
```

- **Default:** You run your own Ona. One person, one Ona, one Solin. No Sphere required.
- **With Sphere:** Each person still has their own Ona and Solin. Those Onas connect to Sphere; Sphere connects the Onas and provides identity, permissions, and shared boundaries. Startup and lifecycle stay independent: you can start/stop Ona and Sphere separately.
- **If Sphere is down:** Each Ona keeps working for that person’s missions, jobs, and channels; it only skips Sphere-backed features and logs a warning.

So you can grow from “just me and my agent” to “many people, each with their own Ona, connected through Sphere” when you need that.

---

## One-line summary

| Product | One line |
|---------|----------|
| **Ona** | Your private personal layer that gets the mission done. Everyone has their own. |
| **Ona Sphere** | What connects the Onas — identity, boundaries, and governance when many people (each with their own Ona) work together. |

---

## Where to go next

- **Community and contributing:** [CONTRIBUTING.md](CONTRIBUTING.md), [COMMUNITY_AND_MAINTAINERS.md](COMMUNITY_AND_MAINTAINERS.md).
- **What’s in this repo:** [README.md](README.md) — policies, maintainers, get in touch.
- **Main project:** For install, setup, API, and architecture, see the main Ona repository when linked.
