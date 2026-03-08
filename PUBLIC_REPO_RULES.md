# Public repo rules

**What may be published to the onapublic GitHub repo.**

This file is the contract for content in **onapublic**. Anything pushed to [github.com/zerwiz/onapublic](https://github.com/zerwiz/onapublic) must follow these rules.

---

## Allowed

- **Markdown docs** that are safe for public read: README, COMMUNITY_AND_MAINTAINERS, CONTRIBUTING, MAINTAINERS, CODE_OF_CONDUCT, PUBLIC_REPO_RULES, and similar policy/onboarding content.
- **Links** to the main Ona project or official install/setup resources (no internal URLs or secrets).
- **Skill catalogs or lists** (names, short descriptions, links only—no keys or paths).
- **Changelog or release notes** for this repo only.

---

## Not allowed

- **Secrets:** API keys, tokens, passwords, credentials, or any file that could contain them.
- **Internal paths:** References to private repos, internal servers, or paths that expose internal layout (e.g. `C:\Ona`, `/opt/ona` only when needed for public install docs; no developer-only paths).
- **Proprietary or private code:** No copy of Ona app code, configs, or core docs from the main repo unless they are explicitly approved for public mirroring.
- **Personal or user-specific data:** No names, emails, or identifiers beyond what is needed for public attribution.

---

## Enforcement

- **In the main Ona repo:** Only the contents of the `onapublic/` folder are synced to the public repo. Scripts and git hooks enforce “push only this folder.” See the main repo’s `.cursor/rules` and `scripts/` for sync rules and the push process.
- **In this repo (onapublic):** PRs that add disallowed content will be rejected. Maintainers check against this file before merging.

---

## Updates

Changes to PUBLIC_REPO_RULES.md itself must be reviewed to ensure they don’t weaken safety. When in doubt, keep content in the main repo and link from here.
