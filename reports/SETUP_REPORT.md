# SETUP_REPORT.md — Engineering System Installation

Date: 2026-11-12 · Host: Linux (x86_64) · Kimi Code CLI v2.6.0

## Files created

| File | Purpose |
|---|---|
| `~/.kimi/AGENTS.md` | Global engineering directives (persona, standards, security baseline, quality gates, token policy) — loaded into every session |
| `~/.kimi/skills/<name>/SKILL.md` × 11 | Discipline skills (native Kimi skill format, directory form) |
| `~/.kimi/commands/<name>/SKILL.md` × 17 | Slash-command skills (composable wrappers routing to disciplines) |
| `~/.kimi/reports/ENGINEERING_SYSTEM.md` | Full system architecture, command→skill routing, tool status, maintenance |
| `~/.kimi/reports/SETUP_REPORT.md` | This report |

## Live wiring (Kimi Code native scan paths)

`~/.kimi/` is the canonical home; the CLI is connected to it via:
- `~/.kimi-code/AGENTS.md` → symlink to `~/.kimi/AGENTS.md`
- `~/.kimi-code/skills` → symlink to `~/.kimi/skills`
- `~/.kimi-code/config.toml` → one added line:
  `extra_skill_dirs = ["~/.kimi/commands"]`

## Files modified

`~/.kimi-code/config.toml` — only the `extra_skill_dirs` line above.
`~/.kimi-code/tui.toml` untouched.

## Files backed up

`~/.kimi-code/backups/pre-engineering-system-20261112-233930/`
(contains `config.toml` and `tui.toml` as they were before setup).

## Commands installed (17)

`/do` `/architect` `/research` `/review` `/debug` `/test` `/security`
`/optimize` `/ai` `/refactor` `/explain` `/document` `/deploy`
`/benchmark` `/token` — available by shorthand name.
`/plan` and `/mcp` — available as `/skill:plan` and `/skill:mcp`, because
the names collide with built-in TUI commands (`/plan` plan-mode toggle,
`/mcp` server status). This is a documented platform limitation, not a
defect.

## Skills installed (28)

Disciplines (11): `principal-architect`, `ai-engineer`, `github-researcher`,
`backend-engineer`, `frontend-engineer`, `security-engineer`,
`code-reviewer`, `test-engineer`, `devops-engineer`, `performance-engineer`,
`token-optimizer`.

Commands (17): `do`, `plan`, `architect`, `research`, `review`, `debug`,
`test`, `security`, `optimize`, `ai`, `mcp`, `refactor`, `explain`,
`document`, `deploy`, `benchmark`, `token`.

## Integration status (verified, not assumed)

| Tool | Status | Evidence |
|---|---|---|
| RTK | **ACTIVE** | v1.2.0 at `~/.local/bin/rtk`; `rtk ls`, `rtk test` executed successfully; `rtk gain` tracks real savings |
| Headroom | INSTALLED, NOT ACTIVE | v0.44.0; `headroom doctor` shows proxy not running — policy requires verification before claiming use |
| LiteLLM | INSTALLED, NOT RUNNING | `~/ai-optimizer/start-litellm.sh` + `config/config.yaml` with `fast`/`powerful` aliases; requires `OPENAI_API_KEY` and `LITELLM_MASTER_KEY` env vars |
| Langfuse | NOT INSTALLED | No binary/package found on the system |
| GPTCache | NOT INSTALLED | No binary/package found on the system |

## Verification results

1. **Skill registration** — all 28 skills confirmed live in the session
   skill catalog after creation (11 discipline + 17 command), each with
   `description` and `whenToUse` for automatic routing.
2. **Tool verification** — RTK executed real commands with savings
   tracking; Headroom and LiteLLM status probed (not claimed as active).
