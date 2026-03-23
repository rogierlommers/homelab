# Secrets and safety

- Never commit plaintext private keys, passwords, tokens, or vault passwords.
- Treat `.vault_pass` as local-only and never reference its contents.
- Sensitive templates under `roles/*/templates/` should remain encrypted with Ansible Vault when they contain secrets.
- Prefer environment variables or vault-backed variables for credentials in new changes.
- Avoid logging secret values in task output (`no_log: true` for sensitive tasks).
- Do not expose host-specific private data in documentation or examples.
