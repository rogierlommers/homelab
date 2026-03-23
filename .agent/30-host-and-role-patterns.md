# Host and role patterns

- Keep host-specific behavior inside `roles/node_specifics/tasks/` and gate by facts (`ansible_facts['nodename']`) unless inventory groups are introduced intentionally.
- Reuse existing role order in `playbook.yml` unless there is a clear dependency reason to change it.
- Put shared package/bootstrap setup in `roles/common`; avoid duplicating setup in host-specific task files.
- Prefer templates in `roles/<role>/templates/` over inline multi-line file content.
- For cron jobs, keep schedule, command, and healthcheck behavior explicit and documented in the role README.
- In cron commands, escape `%` as `\%` to avoid cron newline parsing issues.
