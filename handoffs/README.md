# Shared Inter-Skill Handoff Directory

One directory per project, one record per task:

    ~/.kimi/handoffs/<project>/<task-id>/
    ├── TASK_CONTEXT.md   # objective, requirements, current state
    ├── EXECUTION_LOG.md  # what each skill actually did (appended per skill)
    ├── DECISIONS.md      # architecture/design/technical decisions + rationale
    ├── CHANGES.md        # files and configurations changed
    ├── VALIDATION.md     # tests run, PASS/FAIL/NOT RUN, unresolved failures
    └── NEXT_STEPS.md     # pending work + exact continuation instructions

Rules:
- Single shared record per task; update files in place, never duplicate.
- Every non-trivial skill run reads TASK_CONTEXT/DECISIONS/NEXT_STEPS first,
  continues from recorded state, and appends its own execution record.
- Trivial tasks need no handoff files.
- Never store credentials, API keys or secrets here.
- Template: copy from _TEMPLATE/ when starting a significant task.
