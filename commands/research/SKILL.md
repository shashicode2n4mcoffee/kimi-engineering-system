---
name: research
description: GitHub and official documentation research with build-vs-buy recommendations
type: prompt
whenToUse: When the user asks to research open-source solutions, libraries, or compare options
arguments:
  - topic
---

Invoke the github-researcher skill for: $topic

Deliver: the actual requirement and constraints, 3-5 shortlisted candidates
from GitHub and official docs, per-candidate evidence (maintenance,
contributors, issue resolution, docs, tests, license, security advisories,
dependency footprint, production suitability), a comparison table, risks,
and a build-vs-reuse recommendation. Never invent repo features or
benchmarks; cite sources; state it plainly when network research is
unavailable.

Token optimization is mandatory throughout: apply the `token-optimizer`
skill policy (RTK for compact terminal output where supported, targeted
reads, no duplicate tool calls, parallel independent calls, measured —
not estimated — reporting).
