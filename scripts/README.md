# scripts/

Utility scripts for the personal-cloud platform.

---

## upload-issues.sh

Bulk-uploads GitHub issues from a directory of Markdown files using the `gh` CLI. Adapted from the `create-issue.sh` script in [staylor11x/spider-solitaire](https://github.com/staylor11x/spider-solitaire).

### Requirements

- `bash` 4 or later
- `gh` CLI, authenticated with `repo` scope (`gh auth login`)

### Usage

```bash
./scripts/upload-issues.sh <issues-dir> [--repo OWNER/REPO] [--milestone NAME]
```

| Argument | Required | Description |
|---|---|---|
| `issues-dir` | Yes | Path to a directory containing `.md` issue definition files |
| `--repo OWNER/REPO` | No | Target repository. Defaults to the current repository detected via `gh repo view` |
| `--milestone NAME` | No | Milestone name to attach to every created issue. Must already exist on the target repository |

### Issue file format

Each `.md` file in the issues directory defines one issue. Files are processed in alphabetical order.

#### With YAML frontmatter

```markdown
---
title: The issue title
labels: enhancement,documentation
---

Issue body text goes here. Everything after the closing `---` is used as the
issue body.
```

#### Without frontmatter (spider-solitaire compatible)

```markdown
# The issue title

Issue body text goes here. Everything after the first `# H1` heading is used
as the issue body. If no H1 heading is present, the entire file is used as
the body and the filename (without `.md`) becomes the title.
```

#### Frontmatter fields

| Field | Description |
|---|---|
| `title` | Issue title. Overrides any `# H1` heading in the file |
| `labels` | Comma-separated list of label names. Labels must already exist on the repository |

### Notes

- Issues are never auto-assigned — assignment is a separate human decision made after upload
- Labels and milestones must exist on the target repository before the script is run
- If one or more issues fail to upload, the script prints a summary of failures and exits with a non-zero code. Issues that succeeded are not rolled back
- The repository is auto-detected from the local git context; pass `--repo` to target a different repository
