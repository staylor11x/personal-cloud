# RB-NNN: [Short descriptive title]

<!-- Replace NNN with the next sequential runbook number. Replace the title with a concise
     description of the procedure, e.g. "RB-001: Cluster node recovery". -->

> **Status:** Draft
> **Last tested:** [YYYY-MM-DD]
> **Expected duration:** [N minutes]
> **Severity if skipped:** [Critical / High / Medium / Low]

<!-- A runbook that has never been tested is a liability. Run a drill before marking this Active. -->
<!-- Status must be one of: Draft / Active / Deprecated. -->
<!-- A runbook must not be marked Active unless Last tested contains a real date. -->

---

## Purpose

<!-- One paragraph: what this runbook does and when to use it. State the condition that triggers
     its use. Example: "This runbook recovers the k3s cluster node after an unplanned restart.
     Use it when the node fails to rejoin the cluster automatically within five minutes of
     restarting." -->

---

## Prerequisites

<!-- List everything that must be true before starting. Include:
     - Access requirements (VPN connected, SSH key available, sufficient permissions)
     - Tools that must be installed on the operator's machine
     - Services that must be running before the procedure begins
     - Any backup steps that must be completed before proceeding -->

- [ ] [Prerequisite 1 — e.g. Tailscale VPN active and target node reachable]
- [ ] [Prerequisite 2]

---

## Steps

<!-- Number every step. Each step must include: the action to take, the expected output or
     observable result, and what to do if the step fails. -->

### Step 1: [Action name]

**Action:** <!-- Describe what to do. Be specific enough that the procedure can be followed
               without additional context. -->

```bash
# Command, if applicable
```

**Expected output:** <!-- What success looks like. Include specific strings, states, or
                         return codes to look for. -->

**If this fails:** <!-- What to check or try. Include relevant log paths or diagnostic
                      commands. -->

---

### Step 2: [Action name]

**Action:** <!-- Describe what to do. -->

**Expected output:** <!-- What success looks like. -->

**If this fails:** <!-- What to check or try. -->

---

## Verification

<!-- Describe how to confirm the procedure succeeded end-to-end. List specific commands,
     observable states, or test results that confirm the system is in the expected state. -->

---

## Rollback

<!-- Describe how to undo this procedure if it causes problems. If the procedure is not
     reversible, state that explicitly and describe the recovery path instead. -->

---

## Related runbooks

<!-- Runbooks commonly needed alongside this one. Remove this section if empty. -->

- [RB-NNN: title](./RB-NNN.md) — [brief description of when to use it in relation to this runbook]
