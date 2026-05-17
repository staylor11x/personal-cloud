# Architecture update checklist

<!-- Use this checklist when making any change to docs/architecture.md. Work through all three
     sections in order as part of the PR that contains the update. This is not a standalone
     document — it is a process guide. Do not commit this file to a PR; work through it
     locally or as a PR description reference. -->

---

## Pre-update checklist

Answer these questions before editing `docs/architecture.md`.

- [ ] Does this change reflect a decision that has been or will be recorded in an ADR?
  *If no: the decision must be recorded in an ADR before the architecture document is updated.
  See `docs/contributing/templates/adr-template.md`.*

- [ ] Does this change affect the architecture diagram (`docs/diagrams/architecture-v1.drawio`)?
  *If yes: plan a diagram update. Either include it in this PR or open a follow-up issue immediately.*

- [ ] Does this change require updating the `docs/registry.md` entry for `docs/architecture.md`?
  *Always yes if any content changes — version and last-verified date must be incremented.*

---

## Update checklist

- [ ] `docs/architecture.md` updated with accurate, declarative, present-tense content
- [ ] Version in the metadata block incremented — minor (`1.0 → 1.1`) for content additions or
  corrections, major (`1.1 → 2.0`) for structural rewrites or removal of substantial content
- [ ] ADR index table (Section 9) updated if any ADR changed status or a new ADR was added
- [ ] Architecture diagram updated, or a follow-up issue opened if the diagram is now out of date
- [ ] `docs/registry.md` row for `docs/architecture.md` updated — version and last-verified date

---

## Post-update checklist

- [ ] No placeholder values remain in the document — no `[PLACEHOLDER]` text, no unfilled
  HTML comment guidance notes in the document body
- [ ] All ADR links in the ADR index table (Section 9) resolve to files that exist in `docs/adrs/`
- [ ] PR description states what changed in the architecture and references the governing ADR
- [ ] No real values committed — no IP addresses, domain names, hostnames, API tokens,
  or credentials of any kind
