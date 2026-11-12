# ENGINEERING_SYSTEM.md — Autonomous Principal Engineering Environment

Persistent engineering configuration for Kimi Code CLI. Installed 2026-11-12,
reorganized 2026-11-12 into the `~/.kimi/` layout. Applies to every project
and new session automatically.

## Architecture

```
~/.kimi/                          # canonical home (your layout)
├── AGENTS.md                     # global engineering directives (persona,
│                                 #   standards, security baseline, quality
│                                 #   gates, token policy)
├── commands/                     # 17 slash-command skills
│   ├── do/SKILL.md
│   ├── plan/SKILL.md
│   ├── architect/ … token/
├── skills/                       # 11 discipline skills
│   ├── principal-architect/SKILL.md
│   ├── ai-engineer/ … token-optimizer/
└── reports/
    ├── ENGINEERING_SYSTEM.md     # this file
    └── SETUP_REPORT.md           # install log, verification, limitations

~/.kimi-code/                     # Kimi Code live wiring (do not edit casually)
├── AGENTS.md -> ~/.kimi/AGENTS.md            # symlink: global instructions
├── skills -> ~/.kimi/skills                  # symlink: discipline skills are
│                                             #   scanned via $KIMI_CODE_HOME/skills
└── config.toml                   # only change: extra_skill_dirs = ["~/.kimi/commands"]
```

Why the wiring is needed: Kimi Code natively scans `$KIMI_CODE_HOME/skills/`
(user scope), project `.kimi-code/skills/`, `~/.agents/skills/`, and any
`extra_skill_dirs` in `config.toml`. `~/.kimi/` is not a native scan path, so
the canonical `~/.kimi/` tree is linked in: disciplines via the
`~/.kimi-code/skills` symlink, commands via `extra_skill_dirs`. Both were
verified live after the move (skills re-registered in the running session
catalog under their new paths).

## How it works

1. **Global instructions** — Kimi Code reads `$KIMI_CODE_HOME/AGENTS.md`
   (i.e. `~/.kimi-code/AGENTS.md`) into every session. It carries the
   Principal-Engineer persona, SOLID/clean-architecture standards, the
   security baseline, the open-source-first rule, the 10 quality gates,
   autonomy boundaries, and the mandatory token-optimization policy.

2. **Discipline skills (11)** — reusable domain workflows the model loads
   via the Skill tool when relevant:
   `principal-architect`, `ai-engineer`, `github-researcher`,
   `backend-engineer`, `frontend-engineer`, `security-engineer`,
   `code-reviewer`, `test-engineer`, `devops-engineer`,
   `performance-engineer`, `token-optimizer`.

3. **Command skills (17)** — each is a thin wrapper that routes to the
   right discipline skill(s). Kimi Code registers user skills as slash
   commands automatically:
   - Shorthand works (e.g. `/do`, `/review`, `/debug`, `/test`,
     `/security`, `/token`, ...) for all names not taken by built-ins.
   - `/plan` and `/mcp` collide with built-in TUI commands, so use
     `/skill:plan` and `/skill:mcp` for those two.

| Command | Routes to |
|---|---|
| `/do` | orchestrates all: understand → research (github-researcher) → architecture (principal-architect) → implement (backend/frontend/ai-engineer) → validate (test-engineer, security-engineer) → deliver |
| `/plan` | github-researcher + principal-architect (plan only, no execution) |
| `/architect` | principal-architect |
| `/research` | github-researcher |
| `/review` | code-reviewer |
| `/debug` | reproduce → isolate → fix → verify (+ test-engineer for regression test) |
| `/test` | test-engineer |
| `/security` | security-engineer |
| `/optimize` | performance-engineer |
| `/ai` | ai-engineer |
| `/mcp` | ai-engineer (MCP rules) |
| `/refactor` | test-engineer → principal-architect → code-reviewer |
| `/explain` | direct explanation workflow |
| `/document` | principal-architect (docs/ADRs) |
| `/deploy` | devops-engineer |
| `/benchmark` | performance-engineer + token-optimizer |
| `/token` | token-optimizer |

