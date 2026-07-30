# Changelog — panel-review for Cursor

## 0.18.0 (first Cursor release)
- IDE: write gate (`preToolUse`/Write) + commit gate (`beforeShellExecution`),
  deny via `permission`/`agent_message`; `ask` degrades to allow-with-warning
  (Cursor accepts but does not enforce `ask`).
- CLI: commit-gate-only via repo `.cursor/hooks.json` (see README); write hook
  registered forward-compatibly.
- The write-gate deny binding is marked ASSUMED (unverified upstream) — if it
  proves ineffective, the plugin degrades to commit-gate-only with no update
  needed; verification status is reported by `npx @truverifai/init doctor`.
