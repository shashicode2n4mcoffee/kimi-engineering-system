---
name: debug
description: Root-cause analysis and a verified fix for a bug or failure
type: prompt
whenToUse: When the user reports a bug, error, failure or unexpected behavior
arguments:
  - problem
---

Root-cause and fix: $problem

Workflow:
1. REPRODUCE: capture the exact error, stack trace or failing behavior.
   Preserve error text verbatim — do not compress it.
2. HYPOTHESIZE: form candidate causes ranked by likelihood. A familiar
   error can have a different cause — do not pattern-match blindly.
3. ISOLATE: bisect with targeted inspection, minimal experiments and (when
   available) the debugger/tests. Confirm the cause with evidence before
   naming it.
4. FIX: the smallest correct fix at the root cause, consistent with project
   conventions. Invoke backend-engineer / frontend-engineer / ai-engineer
   as relevant.
5. VERIFY: reproduce the original scenario and prove it now works; run the
   surrounding test suite; invoke the test-engineer skill to add a
   regression test for this defect when the project has tests.

Report: confirmed root cause (with evidence), what was still hypothesis,
the fix, verification results.

Token optimization is mandatory throughout: apply the `token-optimizer`
skill policy (RTK for compact terminal output where supported, targeted
reads, no duplicate tool calls, parallel independent calls, measured —
not estimated — reporting).
