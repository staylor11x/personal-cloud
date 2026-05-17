# Project Approach

> **Version:** 1.0
> **Status:** Living document
> **Related:** [`docs/architecture.md`](../architecture.md) · [`docs/contributing/`](../contributing/)

---

## Table of Contents

1. [AI-native engineering workflow](#1-ai-native-engineering-workflow)
2. [AI tooling inventory](#2-ai-tooling-inventory)
3. [Cost management policy](#3-cost-management-policy)
4. [Definition of technical success](#4-definition-of-technical-success)
5. [Documentation strategy](#5-documentation-strategy)

---

## 1. AI-native engineering workflow

This project is operated AI-natively from day one. AI tooling is embedded across
planning, implementation, review, and deployment — not used only for code
generation. A human approval gate exists at the review stage. All other stages
are automated or AI-assisted.

The governing principle is: AI handles repetitive, mechanical, and first-draft
work. Human judgement governs approval, architectural decisions, and learning.
Every AI action that touches the codebase or the cluster is traceable, reviewable,
and reversible.

### End-to-end workflow

| Stage | Description | Actor |
|---|---|---|
| **1. Planning** | Work is described to Copilot Chat in VS Code. It assists in breaking the work into a GitHub Milestone and well-structured issues with acceptance criteria, context, and scope boundaries. | Human + Copilot Chat |
| **2. Issue creation** | `scripts/bootstrap-agent-issue.sh` creates the issue via the GitHub CLI with the required context block pre-filled. Milestone is assigned automatically. | Bash script + gh CLI |
| **3. Implementation** | The Copilot coding agent is assigned the issue. It checks out a branch, implements the work, and opens a PR autonomously. | Copilot coding agent |
| **4. CI pipeline** | GitHub Actions triggers on the PR. Linting, manifest validation, secret scanning, and Helm lint all run. Results are posted to the PR. | GitHub Actions (GitHub-hosted runner) |
| **5. AI review** | Copilot PR review and CodeRabbit both post automated review comments before the human reads the diff. | Copilot + CodeRabbit |
| **6. Human review** | The diff is read, AI review comments are considered, and changes are requested or the PR is approved. This is the only mandatory human gate before merge. | Human |
| **7. Merge and deploy** | On merge to main, ArgoCD detects the change and reconciles the cluster. No manual `kubectl apply`. | ArgoCD (GitOps) |
| **8. Smoke test** | A post-deploy GitHub Actions job runs a smoke test via the self-hosted runner. Result is posted as a PR comment. | GitHub Actions (self-hosted runner) |
| **9. Observability** | Grafana dashboards reflect the change. A deployment annotation is created. Prometheus alerts fire if something breaks post-deploy. | Prometheus + Grafana |

### CI pipeline detail

**On every pull request — GitHub-hosted runner:**

- YAML and Markdown linting
- Kubernetes manifest validation via `kubeval`
- Helm chart linting via `helm lint`
- Secret scanning via Gitleaks — fails the PR if any credential pattern is detected
- ADR format check — verifies every new ADR follows the required template
- Copilot PR review posts inline comments automatically
- CodeRabbit posts a full review summary with change analysis

**On merge to main — self-hosted runner on k3s cluster:**

- ArgoCD sync triggered — cluster state reconciled to match new Git state
- Post-deploy smoke test — HTTP health checks against all affected services
- Result posted as a comment on the merged PR
- Grafana deployment annotation created

**On schedule — weekly, GitHub-hosted runner:**

- Dependabot dependency review digest posted as an issue comment
- Cost log reminder — automated issue prompts update of `docs/cost-log.md`
- Stale issue detection — flags issues open longer than 30 days with no activity

### Issue quality and agent performance

The single largest determinant of Copilot coding agent output quality is issue
quality. Vague issues produce vague implementations. The
`scripts/bootstrap-agent-issue.sh` script enforces a required context block on
every agent-targeted issue. It prompts for title, acceptance criteria, files
likely affected, and constraints, then creates the issue, assigns it to the
Copilot agent, and links it to the active milestone.

Every agent-targeted issue must contain:

- **Title** — imperative mood, specific and scoped
- **Context** — why this work is needed and which phase it belongs to
- **Acceptance criteria** — numbered list of testable conditions
- **Files likely affected** — scopes the agent's search space
- **Constraints** — explicit things the agent must not do
- **ADR reference** — which ADR governs this work, if applicable
- **Agent instructions** — which agent file to load: e.g. `.github/agents/documentation-agent.md`

---

## 2. AI tooling inventory

All tooling costs are bounded. The AI-native workflow described in this document
costs nothing beyond the existing GitHub Copilot Individual subscription.

| Tool | Role | Cost |
|---|---|---|
| GitHub Copilot Individual | In-editor completions, Copilot Chat for planning, coding agent for autonomous implementation, PR review | Existing subscription — no additional cost |
| Copilot coding agent | Assigned a GitHub issue, autonomously implements in a branch and opens a PR | Included in Copilot Individual |
| Copilot PR review | Automatic inline review comments on every PR | Included in Copilot Individual |
| CodeRabbit | Deep AI PR review — line-by-line analysis, summary, change impact assessment | Free tier for public open-source repositories |
| GitHub Actions | All CI/CD orchestration — linting, validation, secret scanning, smoke tests | Free for public repositories (unlimited minutes) |
| GitHub CLI (`gh`) | Used in automation scripts for issue creation, milestone management, PR operations | Free |
| Dependabot | Automated dependency update PRs — built into GitHub, zero configuration | Free |
| Gitleaks | Secret scanning on every PR — blocks accidental credential commits | Free open-source, runs in Actions |
| Ollama + local LLM | **Stretch goal (Phase 4+):** on-cluster inference for commit messages, issue summarisation, changelog generation | Free to run — hardware-constrained |

---

## 3. Cost management policy

The following rules govern all cloud spend on this project. They are policies,
not guidelines — no exceptions without a documented architectural decision.

### Billing controls — must exist before any cloud resource is provisioned

- AWS Billing Alert configured at £5/month before any AWS resource is created
- AWS Billing Alert configured at £15/month before any AWS resource is created
- AWS Budget hard cap set at £20/month — any forecast exceeding this triggers immediate review and resource teardown if necessary
- GCP free tier only — no billable GCP resources unless a specific, documented experiment explicitly justifies the spend

### Provisioning rules

- All cloud resources are managed via Terraform/OpenTofu — no manual console provisioning under any circumstances
- Resources are destroyed after experiments conclude — no idle cloud resources are permitted to persist
- A running cost log is maintained at `docs/cost-log.md` and updated at least monthly

### Cost log format

`docs/cost-log.md` records actual spend per month per service. It is updated
manually on the first of each month and automatically prompted by a scheduled
GitHub Actions workflow. Entries that show unexpected spend trigger an immediate
review of active resources.

---

## 4. Definition of technical success

The following statements define completion for each phase. Each is a verifiable
condition, not an aspiration. A phase is not complete until all conditions for
that phase are met.

### Phase 1 — Foundations

- A k3s single-node cluster is running on the Dell laptop and accessible via Tailscale VPN from at least one remote device
- ArgoCD is deployed and managing at least one real workload declaratively from the Git repository
- No workload in the cluster was deployed using manual `kubectl apply` after ArgoCD was installed
- ADR-001 (cluster distribution) and ADR-002 (GitOps tooling) are written, accepted, and committed to `docs/adrs/`
- ADR-008 (CI/CD architecture) is written, accepted, and committed to `docs/adrs/`
- The GitHub repository contains the agreed directory structure with `infrastructure/`, `kubernetes/`, and `docs/` populated
- RB-001 (cluster node recovery) is written and has been tested at least once

### Phase 2 — Core platform services

- Traefik ingress is routing internal traffic and all services are reachable via HTTPS with valid Let's Encrypt certificates
- Longhorn is provisioning persistent volumes and at least one stateful workload is using a Longhorn-backed PVC
- MinIO is running and accessible via its S3-compatible API
- Prometheus is scraping cluster and node metrics; Grafana dashboards are showing real data
- Loki is aggregating logs from all running services
- Authentik SSO is protecting at least two internal services — neither is accessible without authentication
- A self-hosted GitHub Actions runner is running on the cluster and successfully executing CI jobs
- Sealed Secrets is managing at least one real secret — no plaintext secrets exist in the repository
- ADR-003 and ADR-004 are written, accepted, and committed
- RB-002 (ArgoCD recovery), RB-004 (certificate renewal failure), RB-005 (observability stack recovery), and RB-006 (adding a new application) are written and tested

### Phase 3 — Applications

- Immich is deployed and the personal photo library is accessible and searchable
- The DAS is mounted read-only by the Immich workload — this mount happened only after RB-003 was written and a full backup-restore cycle was executed and documented
- A full backup-and-restore cycle for the photo library has been executed end-to-end and the result is documented in RB-003
- Nextcloud is deployed and in daily use for at least one real workflow (documents, notes, or file sync)
- Jellyfin is deployed and at least one media file is streamable from a device on the local network
- Automated backups are running on a documented schedule and have been verified by a successful restore test
- ADR-005 (application selection) is written, accepted, and committed

### Phase 4 — Platform engineering features

- A platform CLI exists at `platform-cli/` and is documented in `docs/`
- At least two reusable Helm chart templates exist in `helm-charts/`
- A new application can be deployed end-to-end using only the platform CLI and a Git pull request — no direct cluster access required
- Prometheus alerting is firing correctly on at least two real conditions (node memory pressure and disk usage)
- ADR-006 (platform CLI design) is written, accepted, and committed

### Phase 5 — Hybrid cloud

- At least one cloud resource (S3 bucket or equivalent) is managed via Terraform/OpenTofu and committed to `terraform/`
- Remote backup pipeline to AWS S3 is operational and has been verified by a successful restore from S3
- AWS billing alerts are configured and have been tested
- A disaster recovery scenario has been executed: the cluster rebuilt from scratch using only the Git repository and cloud-stored backups
- ADR-007 (hybrid cloud architecture) is written, accepted, and committed

---

## 5. Documentation strategy

Documentation is a first-class engineering concern on this project, treated with
the same rigour as code. Every significant architectural decision is recorded in
an Architecture Decision Record before implementation begins. Every operational
procedure is written as a runbook and tested before being marked active. The
living documentation registry at `docs/registry.md` maintains an index of every
document in the repository, tracking what each covers and when it was last
verified.

Documentation is maintained through three mechanisms: acceptance criteria on
every issue require relevant documents to be updated as part of the work; the PR
template includes a mandatory documentation checklist that must be completed
before merge; and a dedicated documentation agent
(`.github/agents/documentation-agent.md`) is available to create and update
documents as an assigned task. The documentation skill file at
`.agents/skills/documentation/SKILL.md` defines the conventions, tone,
structure, and diagram standards that all documentation in this repository
follows — whether written by a human or an agent.