# How and What to Push to the Ona Public Repo — A Narrative Guide

**Last updated (UTC): 2026-03-13 15:54**

*For latest consolidated updates, see the main repo’s* `docs/development/DOCUMENT_UPDATES_REGISTRY.md`.

This document is a **presentation in long text**: it explains, in one continuous narrative, what the onapublic repo is for, what may be published there, and how to push to it safely — without using slides or bullet-only format.

---

## What this is about

The **onapublic** repo at [github.com/zerwiz/onapublic](https://github.com/zerwiz/onapublic) is the **community-facing hub** for Ona. It does not hold the main app code. It holds policies, contributor and maintainer onboarding, code of conduct, and links back to the main project. The main Ona application and all of its code live in a **separate repository**. That separation is strict: only certain content from the main repo is ever allowed to reach the public repo, and only through a controlled process. This guide explains **what** is allowed, **what** is forbidden, and **how** to publish updates.

---

## Why the split exists

The main Ona repo is the single source of truth for the application: boot scripts, systems, production configs, internal docs, and developer-only paths. Some of that is not safe or not useful to publish as-is. The public repo exists so that the community can see how to get in touch, how to contribute on the community side, and what the rules are — without ever being given secrets, internal layout, or proprietary code. So we have two rules: **only the right content** goes to the public repo, and **only the right method** is used to send it there.

---

## What may be pushed (allowed)

The contract for “what may be published” is [PUBLIC_REPO_RULES.md](PUBLIC_REPO_RULES.md). Anything that goes to the onapublic GitHub repo must follow it.

**Allowed content** includes: **Markdown docs** that are safe for public read — for example README, COMMUNITY_AND_MAINTAINERS, CONTRIBUTING, MAINTAINERS, CODE_OF_CONDUCT, PUBLIC_REPO_RULES, and similar policy or onboarding content. **Links** to the main Ona project or to official install/setup resources are fine, as long as they are not internal URLs and contain no secrets. **Skill catalogs or lists** are allowed when they contain only names, short descriptions, and links — no API keys, tokens, or internal paths. **Changelog or release notes** for the onapublic repo itself are also allowed.

So: community-facing docs, safe links, and lightweight catalogs. That is what the public repo is for.

---

## What must not be pushed (forbidden)

**Secrets** must never be published: no API keys, tokens, passwords, credentials, or any file that could contain them. **Internal paths** are not allowed — no references to private repos, internal servers, or paths that expose internal layout; public install docs may mention paths like `C:\Ona` or `/opt/ona` only when needed for public instructions, and developer-only paths must stay out. **Proprietary or private code** must not be copied from the main repo — no Ona app code, configs, or core docs unless they are explicitly approved for public mirroring. **Personal or user-specific data** beyond what is needed for public attribution (e.g. maintainer contact) must not be included.

If in doubt, keep the content in the main repo and link to it from the public repo instead of copying.

---

## Where the content lives in the main repo

In the **main Ona repository**, the only folder that is ever synced to the public repo is **`onapublic/`**. Everything that ends up on GitHub as the onapublic repo comes from that folder. No other part of the main repo is pushed to the public repo. Scripts and git hooks are in place to enforce “push only this folder” so that the full main repo is never sent to the onapublic remote.

---

## How to push: use the sync script (do not push the main repo)

You must **not** push the main Ona repo to a remote whose URL contains **onapublic**. If you add the public repo as a remote and run `git push` from the main repo to it, you would risk exposing the entire codebase. A **pre-push hook** is available to block that: when the push target is a remote URL containing “onapublic”, the hook stops the push and tells you to use the sync script instead.

The **correct way** to publish is to use the **sync script**. On Linux, macOS, or WSL you run **`./scripts/sync-onapublic.sh`** from the main Ona repo root. On Windows (PowerShell) you run **`.\scripts\sync-onapublic.ps1`**. The script clones or refreshes a copy of the public repo (for example into a temporary directory), copies **only the contents** of the main repo’s **`onapublic/`** folder into that copy (replacing existing files), and then commits and pushes from that copy to the public repo. So the public repo ever only receives what is inside `onapublic/` — nothing else.

Prerequisites: Git, and push access to the public repo (e.g. [github.com/zerwiz/onapublic](https://github.com/zerwiz/onapublic)). The script uses the remote URL from the environment variable **`ONAPUBLIC_REMOTE_URL`** if set, otherwise defaults to **`https://github.com/zerwiz/onapublic.git`**, and the branch from **`ONAPUBLIC_BRANCH`** if set, otherwise **`main`**. Full step-by-step and prerequisites are in the main repo at **`scripts/README-onapublic-sync.md`**.

---

## Install the pre-push hook (recommended)

To avoid accidentally pushing the full main repo to the public remote, install the pre-push hook. From the main Ona repo root, on Linux, macOS, or WSL, run: **`cp scripts/githooks/pre-push .git/hooks/pre-push`** and **`chmod +x .git/hooks/pre-push`**. On Windows in PowerShell: **`Copy-Item scripts\githooks\pre-push .git\hooks\pre-push`**. After that, any `git push` to a remote whose URL contains “onapublic” will be blocked with a message directing you to the sync script.

---

## Manual sync if the script is unavailable

If the sync script is not available, you can do the same steps by hand. Clone the public repo somewhere outside the main repo (e.g. `git clone https://github.com/zerwiz/onapublic.git`). Copy everything from the main repo’s **`onapublic/`** folder into the clone’s root, overwriting existing files. In the clone run **`git add -A`**, **`git status`**, then **`git commit -m "Sync from main repo onapublic/ folder"`**, and **`git push`**. Never push from the main Ona repo to a remote that points at onapublic; always push only from a clone that contains just the synced files.

---

## Who checks the rules

In the **main Ona repo**, everyone editing `onapublic/` should follow [PUBLIC_REPO_RULES.md](PUBLIC_REPO_RULES.md) and the Cursor rule **ona-public-repo-sync** so that only allowed content is ever placed in that folder. In the **onapublic repo** itself (e.g. if someone opens a pull request there), maintainers check proposed changes against PUBLIC_REPO_RULES and reject anything that adds secrets, internal paths, proprietary code, or inappropriate personal data.

---

## One-page summary

**What:** The onapublic repo holds community-facing content only (policies, contributing, maintainers, code of conduct). The main app and code stay in the main repo.

**Allowed:** Public-safe Markdown docs, safe links, skill catalogs (names/descriptions/links only), and this repo’s changelog/release notes.

**Forbidden:** Secrets, internal paths, proprietary/private code from the main repo, and unnecessary personal data.

**How:** Edit files in the main repo’s **`onapublic/`** folder, then run **`./scripts/sync-onapublic.sh`** (or the Windows PowerShell script). Do not push the main repo to an onapublic remote; use the sync script so only `onapublic/` content is pushed. Install the pre-push hook to block mistaken pushes.

**Where to read more:** [PUBLIC_REPO_RULES.md](PUBLIC_REPO_RULES.md) (what may be published), [README.md](README.md) (what’s in this repo), and in the main repo: **scripts/README-onapublic-sync.md** (sync steps) and **.cursor/rules/ona-public-repo-sync.mdc** (editor rule for onapublic).

---

*This document is the long-text “presentation” of how and what to push to the onapublic repo. For slide-style overviews of Ona and Ona Sphere, see [PRESENTATION.md](PRESENTATION.md).*
