---
name: plan
description: Requirements analysis, research and a step-by-step implementation plan without executing it
type: prompt
whenToUse: When the user wants a plan before implementation, or requirements and research for a task
arguments:
  - task
---

Produce a requirements + research + implementation plan for: $task

NOTE: invoked via /skill:plan because /plan collides with the built-in
Plan-mode toggle.

Workflow:
1. UNDERSTAND: inspect the repository, architecture, conventions and
   constraints relevant to the task. Never assume greenfield. List
   assumptions and ask only essential questions.
2. RESEARCH: invoke the github-researcher skill for technology/library
   selection: official docs, GitHub candidates, licenses, maintenance,
   security advisories, build-vs-reuse. State when research is unavailable.
3. DESIGN: invoke the principal-architect skill for the target
   architecture: simplest sufficient design, key trade-offs, ADR-worthy
   decisions flagged.
4. PLAN: ordered, verifiable steps. Each step names files/components
   touched, the discipline skill that governs it (backend-engineer,
   frontend-engineer, ai-engineer, security-engineer, test-engineer,
   devops-engineer, performance-engineer) and how to verify it. End with
   the quality-gate checklist from ~/.kimi-code/AGENTS.md mapped to steps.

Do NOT implement. Deliver the plan and stop, unless the user says to
proceed. Keep it concise — no filler.
