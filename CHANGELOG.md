# Changelog — panel-review for Cursor

## 0.18.8
- Skills copy sync with gate core 0.19.46: the commit gate now also prints
  `target_hunk_hashes` (A5), so the skip-gate and audit skills no longer
  describe it as write-gate-only; matching updates in the deliberate and
  synthesize skills and the reason-codes reference. (0.18.7 was the prior
  published version; no separate 0.18.7 entry existed.)

## 0.18.6
- `define-custom-floors` skill: explicit `(^|/)` path-anchor rule (a bare `^file$`
  matches only a root-level file) + resolve every `floors check` advisory before
  showing the user. (The write-gate `^file$` fix ships via the npm gate update.)

## 0.18.5
- `define-custom-floors` skill: workflow now leads with the whole-codebase scan
  and presents the full candidate floor list up front (interview moved to a
  refine step); every floor ships thorough code-derived keywords, and path floors
  propose `exclude_paths` for test/example subtrees by default.

## 0.18.4
- `define-custom-floors` skill: broader, more thorough first-draft authoring.


## 0.18.3
- Custom floor classes: adds the `define-custom-floors` skill. Gate enforcement
  ships via the npm `@truverifai/init` vendored gates (cli_vendor 0.19.39).

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
