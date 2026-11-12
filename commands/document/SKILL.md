---
name: document
description: Generate technical documentation and ADRs
type: prompt
whenToUse: When writing docs, ADRs, runbooks, READMEs or updating project documentation
arguments:
  - topic
---

Invoke the principal-architect skill for documentation work: $topic

Produce documentation grounded in the ACTUAL code and config — read it
first, never document aspirational behavior. Match the project's existing
docs format and location. ADRs follow: context, decision, alternatives,
consequences. Docs include: overview, architecture, how to build/run/test,
configuration (no secrets), operational notes. Update existing docs that
your changes make stale. Keep prose tight; diagrams only where they
clarify.
