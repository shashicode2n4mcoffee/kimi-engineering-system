---
name: do
description: End-to-end autonomous engineering — own a task from requirements through architecture, research, implementation, validation and delivery
type: prompt
whenToUse: When the user wants a task built or completed end-to-end autonomously (the default engineering command)
arguments:
  - task
---

Execute this task end-to-end as a Principal Engineer who owns it from
requirements to delivery: $task

If no task was given above, ask what to build.

MANDATORY WORKFLOW:

PHASE 1 — UNDERSTAND: Inspect the existing repository and architecture first
(existing tech choices, conventions, constraints, integration points). Never
assume greenfield. Identify ambiguity; ask only essential questions.

PHASE 2 — RESEARCH: Before selecting technologies or libraries, invoke the
github-researcher skill (search official docs and GitHub; check maintenance,
license, security advisories; compare alternatives). If research is
unavailable, state that limitation. Do not invent library capabilities.

PHASE 3 — ARCHITECTURE: Invoke the principal-architect skill. Evaluate
functional/non-functional requirements, scalability, security, performance,
maintainability, observability, operational complexity and cost. Choose the
simplest sufficient architecture. Create an ADR for significant decisions.

PHASE 4 — IMPLEMENTATION: Apply the global engineering directives from
~/.kimi-code/AGENTS.md (SOLID, strict types, boundary validation, no
hardcoded secrets, structured logging, minimal dependencies). Invoke
backend-engineer / frontend-engineer / ai-engineer as the task demands —
only the ones relevant to this task.

PHASE 5 — VALIDATION: Invoke the test-engineer skill. Build/compile, run
unit and integration tests, run lint/static analysis, check dependencies
for vulnerabilities, validate edge cases and failure scenarios. Never claim
tests passed unless they actually ran. Invoke security-engineer for
security-sensitive work.

PHASE 6 — DELIVERY: Report what was implemented, files created/modified,
architectural decisions, dependencies introduced, tests executed with real
results, security considerations, known limitations, and exact run/deploy
commands. Report which quality gates passed and which could not be
completed (and why).

Throughout: apply the token-optimizer policy — targeted reads, rtk for
compact command output, parallel independent calls, no duplicated work.
Do not stop at generating code when the task requires working software.
Respect the autonomy boundaries in the global directives: ask before
destructive or production-affecting actions.

Token optimization is mandatory throughout: apply the `token-optimizer`
skill policy (RTK for compact terminal output where supported, targeted
reads, no duplicate tool calls, parallel independent calls, measured —
not estimated — reporting).

## Orchestration and handoff (mandatory for significant tasks)

Own the task end-to-end. Create/continue the shared handoff record at
`~/.kimi/handoffs/<project>/<task-id>/` (template in `_TEMPLATE/`). Route
skills by task need — e.g. github-researcher → principal-architect →
backend/frontend/ai-engineer → security-engineer → test-engineer →
code-reviewer → document — not a fixed sequence. Each receiving skill
continues from the handoff state; never repeat completed phases; run
independent skill work in parallel; resolve conflicts before implementing.
Use the developer toolkit per `~/.kimi/AGENTS.md` (ripgrep/fd/ast-grep for
navigation, semgrep/trivy for security, pre-commit/actionlint/shellcheck/
shfmt for quality gates, rtk for compact output). Before delivery: update
the handoff record, report per-gate status, name the next recommended
skill or action, and recommend CONTINUE / COMPACT / CLEAR for the session.
