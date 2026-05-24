# Documentation registry

> **Version:** 2.1
> **Status:** Living document — updated whenever a living document is created, modified, or removed
> **Related:** [docs/contributing/README.md](./contributing/README.md)

This file is the authoritative index of every living document in the repository. It serves two purposes: human navigation — a single place to locate any document without knowing the directory structure — and agent efficiency — a structured reference that any agent can read to understand what documentation exists, what it covers, and whether it may need updating as part of a task.

**Update requirement:** Every pull request that creates or modifies a living document must update this registry. Increment the version and update the last-verified date for any document that changed. Add a new row for any document that was created. Remove a row for any document that was deleted and note the removal in the PR description.

---

| Document | Covers | Version | Last verified | Update trigger |
|---|---|---|---|---|
| [docs/architecture.md](./architecture.md) | Platform architecture — hardware, technology stack, security model, phase sequencing rationale, and ADR index | 1.0 | 2026-05-17 | Architecture changes, new ADRs accepted, hardware inventory changes, phase transitions |
| [docs/adrs/ADR-001.md](./adrs/ADR-001.md) | ADR-001: Cluster distribution — evaluation of k3s, Talos Linux, and kubeadm; decision to use k3s on Ubuntu Server | 1.0 | 2026-05-24 | Kubernetes distribution changes or hardware profile changes significantly |
| [docs/adrs/ADR-008.md](./adrs/ADR-008.md) | ADR-008: CI/CD architecture — dual-runner strategy, bootstrap dependency, GitHub-hosted runners for CI, self-hosted runner for CD | 1.0 | 2026-05-24 | CI/CD runner strategy changes, GitHub Actions workflow structure changes, or Phase 2 self-hosted runner setup changes |
| [docs/adrs/ADR-009.md](./adrs/ADR-009.md) | ADR-009: AI tooling strategy — Copilot, CodeRabbit, GitHub Actions CI/CD, dual-runner strategy, and Ollama stretch goal | 1.0 | 2026-05-23 | AI tooling decisions change or Ollama stretch goal is activated |
| [docs/decisions/ai-engineering-approach.md](./decisions/ai-engineering-approach.md) | AI engineering governance — usage principles, tool roles, context-loading model, agent orchestration flow, and issue quality contract | 1.2 | 2026-05-24 | AI workflow changes, agent context model changes, tooling policy changes, or issue quality requirements change |
| [docs/decisions/project-approach.md](./decisions/project-approach.md) | Project operating model — AI-native workflow, tooling inventory, cost policy, per-phase definition of success, and documentation strategy | 1.1 | 2026-05-23 | Workflow or tooling changes, cost policy changes, phase completion |
| [docs/contributing/README.md](./contributing/README.md) | Purpose and contents of the docs/contributing directory | 1.1 | 2026-05-23 | Contents of docs/contributing change |
| [.agents/skills/documentation/SKILL.md](../.agents/skills/documentation/SKILL.md) | Documentation standards for agents — writing conventions, diagram selection, structure standards, and maintenance protocol | 1.0 | 2026-05-17 | Documentation conventions change or new document types are added |
| [docs/contributing/templates/issue-template.md](./contributing/templates/issue-template.md) | Template for agent-targeted GitHub issues — required sections, phase and agents metadata, and documentation update criterion | 1.1 | 2026-05-24 | Issue process changes or required sections are added or removed |
| [docs/contributing/templates/adr-template.md](./contributing/templates/adr-template.md) | Template for Architecture Decision Records — required sections, metadata format, and guidance notes | 1.0 | 2026-05-17 | ADR process changes or required sections are added or removed |
| [docs/contributing/templates/runbook-template.md](./contributing/templates/runbook-template.md) | Template for operational runbooks — required sections, step structure, and guidance notes | 1.0 | 2026-05-17 | Runbook process changes or required sections are added or removed |
| [docs/contributing/templates/architecture-update.md](./contributing/templates/architecture-update.md) | Checklist for updating docs/architecture.md — pre-update, update, and post-update steps | 1.0 | 2026-05-17 | Architecture update process changes |
| [.github/PULL_REQUEST_TEMPLATE.md](../.github/PULL_REQUEST_TEMPLATE.md) | PR template — required sections and documentation checklist enforced on every pull request | 1.0 | 2026-05-17 | PR process changes or checklist items are added or removed |
| [docs/registry.md](./registry.md) | Index of all living documents with version, coverage summary, and update triggers | 2.1 | 2026-05-24 | Any living document is created, modified, or removed |
| [README.md](../README.md) | Repository landing page — platform description, repository structure, key document navigation, architecture diagram, and security overview | 1.0 | 2026-05-23 | Platform name changes, repository structure changes, key documents added or removed |
| [scripts/README.md](../scripts/README.md) | Usage reference for scripts/ — upload-issues.sh and branch-name.sh interface, input file format, and operational notes | 1.1 | 2026-05-24 | Scripts added, removed, or their interface changes |
| [.github/agents/infrastructure-agent.md](../.github/agents/infrastructure-agent.md) | Infrastructure agent instructions — role (subagent only), absolute rules, manifest and Helm standards, phase constraints, and escalation conditions | 1.1 | 2026-05-24 | Infrastructure conventions change, phase scope changes, or new constraint types are added |
| [.github/agents/application-agent.md](../.github/agents/application-agent.md) | Application agent instructions — role (subagent only), absolute rules, deployment and backup standards, phase constraints, and escalation conditions | 1.1 | 2026-05-24 | Application deployment conventions change, new applications added to ADR-005, or phase scope changes |
| [.github/agents/documentation.agent.md](../.github/agents/documentation.agent.md) | Documentation agent instructions — role (subagent only), absolute rules, document standards, and return value protocol | 1.0 | 2026-05-24 | Documentation conventions change or new document types are added |
| [.github/agents/platform.agent.md](../.github/agents/platform.agent.md) | Platform orchestrator agent — single entry point for all issues, specialist delegation order, escalation handling, and GitOps handoff | 1.0 | 2026-05-24 | Orchestration workflow changes, new specialist agents added, or classification logic changes |
| [.github/agents/git-ops.agent.md](../.github/agents/git-ops.agent.md) | GitOps agent instructions — role (subagent only), branch naming via scripts/branch-name.sh, commit message format, and PR creation via GitHub MCP | 1.0 | 2026-05-24 | Git workflow changes, branch naming conventions change, or PR template changes |
