---
name: refactor
description: Safe architectural and code refactoring with verification at each step
type: prompt
whenToUse: When restructuring code, extracting modules, simplifying designs or paying down tech debt
arguments:
  - target
---

Refactor safely: $target

Workflow:
1. CHARACTERIZE: invoke the test-engineer skill first — existing tests must
   pin current behavior; add characterization tests where coverage is thin.
2. PLAN: invoke the principal-architect skill. Small, behavior-preserving
   steps; one step at a time; never mix refactoring with behavior change.
3. EXECUTE: rename/extract/move with the project's own tooling where
   available; keep commits/steps independently verifiable.
4. VERIFY: run the full test suite after every step; diff the public
   surface to prove no contract changed.
5. REVIEW: invoke the code-reviewer skill on the final diff.

Report: before/after structure, behavior-preservation evidence (tests that
ran), any intentional contract changes called out explicitly.

Use ast-grep for structural search and safe, targeted rewrites; ripgrep to
verify no stragglers remain. Targeted transformations over broad regex.
