# .agent rules

This directory contains repository-specific rule files for coding agents working in this homelab Ansible project.

## Purpose

- Keep agent behavior consistent with repository structure and conventions.
- Prevent unsafe changes (especially around secrets).
- Make future rule additions predictable and easy to review.

## File naming convention

Use ordered filenames so broad rules load first and specialized rules load later:

- `00-*` : repository scope and general behavior
- `10-*` : implementation standards (for example Ansible authoring)
- `20-*` : security and secret handling
- `30-*` : role/host-specific patterns
- `90-*` : temporary or migration notes (remove after use)

Keep each file focused on one theme.

## How to add a new rule file

1. Pick the smallest scope needed (general, Ansible, security, host-specific).
2. Create a new markdown file in `.agent/` using the numbering convention above.
3. Write short, enforceable bullet rules (avoid vague guidance).
4. Avoid duplicates with existing files; update an existing file when possible.
5. If behavior changes, update related role docs in `roles/*/README.md` when relevant.

## Rule writing guidelines

- Prefer concrete instructions over broad style statements.
- Bias toward idempotent Ansible patterns and minimal diffs.
- Include repository-specific gotchas (for example cron `%` escaping as `\%`).
- Do not include secrets, tokens, private key material, or vault password contents.

## Validation

Use this command from the repository root to list all active rule files:

```bash
find .agent -type f -name "*.md" | sort
```

If a new file does not appear in that output, fix path or extension before merging.
