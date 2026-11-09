---
name: minimal-file-access
description: Enforce justified, approved file access before any reads. Use when editing codebases, debugging, refactoring, or any task that risks opening unnecessary files. Triggers on requests involving source files, configs, or multi-file changes where over-reading wastes tokens.
---

# Minimal File Access

Force deliberate file selection. AI agents over-read because more context feels safer. This skill cuts browse-and-hope behavior.

## Core Rules

1. **Before opening any file**, list the exact files needed and why each one is required.
2. Discover candidates via file tree, directory listing, or search tools only. Do not open content yet.
3. Present the list to the user and wait for explicit approval.
4. After approval, make the **smallest, highest-confidence change** that fully solves the problem.
5. If a needed file is not on the approved list, **do not open it**. Summarize what is still needed in one line and stop.

## Workflow

### Phase 1 — Discover and Justify

- Use `ls`, `find`, `tree`, or search tools to locate candidate files.
- Output a numbered list in this format:

```
Proposed files to open:
1. path/to/file1.ext — reason (e.g. contains the function that needs changing)
2. path/to/file2.ext — reason
```

- Do not open, read, or cat any file content in this phase.
- If the list is incomplete, say so and ask for guidance instead of guessing.

### Phase 2 — Await Approval

- Stop after presenting the list.
- Only proceed once the user explicitly approves (or amends) the list.
- Treat silence or unrelated replies as non-approval.

### Phase 3 — Minimal Edit

- Open **only** approved files.
- Prefer the smallest diff that achieves the goal.
- Prefer high-confidence changes over speculative ones.
- After the change, briefly confirm what was done and which files were touched.

### Hard Stop Rule

If during work you discover you need an unapproved file:

```
Still need: path/to/missing.file — one-line reason
```

Then stop. Do not open it.

## Anti-Patterns to Avoid

- Opening files "just in case" or for background context.
- Reading entire directories when only one file is needed.
- Making large exploratory refactors before confirming the minimal fix.
- Continuing after realizing a required file is missing from the approved list.

## When to Apply

Apply this skill on any task that involves reading or editing multiple files, especially in unfamiliar or large codebases. Skip it only for single-file tasks where the exact path is already known and approved by context.
