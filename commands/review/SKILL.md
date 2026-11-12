---
name: review
description: Comprehensive code review — correctness, concurrency, security, performance, tests, architecture
type: prompt
whenToUse: When the user asks for a code review of a diff, branch, PR or files
arguments:
  - target
---

Invoke the code-reviewer skill and review: $target

If no target given, review the current uncommitted changes (git diff /
git status). Read the actual code; cite file:line for every finding;
prioritize correctness, race conditions, security and data integrity over
style; verify claims before reporting; mark unverified suspicions as
questions. Deliver: verdict (approve / request changes), blocking findings,
non-blocking suggestions, test-coverage assessment, positive notes.

Token optimization is mandatory throughout: apply the `token-optimizer`
skill policy (RTK for compact terminal output where supported, targeted
reads, no duplicate tool calls, parallel independent calls, measured —
not estimated — reporting).

Toolkit: ast-grep to verify structural claims, semgrep for security
patterns, trivy when dependency/container changes are in scope, ripgrep for
cross-reference checks. Record findings in the task handoff.
