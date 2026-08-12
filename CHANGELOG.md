# Changelog — panel-review for Cursor


## 0.18.2

- **Server identity is now declared properly instead of inferred.** The plugin
  declared no icon, so a client that wanted one had to scrape the `homepage`
  page for its icon links — and that page, `truverif.ai/mcp`, now 308-redirects
  and served a stub with no icon links. `homepage` now points at the canonical
  `truverif.ai/panel-review`, and the MCP server declares its icons and website
  URL directly in the initialize handshake (`serverInfo.icons` / `websiteUrl`,
  per the MCP spec).
- **This is not expected to be visible in Cursor yet.** Cursor staff have
  confirmed their UI does not render custom MCP server icons even when the
  server declares them correctly, and the Cursor plugin manifest has no icon
  field. This release makes the metadata correct so it renders if and when
  Cursor adds support; it does not by itself put a mark on your screen. No
  behaviour change to the gates or the tools.


## 0.18.0 (first Cursor release)
- IDE: write gate (`preToolUse`/Write) + commit gate (`beforeShellExecution`),
  deny via `permission`/`agent_message`; `ask` degrades to allow-with-warning
  (Cursor accepts but does not enforce `ask`).
- CLI: commit-gate-only via repo `.cursor/hooks.json` (see README); write hook
  registered forward-compatibly.
- The write-gate deny binding is marked ASSUMED (unverified upstream) — if it
  proves ineffective, the plugin degrades to commit-gate-only with no update
  needed; verification status is reported by `npx @truverifai/init doctor`.
