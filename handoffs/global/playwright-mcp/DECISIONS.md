# Decisions
- Node.js installed user-level at ~/.local/node (official tarball v26.13.1 LTS), symlinked node/npm/npx/playwright-mcp into ~/.local/bin (already on PATH). No sudo used.
- @playwright/mcp 0.0.85 installed globally into the user-level Node prefix.
- Registered in USER-LEVEL ~/.kimi-code/mcp.json (applies to all projects) as stdio server with --headless --isolated (no background service, fresh profile per session).
- Kept stdio transport (not --port HTTP mode) to avoid a persistent background process.
