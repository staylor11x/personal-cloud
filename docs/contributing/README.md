The `docs/contributing/` directory contains the reference material that defines how documentation is created and maintained in this repository. The documentation skill file at `.agents/skills/documentation/SKILL.md` is the primary resource: it encodes writing standards, document structure conventions, diagram selection rules, and maintenance protocols for use by agents performing documentation tasks. The skill file is loaded by agents on demand; it is not a guide for end users of the platform.

The `templates/` subdirectory contains the following document templates:

| Template | Purpose |
|---|---|
| [`templates/issue-template.md`](./templates/issue-template.md) | Required structure for all agent-targeted GitHub issues |
| [`templates/adr-template.md`](./templates/adr-template.md) | Required sections and metadata format for Architecture Decision Records |
| [`templates/runbook-template.md`](./templates/runbook-template.md) | Required sections and step structure for operational runbooks |
| [`templates/architecture-update.md`](./templates/architecture-update.md) | Checklist for updating `docs/architecture.md` |
