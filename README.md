# minimal-file-access

A Grok skill that forces deliberate, approved file access before any reads.

AI agents tend to over-read because more context feels safer.  
This skill cuts that behavior by requiring justification and explicit approval first.

## What it does

1. **Discover only** — use tree / search / ls. Never open file contents yet.
2. **List exact files + one-line reason** for each.
3. **Stop and wait** for your explicit approval.
4. After approval → make the **smallest, highest-confidence change**.
5. If anything else is needed later → one-line “Still need: …” and stop. No unapproved opens.

## Installation

Copy the `SKILL.md` into your Grok skills directory:

```bash
mkdir -p ~/.grok/skills/minimal-file-access
cp SKILL.md ~/.grok/skills/minimal-file-access/
```

Or place the whole folder under `/home/workdir/.grok/skills/` (or your equivalent user skills path).

## When it triggers

Any task that involves reading or editing source files, configs, or multi-file changes where over-reading wastes tokens — debugging, refactoring, feature work in unfamiliar codebases, etc.

## Example interaction

```
Proposed files to open:
1. src/auth/login.ts — contains the function that needs the timeout fix
2. src/config.ts   — holds the default timeout value

(waiting for approval)
```

After you say “yes” or “approved”, it proceeds with the minimal edit.

## License

MIT (or whatever you prefer — feel free to change)