4. **Skill selection is intelligent by design**: command wrappers name only
   the skills relevant to the task, and each discipline skill carries a
   `whenToUse` trigger so the model auto-invokes it for matching work.
   Skills are never all activated at once.

5. **Quality gates** — the 10 gates in AGENTS.md are the contract for every
   significant implementation; `/do` reports per-gate status and never
   falsely claims completion.

## Token optimization stack (verified status)

| Tool | Status | How it is used |
|---|---|---|
| RTK (`~/.local/bin/rtk`) | **ACTIVE — verified** (v1.2.0, savings via `rtk gain`; Copilot hook installed and tested) | Preferred wrapper for compact terminal output. Global policy in AGENTS.md. |
| Headroom (`~/.local/bin/headroom`) | INSTALLED, NOT ACTIVE (no Kimi Code or VS Code integration target; proxy not running) | Analysis commands usable now: `headroom doctor`, `agent-savings`, `audit-reads`. Full proxy integration requires Copilot OAuth (`headroom copilot-auth login`) — optional manual step. |
| LiteLLM (`~/ai-optimizer/`) | INSTALLED, NOT REQUIRED (Kimi-only environment, no API keys) | Do not start. Kept for future use. |
| GPTCache / Langfuse | INSTALLED in venv, NOT REQUIRED | Libraries usable programmatically; no server/monitoring infrastructure by design. |

## Developer toolkit (all verified 2026-11-13)

ripgrep 15.0.0 · fd 10.3.0 · fzf 0.67.0 · bat 0.25.0 · jq 1.8.1 ·
ast-grep 0.51.2 · semgrep 1.185.0 · trivy 0.76.2 · pre-commit 4.7.0 ·
shellcheck 0.11.0 · shfmt 3.12.0 · actionlint 1.7.12.

Selection policy and per-skill integration: see `~/.kimi/AGENTS.md`
("Developer toolkit" section). Targeted checks first; escalate to full
scans only when justified. fzf is attended-interactive only.

## Handoff system (execution memory)

`~/.kimi/handoffs/<project>/<task-id>/` — shared task records
(TASK_CONTEXT, EXECUTION_LOG, DECISIONS, CHANGES, VALIDATION,
NEXT_STEPS; template in `_TEMPLATE/`, spec in AGENTS.md). Every
non-trivial skill run reads the record first, continues from recorded
state, and appends its execution record. `/do` owns orchestration and
routes skills by task need. Context lifecycle: CONTINUE by default,
native `/compact` when large (handoff must be current first), native
`/clear` only after state is persisted — skills recommend these to the
user, they cannot invoke TUI commands themselves.

## Context7 / Playwright evaluation (deferred — recommendation only)

- **Context7**: adds an MCP server for live library docs. The
  `github-researcher` skill already retrieves official docs directly, and
  the directive is to avoid unnecessary MCP surface. Not installed.
  Revisit if research tasks repeatedly hit stale documentation.
- **Playwright**: large browser download; only valuable for frontend E2E.
  Not installed globally. Install per-project when a concrete E2E task
  requires it.

Core rules (full text in AGENTS.md): targeted reads and searches, no
duplicate tool calls, parallel independent calls, cheaper models for
mechanical subtasks, and never compress source code, errors, instructions
or security evidence at the cost of correctness.

## Installation / maintenance

- **Already installed** — nothing to do; new sessions pick everything up
  automatically (skills are scanned at startup; AGENTS.md is loaded at
  startup).
- Edit a skill: modify `~/.kimi-code/skills/<name>/SKILL.md`; changes are
  picked up on new sessions (or `/reload` in the TUI).
- Add a command: create a new directory under `~/.kimi-code/skills/` with a
  `SKILL.md` containing `name` and `description` frontmatter.
- Backup before changing global config: `cp ~/.kimi-code/config.toml
  ~/.kimi-code/tui.toml ~/.kimi-code/backups/`
- Verify tool status: `rtk gain`, `headroom doctor`, LiteLLM health at
  `http://localhost:4000/health` when running.
