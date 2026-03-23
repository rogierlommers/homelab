
# Git patterns

## Commit messages

- Use Conventional Commits format: `<type>(<scope>): <subject>` (for example `feat(fail2ban): add custom jail for SSH`).
- Common types: `feat` (new behavior), `fix` (bug/correction), `chore` (maintenance), `docs` (documentation only), `refactor` (no behavior change).
- Use the role name as the scope when the change is confined to one role (for example `feat(common):`, `fix(ssh):`); use `playbook` or `inventory` for changes outside roles.
- Keep the subject line under 72 characters and written in imperative mood ("add", "remove", "update" — not "added" or "adds").
- Do not end the subject line with a period.

## Commit body

- Add a body when the reason for a change is not obvious from the subject alone.
- Explain *why* the change is needed, not just what was changed.
- Reference any relevant host, Ansible module, or playbook behavior that motivated the change.
- Separate the subject from the body with a blank line.

## Commit scope and atomicity

- Keep each commit focused on one logical change; do not bundle unrelated role edits in a single commit.
- If a role README is updated to reflect a task change, include that update in the same commit as the task change.
- Do not commit commented-out tasks, debug output, or temporary `ansible.cfg` overrides.

## Branching

- Use short, lowercase, hyphen-separated branch names prefixed with the type (for example `feat/fail2ban-recidive`, `fix/cron-percent-escape`).
- Keep `main` releasable at all times; use branches for work in progress.