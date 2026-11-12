---
name: test
description: Create and execute test suites — unit, integration, E2E, boundary and failure testing
type: prompt
whenToUse: When the user asks to write, run or improve tests
arguments:
  - target
---

Invoke the test-engineer skill for: $target

If no target given, assess and extend tests for the code changed in the
current working tree. Follow the project's existing test framework and
conventions. Cover behavior and contracts, boundary values, and failure
paths; mock only at architectural boundaries. Then EXECUTE the tests and
report real results — never claim tests passed unless they ran. Report
coverage of critical paths, gaps that remain, and any flakiness found.

Run pre-commit checks where the project has them (preserve existing
config/hooks). Targeted tests first, `rtk test` for compact failure-only
output; full suites when justified. Record PASS/FAIL/NOT RUN in the task
handoff VALIDATION.md.
