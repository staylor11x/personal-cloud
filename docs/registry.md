# Documentation registry

> **Version:** 1.0
> **Status:** Living document — updated whenever a living document is created, modified, or removed
> **Related:** [docs/contributing/README.md](./contributing/README.md)

This file is the authoritative index of every living document in the repository. It serves two purposes: human navigation — a single place to locate any document without knowing the directory structure — and agent efficiency — a structured reference that any agent can read to understand what documentation exists, what it covers, and whether it may need updating as part of a task.

**Update requirement:** Every pull request that creates or modifies a living document must update this registry. Increment the version and update the last-verified date for any document that changed. Add a new row for any document that was created. Remove a row for any document that was deleted and note the removal in the PR description.

---

| Document | Covers | Version | Last verified | Update trigger |
|---|---|---|---|---|
| [docs/architecture.md](./architecture.md) | Platform architecture — hardware, technology stack, security model, phase sequencing rationale, and ADR index | 1.0 | 2026-05-17 | Architecture changes, new ADRs accepted, hardware inventory changes, phase transitions |
| [docs/decisions/project-approach.md](./decisions/project-approach.md) | Project operating model — AI-native workflow, tooling inventory, cost policy, per-phase definition of success, and documentation strategy | 1.0 | 2026-05-17 | Workflow or tooling changes, cost policy changes, phase completion |
| [docs/contributing/README.md](./contributing/README.md) | Purpose and contents of the docs/contributing directory | 1.0 | 2026-05-17 | Contents of docs/contributing change |
| [.agents/skills/documentation/SKILL.md](../.agents/skills/documentation/SKILL.md) | Documentation standards for agents — writing conventions, diagram selection, structure standards, and maintenance protocol | 1.0 | 2026-05-17 | Documentation conventions change or new document types are added |
| [docs/registry.md](./registry.md) | Index of all living documents with version, coverage summary, and update triggers | 1.0 | 2026-05-17 | Any living document is created, modified, or removed |
