---
name: architect
description: System architecture and technical design with ADRs
type: prompt
whenToUse: When the user asks for system design, architecture, or an ADR
arguments:
  - topic
---

Invoke the principal-architect skill and produce the architecture for:
$topic

Include: requirements and constraints (functional and non-functional),
existing-system fit, candidate architectures compared (scalability,
availability, security, performance, maintainability, observability,
operational complexity, cost), the chosen simplest-sufficient design with
justification, component/responsibility map, data flow, failure-mode
strategy, and ADRs for significant decisions (context, decision,
alternatives, consequences).

Token optimization is mandatory throughout: apply the `token-optimizer`
skill policy (RTK for compact terminal output where supported, targeted
reads, no duplicate tool calls, parallel independent calls, measured —
not estimated — reporting).
