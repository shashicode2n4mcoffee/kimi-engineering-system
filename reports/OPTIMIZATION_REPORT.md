# OPTIMIZATION_REPORT.md — AI Optimization Stack Integration

Date: 2026-11-13. Every status below was verified by execution in this
session; nothing is assumed from installation alone.

## ACTIVE (tested working)

| Tool | Evidence |
|---|---|
| RTK 1.2.0 | `rtk gain`: 2 commands tracked, 388 tokens saved (83.4% efficiency). Used throughout this session for compact output. |
| RTK → GitHub Copilot integration | `rtk init -g --copilot` installed `~/.copilot/hooks/rtk-rewrite.json` + `~/.copilot/copilot-instructions.md`. Hook TESTED: `git status` correctly rewritten to `rtk git status`, valid PreToolUse JSON, exit 0. Backup of prior `~/.copilot` in `~/.kimi-code/backups/`. Note: Copilot CLI itself still needs its own first-run setup (`copilot` in a terminal). |
| LiteLLM gateway mechanics | Started with a throwaway config (real upstream key absent): `/health` enforced auth (401 without key), `/v1/models` with master key listed aliases `fast` and `powerful`. Gateway stopped and temp config deleted after the test. |
| GPTCache library (core) | `import gptcache` OK, v0.1.44 — usable programmatically in applications. |
| Langfuse library (core) | `import langfuse` OK, v5.2.0 — usable programmatically in applications. |

## INSTALLED, NOT ACTIVE (manual step required)

| Tool | Blocker | Manual step |
|---|---|---|
| LiteLLM (full routing) | `OPENAI_API_KEY` and `LITELLM_MASTER_KEY` not set anywhere | Export both, then `~/ai-optimizer/start-litellm.sh`; point compatible apps at `http://localhost:4000` with the master key, using aliases `fast` / `powerful` |
| Headroom 0.44.0 proxy | GitHub Copilot OAuth not logged in (`headroom copilot-auth status`: not logged in); no Claude Code/Codex installed | `headroom copilot-auth login` (interactive device flow), then `headroom proxy` and `headroom init copilot` |
| Langfuse server | Needs Docker daemon (permission denied — user not in `docker` group; fixing that is admin-level) or Langfuse Cloud keys | `sudo usermod -aG docker $USER` + re-login, then self-host; or set `LANGFUSE_PUBLIC_KEY`/`LANGFUSE_SECRET_KEY`/`LANGFUSE_HOST` |

## UNSUPPORTED / BROKEN (do not use as-is)

| Tool | Status |
|---|---|
| `gptcache_server` binary | BROKEN in `~/ai-optimizer/venv`: gptcache 0.1.44's server requires `openai<1.0`, LiteLLM requires `openai>=1.0` (verified crash on startup). Fix would need a separate venv; pointless until upstream API credentials exist. Not integrated. |
| RTK native hooks for Kimi Code / Codex / Cursor / Cline / Gemini | rtk's hook targets: claude (not installed), codex (not installed), cursor/trae/windsurf/cline/kilocode/antigravity (not installed), opencode/gemini (not installed). Kimi Code is not an rtk hook target; RTK applies here via the global AGENTS.md policy instead. |
| Headroom integrations for Claude Code / Codex / OpenClaw | Targets not installed on this machine. |
| Kimi Code via LiteLLM | The managed Kimi provider uses OAuth against `api.kimi.com`; it does not support a custom base_url redirect through LiteLLM without changing providers — left untouched to avoid breaking the login. |
| Docker daemon | Client v29.1.3 present, daemon socket permission denied. Blocks Langfuse self-hosting. Admin action required. |

## Persisted configuration

- `~/.kimi/AGENTS.md` — token policy rewritten with verified statuses,
  gateway URL, aliases, and measured-vs-estimated reporting rules. Applies
  to every session and project.
- `~/.kimi/skills/token-optimizer/SKILL.md` — full verified inventory,
  start procedures, and audit workflow (incl. `rtk gain`, `rtk discover`,
  `headroom audit-reads`, `headroom agent-savings`).
- Command skills `/do`, `/research`, `/architect`, `/review`, `/debug`,
  `/ai`, `/token` — each now explicitly invokes the token-optimizer policy.
- No duplicate configs created; no conflicting hooks; existing user configs
  backed up before modification (`~/.kimi-code/backups/`).

---

**Update 2026-11-13 (upgrade):** This environment is now Kimi-only by
design. LiteLLM, GPTCache and Langfuse are reclassified as **not required**
— do not start or depend on them. RTK remains the only ACTIVE optimization
tool; Headroom remains installed with no Kimi Code/VS Code integration
target (analysis commands only). See SETUP_REPORT.md "Upgrade 2026-11-13".
