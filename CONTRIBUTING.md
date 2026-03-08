# Contributing to Ona

**Welcome.** We’re glad you’re here. This repo is where we build the future of multi-agent orchestration—together.

*Movement over ego. Collaboration over competition. Action over perfection.*

> **AI capabilities and risk.** Ona’s agents can run code, read and write files, access memory and personal data, and send messages on your behalf. That’s why we’re making the **lockbox** — to keep credentials and secrets out of plaintext and limit what agents can access. Treat input from channels and external sources as **untrusted**. Restrict who can talk to your bots and scope API keys. See the main Ona repo’s security doc when linked.
>
> **Alpha — controlled matters.** Ona is an **alpha** project under active development; behaviour and APIs can change. The project is under **controlled matters** (proprietary, limited distribution) for this reason. Use and contribute at your own risk; we do not recommend production reliance until we announce a stable release.

This document explains how to contribute on the **community side** (this repo). Here we accept contributions to **policies, onboarding docs, and community processes**—not to the main app code.

---

## Core philosophy

Ona’s main repository is a **factory for building functional installations**. It is not a standard “clone and run” source tree. The build process turns that source into a production-ready environment at a specific **operational path**. The installed product must be **100% functional** at that location. All developer documentation and troubleshooting assume those paths. This repo (onapublic) is the **community and maintainer** hub—policies, get-in-touch, and contributor path live here.

---

## What you can contribute here

- **Skills:** Proposals or listings for community skills (see MAINTAINERS.md or “How to add a skill” when added).
- **Install/setup ideas:** Documented as issues or short docs; actual changes to install scripts live in the main Ona repo.
- **Policies:** Code of conduct, security reporting, community expectations (via PRs to this repo).
- **Maintainer docs:** Improvements to MAINTAINERS.md, release/triage notes.

---

## What belongs in the main repo

- **App code:** Rust, TypeScript, Astro, scripts under `boot/`, `systems/`, `scripts/production/`.
- **Core docs:** ARCHITECTURE, API_MAP, INSTALLATION, SECURITY, etc.
- **Config examples:** prod.env.example, config-reference—only in the main repo.

If in doubt, open an issue in this repo and we’ll point you to the right place.

---

## How to contribute

1. Fork this repo (onapublic).
2. Create a branch (`git checkout -b topic/short-name`).
3. Edit only **allowed** content (see [PUBLIC_REPO_RULES.md](PUBLIC_REPO_RULES.md)).
4. Commit with a clear message.
5. Open a Pull Request.

We do not accept PRs that add secrets, internal paths, or proprietary code. Only content that is safe for a **public** community repo.
