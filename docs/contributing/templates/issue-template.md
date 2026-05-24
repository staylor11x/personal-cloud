# Issue Template

> This template defines the required structure for all agent-targeted issues
> in this repository. AI tools generating issues must follow this format exactly.
> Human-created issues should follow it where possible.
>
> Remove all HTML comments and guidance text before uploading to GitHub.

---

<!-- ================================================================
TITLE GUIDANCE
- Imperative mood: "Deploy Longhorn storage class" not "Longhorn deployment"
- Specific and scoped: one clear deliverable per issue
- No phase prefix in the title — phase is captured in the body
================================================================ -->

## Context

<!-- Why is this work needed? What problem does it solve?
     Which phase does it belong to? What breaks or is missing without it?
     2–4 sentences maximum. -->

**Phase:** <!-- e.g. Phase 1 -->
**Agents:** <!-- Comma-separated list of specialists for the Platform agent to invoke: Infrastructure, Documentation, Application. E.g. "Infrastructure, Documentation" -->
**Related ADR:** <!-- e.g. ADR-001, or "none" -->

---

## Acceptance criteria

<!-- Numbered list of testable conditions.
     Every criterion must be verifiable — if you cannot check it, rewrite it.
     The documentation criterion below is mandatory on every issue. -->

1.
2.
3.
- [ ] All documentation affected by this change has been identified and updated
      — `docs/registry.md` reflects any new or modified living documents

---

## Files likely affected

<!-- List the files the agent is expected to create or modify.
     Be specific — this scopes the agent's search space. -->

```
```

## Files to not touch

<!-- List files the agent must not modify under any circumstances.
     Include files that are adjacent to the work and might tempt the agent. -->

```
```

---

## Constraints

<!-- Things the agent must not do, even if they seem helpful.
     Examples: "do not modify the DAS mount configuration",
     "do not create new namespaces without documenting them" -->

---

## Definition of done

<!-- How will a human reviewer confirm this issue is complete?
     What command to run, what URL to check, what output to expect.
     This is distinct from acceptance criteria — it is the verification step. -->