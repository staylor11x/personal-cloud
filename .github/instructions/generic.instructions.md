---
description: Describe when these instructions should be loaded by the agent based on task context
# applyTo: 'Describe when these instructions should be loaded by the agent based on task context' # when provided, instructions will automatically be added to the request context when the pattern matches an attached file
---

<!-- Tip: Use /create-instructions in chat to generate content with agent assistance -->

# Copilot Instructions

These instructions apply to every agent interaction in this repository without exception.
They are intentionally minimal. Task-specific behaviour is defined in the relevant agent file under `.github/agents/`.

---

## Security — absolute rules

- Never commit real values of any kind: IP addresses, domain names, hostnames, API tokens, passwords, TLS keys, Tailscale keys, or session secrets
- All secrets use placeholder syntax: `${SECRET_NAME}` in manifests, `<redacted>` in docs
- Never mount, write to, or modify the DAS in any task — see `docs/architecture.md#das-safety-policy`
- Never provision cloud resources manually — all cloud infrastructure is managed via Terraform

---

## Repository structure

```
.github/                  # GitHub config: Actions, issue/PR templates, agent instructions
.github/agents/           # Agent instruction files — load the relevant file for your task
docs/                     # All documentation
docs/adrs/                # Architecture Decision Records
docs/runbooks/            # Operational runbooks
docs/diagrams/            # Architecture diagrams (.drawio source + exported .png)
docs/contributing/        # Documentation skill file and templates
docs/registry.md          # Living documentation registry — update when docs change
infrastructure/           # Base cluster config and node provisioning scripts
kubernetes/               # All Kubernetes manifests and Kustomize overlays
kubernetes/apps/          # Per-application ArgoCD Application definitions
kubernetes/core/          # Core platform services (ingress, cert-manager, Longhorn, etc.)
helm-charts/              # Custom Helm charts
terraform/                # Cloud resource definitions (Phase 5+)
monitoring/               # Prometheus rules, Grafana dashboards, Alertmanager config
platform-cli/             # Platform CLI source
scripts/                  # Utility and automation scripts
```

---

## Universal behaviour rules

- If uncertain about scope, intent, or safety: add a comment on the issue and stop. Do not proceed and correct later.
- Do not modify files outside the scope defined in the issue. If related files need changing, flag them in a comment.
- Every PR must update `docs/registry.md` if any living document was created or modified.
- ADR references must be valid. Do not reference an ADR that does not exist. If a decision needs an ADR, note it in the PR description.
- All documentation is written in Markdown. No Word documents, no PDFs, no HTML files in the docs tree.

---

## Agent instruction files

Load the relevant file at the start of every task:

| Task type | Agent instruction file |
|---|---|
| Documentation | `.github/agents/documentation-agent.md` |
| Infrastructure / Kubernetes | `.github/agents/infrastructure-agent.md` *(Phase 1)* |
| Application deployment | `.github/agents/application-agent.md` *(Phase 3)* |
| Platform CLI | `.github/agents/platform-cli-agent.md` *(Phase 4)* |
