# Maintainer onboarding

**For people who release, triage, or curate content in the onapublic repo.**

---

## Role of this repo

- **onapublic** holds community-facing content only: policies, contributor/maintainer docs, code of conduct, and links to the main Ona project.
- The **main Ona repo** remains the single source of truth for the app. We do not duplicate app code or core docs here.

---

## Maintainer responsibilities (when adopted)

- **Release:** When we version this repo, tag and document what changed (e.g. CHANGELOG or release notes).
- **Triage:** Issues and PRs in onapublic—route install/code questions to the main repo; keep only community/policy content here.
- **Skills:** Document “how to add a skill” and curate a list or catalog when we add one; keep the process in this repo.
- **Docs:** Keep COMMUNITY_AND_MAINTAINERS, CONTRIBUTING, CODE_OF_CONDUCT, and this file accurate and safe for public read.

---

## What may be pushed to onapublic

Only content that passes [PUBLIC_REPO_RULES.md](PUBLIC_REPO_RULES.md): no secrets, no internal paths, no proprietary code. The main repo syncs the `onapublic/` folder to this GitHub repo via a controlled process (see main repo’s scripts and rules).

---

## Links

- [PUBLIC_REPO_RULES.md](PUBLIC_REPO_RULES.md) — What may be published here
- [COMMUNITY_AND_MAINTAINERS.md](COMMUNITY_AND_MAINTAINERS.md) — Core vs community boundary
