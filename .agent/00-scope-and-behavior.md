# Scope and behavior

- This repository provisions Debian VMs with Ansible from `playbook.yml` and `roles/`.
- Make minimal, targeted changes; do not refactor unrelated roles or task files.
- Keep role boundaries intact: shared logic in role `tasks/main.yml`, host-specific logic in included task files.
- Preserve existing YAML style used in this repo unless a file already uses a different style.
- Prefer idempotent Ansible modules over shell/command invocations whenever possible.
- When adding new role behavior, update that role’s `README.md` with a concise task/variable summary.
