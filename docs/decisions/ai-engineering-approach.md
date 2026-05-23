# AI Engineering Approach

> **Version:** 1.0
> **Status:** Living document
> **Related:** [`docs/decisions/project-approach.md`](./project-approach.md) · [`.github/agents/`](../../.github/agents/)

---

## Purpose

This document defines the principles and conventions governing AI tool usage
throughout this project. It is the reference point for any future AI tooling
decision and the context any agent needs to understand how AI is used here.

---

## Principles

**Traceable.** Every AI action that touches the codebase is visible in Git
history, PR comments, or CI logs. Nothing happens silently.

**Reversible.** No AI action bypasses the human review gate. Every change
can be reverted via a standard Git revert.

**Human-gated.** AI handles first-draft and mechanical work. A human
approves every change before it reaches the main branch. This gate is
non-negotiable regardless of AI confidence.

**Token-efficient.** Context is loaded on demand, not by default. Always-loaded
instructions are kept to the absolute minimum. Task-specific guidance lives
in agent files loaded only when relevant. [me] AI is not to conduct work that can otherwise be handled by other automation i.e. bash scripting, etc.

**IDE-agnostic.** Agent instruction files are plain markdown documents in the
repository. They are not coupled to any specific tool. Switching from Copilot
to Cursor to Claude Code requires no changes to the agent files themselves.

**Quality-in quality-out.** Agent output quality is directly proportional to
issue quality. Vague issues produce vague implementations. The issue template
and upload script exist to enforce this contract.

---

## Tool roles

| Tool | Role | When active |
|---|---|---|
| AI chat (Copilot Chat, Claude, etc.) | Planning, issue generation, architectural discussion | Any time |
| Coding agent (Copilot agent, Claude Code, etc.) | Issue implementation — writes code, creates files, opens PRs | When assigned a well-formed issue |
| AI PR review (Copilot review, CodeRabbit) | First-pass review before human reads the diff | On every PR automatically |
| GitHub Actions | CI validation — linting, secret scanning, manifest validation | On every PR and merge |
| Local LLM (Ollama) | On-cluster inference — commit messages, summaries | Stretch goal, Phase 4+ |

No tool in this list has merge authority. No tool bypasses secret scanning.

---

## Context architecture

```
.github/copilot-instructions.md   ← always loaded, ~40 lines, universal rules only [me] Is this not vscode specific how does this work for claude code?
        │
        └── .github/agents/       ← loaded on demand, one file per task type [me] Again is this code vscode specific?
                documentation-agent.md
                infrastructure-agent.md
                application-agent.md
                ...

docs/contributing/
        documentation-skill.md    ← judgment and convention detail, agent-referenced    [me] is this the correct convention for location of skill files?
        templates/                ← document structure, referenced by agents
```

Always-loaded context contains only: security absolutes, repo navigation,
and the routing table to agent files. Everything else is on demand.

---

## Issue quality contract

Issues are the primary interface between human intent and agent output.
Every agent-targeted issue must contain:

- Specific, scoped title in imperative mood
- Context explaining why the work is needed and which phase it belongs to
- Numbered, testable acceptance criteria
- Explicit list of files the agent should touch [me] Are these points useful?
- Explicit list of files the agent must not touch [me] Are these points useful?
- Constraints — things the agent must not do
- Which agent instruction file to load [me] Should we let the agent figure out this itself? Is it efficient to predict this? Is it token efficient?

Issues that omit these fields produce unpredictable output. The
`scripts/upload-issues.sh` script and the issue template exist to make
compliance the path of least resistance.

---

## What AI does not decide

AI tooling in this project does not:

- Make architectural decisions — those require an ADR and human sign-off (Realistically the AI is working with the human to write these ADRs)
- Merge pull requests — every merge requires human approval
- Modify the DAS or any safety-gated resource
- Select new tools not already listed in this document or an ADR

When an agent encounters a decision outside its scope it stops, comments
on the issue, and waits. It does not proceed and correct later.