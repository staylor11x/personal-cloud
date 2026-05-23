# Documentation registry

> **Version:** 1.3
> **Status:** Living document — updated whenever a living document is created, modified, or removed
> **Related:** [docs/contributing/README.md](./contributing/README.md)

This file is the authoritative index of every living document in the repository. It serves two purposes: human navigation — a single place to locate any document without knowing the directory structure — and agent efficiency — a structured reference that any agent can read to understand what documentation exists, what it covers, and whether it may need updating as part of a task.

**Update requirement:** Every pull request that creates or modifies a living document must update this registry. Increment the version and update the last-verified date for any document that changed. Add a new row for any document that was created. Remove a row for any document that was deleted and note the removal in the PR description.

---

| Document | Covers | Version | Last verified | Update trigger |
|---|---|---|---|---|
| [docs/architecture.md](./architecture.md) | Platform architecture — hardware, technology stack, security model, phase sequencing rationale, and ADR index | 1.0 | 2026-05-17 | Architecture changes, new ADRs accepted, hardware inventory changes, phase transitions |
| [docs/decisions/ai-engineering-approach.md](./decisions/ai-engineering-approach.md) | AI engineering governance — usage principles, tool roles, context-loading model, and issue quality contract | 1.1 | 2026-05-23 | AI workflow changes, agent context model changes, tooling policy changes, or issue quality requirements change |
| [docs/decisions/project-approach.md](./decisions/project-approach.md) | Project operating model — AI-native workflow, tooling inventory, cost policy, per-phase definition of success, and documentation strategy | 1.1 | 2026-05-23 | Workflow or tooling changes, cost policy changes, phase completion |
| [docs/contributing/README.md](./contributing/README.md) | Purpose and contents of the docs/contributing directory | 1.0 | 2026-05-17 | Contents of docs/contributing change |
| [.agents/skills/documentation/SKILL.md](../.agents/skills/documentation/SKILL.md) | Documentation standards for agents — writing conventions, diagram selection, structure standards, and maintenance protocol | 1.0 | 2026-05-17 | Documentation conventions change or new document types are added |
| [docs/contributing/templates/adr-template.md](./contributing/templates/adr-template.md) | Template for Architecture Decision Records — required sections, metadata format, and guidance notes | 1.0 | 2026-05-17 | ADR process changes or required sections are added or removed |
| [docs/contributing/templates/runbook-template.md](./contributing/templates/runbook-template.md) | Template for operational runbooks — required sections, step structure, and guidance notes | 1.0 | 2026-05-17 | Runbook process changes or required sections are added or removed |
| [docs/contributing/templates/architecture-update.md](./contributing/templates/architecture-update.md) | Checklist for updating docs/architecture.md — pre-update, update, and post-update steps | 1.0 | 2026-05-17 | Architecture update process changes |
| [.github/PULL_REQUEST_TEMPLATE.md](../.github/PULL_REQUEST_TEMPLATE.md) | PR template — required sections and documentation checklist enforced on every pull request | 1.0 | 2026-05-17 | PR process changes or checklist items are added or removed |
| [docs/registry.md](./registry.md) | Index of all living documents with version, coverage summary, and update triggers | 1.3 | 2026-05-23 | Any living document is created, modified, or removed |
| [README.md](../README.md) | Repository landing page — platform description, repository structure, key document navigation, architecture diagram, and security overview | 1.0 | 2026-05-23 | Platform name changes, repository structure changes, key documents added or removed |
