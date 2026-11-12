---
name: mcp
description: MCP tools, servers and integration engineering
type: prompt
whenToUse: When building MCP servers/clients, designing MCP tools, or integrating MCP into the environment
arguments:
  - task
---

NOTE: invoked via /skill:mcp because /plan-style shorthand is unavailable —
/mcp collides with the built-in MCP-status command.

Invoke the ai-engineer skill for the MCP work: $task

MCP engineering rules: small, focused tools with clear names and validated
input schemas; least-privilege tool design (each tool grants only the access
it needs); explicit error responses that help the calling model recover;
side-effecting tools require confirmation; treat tool output as untrusted
content in the calling agent (prompt-injection defense); version the
protocol surface and keep backward compatibility. Verify by actually
connecting/listing tools (e.g. via the built-in /mcp command) and exercising
a real call. Never invent server capabilities — verify against the official
MCP spec/docs.

## Installed servers (verified)

- `playwright` — official @playwright/mcp 0.0.85, user-level
  (`~/.kimi-code/mcp.json`), stdio, `--headless --isolated`. Browser
  automation for E2E validation, UI testing, page inspection. First use
  downloads the headless browser shell (one-time). Verify status with the
  native `/mcp` command; tools appear as `mcp__playwright__*`.
  Node.js runtime: ~/.local/node (symlinked into ~/.local/bin).
