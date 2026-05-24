# Personal Cloud Platform

A self-hosted, cloud-native internal developer platform running on commodity hardware, providing personal cloud services and a fully instrumented GitOps-driven CI/CD pipeline.

> **Version:** 1.0
> **Status:** Living document — updated as the platform evolves
> **Architecture:** [docs/architecture.md](docs/architecture.md)

---

## Overview

The platform runs on a single-node Kubernetes cluster hosted on a Dell laptop, with a Raspberry Pi operating independently as a network edge node. It provides personal cloud services — photo management, file sync, media streaming, and automated backup — alongside a complete observability and GitOps deployment stack. All cluster state is managed declaratively through Git; no manual cluster operations are performed in normal operation.

---

## Repository structure

| Directory | Purpose |
|---|---|
| `.github/` | GitHub config: Actions, issue/PR templates, agent instructions |
| `.github/agents/` | Agent instruction files — load the relevant file for each task |
| `docs/` | All documentation |
| `docs/adrs/` | Architecture Decision Records |
| `docs/runbooks/` | Operational runbooks |
| `docs/diagrams/` | Architecture diagrams (.drawio source + exported .png) |
| `docs/contributing/` | Documentation standards, templates, and contributing guides |
| `docs/registry.md` | Living documentation registry — updated when docs change |
| `infrastructure/` | Base cluster config and node provisioning scripts |
| `kubernetes/` | All Kubernetes manifests and Kustomize overlays |
| `kubernetes/apps/` | Per-application ArgoCD Application definitions |
| `kubernetes/core/` | Core platform services (ingress, cert-manager, Longhorn, etc.) |
| `helm-charts/` | Custom Helm charts |
| `terraform/` | Cloud resource definitions (Phase 5+) |
| `monitoring/` | Prometheus rules, Grafana dashboards, Alertmanager config |
| `platform-cli/` | Platform CLI source |
| `scripts/` | Utility and automation scripts |

---

## Key documents

| Document | Location | Purpose |
|---|---|---|
| Platform architecture | [docs/architecture.md](docs/architecture.md) | Hardware inventory, technology stack, security model, phase sequencing, and ADR index |
| Project approach | [docs/decisions/project-approach.md](docs/decisions/project-approach.md) | Operating model, AI-native workflow, tooling inventory, and per-phase success criteria |
| ADRs | [docs/adrs/](docs/adrs/) | Architecture Decision Records — one per significant technology choice |
| Runbooks | [docs/runbooks/](docs/runbooks/) | Operational procedures for common tasks and incident response |
| Documentation contributing guide | [docs/contributing/](docs/contributing/) | Writing standards, templates, and documentation maintenance protocol |
| Living document registry | [docs/registry.md](docs/registry.md) | Index of all living documents with version, coverage, and update triggers |
| Architecture diagram | [docs/diagrams/architecture-v1.drawio.png](docs/diagrams/architecture-v1.drawio.png) | Visual overview of the platform architecture |

---

## Architecture diagram

![Platform architecture](docs/diagrams/architecture-v1.png)

Figure 1 — Platform architecture. Source: `docs/diagrams/architecture-v1.drawio`.

---

## Getting started

Cluster provisioning documentation will be added in Phase 1.

---

## Security

All remote access to the platform is via Tailscale VPN — no service is exposed to the public internet directly. No credentials, keys, or real environment values are committed to this repository — see [docs/architecture.md](docs/architecture.md) for the full security model.