3. **`/do` end-to-end demonstration** — ran `kimi -p "/do Inspect this
   repository and propose three high-impact engineering improvements. Do
   not modify source files."` in a scratch repo (`/tmp/do-demo`,
   deliberately vulnerable demo). The fresh session resolved `/do` to the
   skill and executed the workflow correctly:
   - inspected the repo before proposing anything (no greenfield
     assumption),
   - identified SQL injection (cited `app.py:8`, `app.py:13`), a hardcoded
     secret (`app.py:3`), and missing data-layer reliability/tests,
   - ranked findings by severity with effort estimates and a summary
     table,
   - reported quality-gate status honestly ("no build/tests exist to run;
     validation and security remediation gates pending"),
   - did not modify source files, per instruction.

## Unsupported capabilities / limitations

- `/plan` and `/mcp` shorthand unavailable due to built-in command-name
  collisions; use `/skill:plan` and `/skill:mcp`.
- Langfuse and GPTCache are not installed; the token policy treats them as
  optional and forbids claiming them. Installing them is a manual step.
- Headroom and LiteLLM proxies are intentionally not left running (no
  background token-consuming processes); start them on demand.

## Remaining manual steps (optional)

- To enable Headroom: `headroom proxy` (and `headroom init` for durable
  integration), then verify with `headroom doctor`.
- To enable LiteLLM routing: `export OPENAI_API_KEY=... LITELLM_MASTER_KEY=...`
  then `~/ai-optimizer/start-litellm.sh`; verify at
  `http://localhost:4000/health`.
- To add Langfuse/GPTCache: install and wire them into your AI stack; the
  `token-optimizer` skill already documents their status-check procedure.

---

# UPGRADE 2026-11-13 — Developer Toolkit, Handoff System, Kimi-Only Architecture

Backup before changes: `~/.kimi-code/backups/pre-upgrade-20261113-001058/`
(full `~/.kimi` tree + `config.toml`/`tui.toml`).

## What changed

- `~/.kimi/AGENTS.md` — added Developer toolkit policy (tool selection
  table), Inter-skill handoff protocol, Context lifecycle (native
  `/compact`/`/clear` only), Final completion protocol; token policy now
  Kimi-only (LiteLLM/GPTCache/Langfuse marked not required).
- `~/.kimi/handoffs/` — NEW shared handoff directory with README and
  `_TEMPLATE/` (TASK_CONTEXT, EXECUTION_LOG, DECISIONS, CHANGES,
  VALIDATION, NEXT_STEPS).
- 11 discipline skills — each gained a "Developer toolkit" section
  (per-skill tools) and the mandatory "Handoff protocol" section.
- 17 commands preserved; `/do` gained orchestration + handoff +
  toolkit routing; `/security`, `/refactor`, `/review`, `/test`,
  `/deploy` gained explicit tool workflows.
- No skills or commands deleted, renamed or duplicated. No packages
  installed (all 14 toolkit tools were already present). No services
  started. `config.toml` unchanged in this upgrade.

## Classification of every component

| Component | Classification |
|---|---|
| RTK 1.2.0 | Installed, Configured, **Actively verified** (incl. Copilot hook test) |
| Headroom 0.44.0 | Installed; integration **Unsupported** for Kimi Code/VS Code (no native target); analysis commands usable; proxy inactive |
| LiteLLM 1.109.1 | Installed, **Not required** (no API keys; do not start) |
| GPTCache 0.1.44 | Installed (library OK; server broken — openai<1.0 conflict), **Not required** |
| Langfuse 5.2.0 | Installed (library OK), **Not required** |
| ripgrep / fd / fzf / bat / jq | Installed, **Actively verified** |
| ast-grep / semgrep / trivy / pre-commit / shellcheck / shfmt / actionlint | Installed, **Actively verified** (trivy: version verified; vuln DB downloads on first scan) |
| 11 discipline skills + 17 commands | Installed, Configured, **Actively verified** (catalog + on-disk counts) |
| Global AGENTS.md + symlinks | Installed, Configured, **Actively verified** |
| Handoff system | Installed, Configured, **Actively verified** |
| Context7 | **Not installed** — recommended only if research hits stale docs |
| Playwright | **Not installed** — install per-project when E2E is needed |

## 20-point verification (all run 2026-11-13, harmless inputs, /tmp)

PASS: rtk, ripgrep, fd, fzf, bat, jq, ast-grep, semgrep, trivy (version),
pre-commit, shellcheck, shfmt, actionlint, skills load (11+17), commands
load, `/do` routing block present, AGENTS.md loads (symlink verified),
no API keys required, no optimization services running.
Headroom: installed; proxy inactive (expected in Kimi-only setup).
Two initial FAILs were verification-script artifacts (invalid `ast-grep -q`
flag; `pgrep` matching its own command line) — both re-tested and pass.

## Manual actions remaining (optional)

- Headroom full integration: `headroom copilot-auth login` → `headroom
  proxy` → `headroom init copilot` (only if you want Copilot CLI
  compression).
- Trivy first scan downloads its vulnerability DB (network, one-time).

---

# ADDENDUM 2026-11-13 — Playwright MCP INSTALLED (now active)

Reverses the earlier "deferred" recommendation per explicit user request.

- Node.js v26.13.1 installed user-level (`~/.local/node`, no sudo); node,
  npm, npx, playwright-mcp symlinked into `~/.local/bin`.
- @playwright/mcp 0.0.85 (official Microsoft Playwright MCP server).
- Registered user-level in `~/.kimi-code/mcp.json` (stdio, `--headless
  --isolated`, `--executable-path` pinned to downloaded Chromium
  `chromium-1254`). Applies to all projects; tools appear as
  `mcp__playwright__*`.
- VERIFIED end-to-end: fresh headless Kimi session navigated to
  example.com via the MCP browser tools and returned the page title.
- One-time browser download completed (ms-playwright cache).
- Handoff record: `~/.kimi/handoffs/global/playwright-mcp/`.
- Maintenance: after a @playwright/mcp upgrade, re-install the browser and
  update the pinned --executable-path.
- Classification: Installed, Configured, **Actively verified**.
