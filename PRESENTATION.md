# Ona & Ona Sphere — Presentation

**Last updated (UTC): 2026-03-12 17:36**

This is a presentation-style overview of Ona and Ona Sphere. You can use it as speaker notes, or render it with [Marp](https://marp.app/) (add `---` between slides if your tool uses that). For full narrative and diagrams, see [WHAT_IS_ONA_AND_SPHERE.md](WHAT_IS_ONA_AND_SPHERE.md).

---

## Slide 1: Title

**Ona & Ona Sphere**

Your AI squad. Your mission. Safe for one — or many.

---

## Slide 2: The problem

- Most AI products stop at **chat**.
- Real work needs **execution**: tasks, memory, tools, many skills.
- One user is easy. **Many users on one system** need boundaries so shared intelligence doesn’t become shared private data.

---

## Slide 3: What is Ona?

**Ona = your private AI layer that gets the mission done.**

- You talk to **Solin** (your main agent).
- Solin runs a **squad** of specialists: Writer, Researcher, Developer, Marketer, etc.
- **Missions**, not just prompts: decompose work, assign agents, use memory and tools, deliver outcomes.
- **Channels:** web, terminal, Telegram, WhatsApp, Signal, Discord.
- **Self-hosted:** your machine or your VPS; local or cloud models; no vendor lock-in.

---

## Slide 4: What Ona does (summary)

| What | How |
|------|-----|
| Missions | Turn a message into a plan → tasks → specialists → results |
| Squad | One lead (Solin) + role-based agents for content, research, code, marketing, etc. |
| Memory & knowledge | Persistent memory + RAG over your docs |
| Safety | Lockbox for secrets; human-in-the-loop for sensitive actions |

---

## Slide 5: What is Ona Sphere?

**Ona Sphere = get it done safely for many users on one server.**

- When **families, teams, or companies** share one AI system, you need:
  - **Identity** — who is who
  - **Roles** — who can do what
  - **Private vs shared zones** — no cross-user data leakage
  - **Audit and policy** — what happened and who allowed it

Sphere is the **trust boundary and control plane** for multi-user Ona. It runs **standalone**; Ona does not depend on it to start or run.

---

## Slide 6: What Sphere adds (summary)

| Area | Sphere adds |
|------|-------------|
| Identity | Tenant, user, session, role — operations need valid context |
| Roles | Who can do personal vs shared vs admin actions |
| Data zones | Private (per user), shared (group), system (ops) |
| Governance agents | Gateway, lockbox, guardian — policy and security, not task execution |
| Audit | Allow/deny and sensitive events for admins |

---

## Slide 7: How they fit together

- **Ona** = execution and experience (the part people use daily).
- **Sphere** = shared-server layer (identity, permissions, governance).

**Default:** Ona runs alone; no Sphere required.

**With Sphere:** Ona still does missions and UX; Sphere handles cross-user boundaries. Start/stop independently.

**If Sphere is down:** Ona keeps working; only Sphere-backed features are skipped.

---

## Slide 8: One-line takeaway

- **Ona:** “Your private personal layer that gets the mission done.”
- **Ona Sphere:** “Get it done safely for many users on one shared server.”

Sphere is **optional**. Ona works fully on its own.

---

## Slide 9: Get in touch

- **Community hub:** this repo (onapublic) — policies, contributing, maintainers.
- **Docs:** [WHAT_IS_ONA_AND_SPHERE.md](WHAT_IS_ONA_AND_SPHERE.md), [README.md](README.md), [CONTRIBUTING.md](CONTRIBUTING.md).
- **Main project:** See the main Ona repository for install, setup, and architecture (linked when available).
- **Contact:** [Discord](https://discord.com/invite/p74cGwrdPd) · [WhyNot Productions](https://whynotproductions.netlify.app/) · Zerwiz (Josef Lindbom) — [josef.lindbom@gmail.com](mailto:josef.lindbom@gmail.com).

---

*For detailed narrative, diagrams, and tables, see [WHAT_IS_ONA_AND_SPHERE.md](WHAT_IS_ONA_AND_SPHERE.md).*
