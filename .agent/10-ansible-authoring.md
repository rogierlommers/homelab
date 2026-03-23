# Ansible authoring rules

- Always use explicit, descriptive `name` values for tasks.
- Keep one concern per task; split large mixed tasks into small sequential tasks.
- Prefer fully-qualified collection names for community modules (for example `community.general.*`).
- Use `include_tasks` for node-specific flows, with clear `when` conditions.
- New variables must live in `group_vars/all.yml` unless they are role-internal defaults.
- Prefer booleans in canonical YAML form (`true`/`false`) in new edits.
- For package installation, use list form under `apt.name` and keep alphabetical ordering when practical.
- For filesystem/config changes, set ownership and permissions explicitly when relevant.
