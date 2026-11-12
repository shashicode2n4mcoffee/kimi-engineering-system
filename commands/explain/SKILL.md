---
name: explain
description: Explain code and architecture clearly, at the depth the audience needs
type: prompt
whenToUse: When the user asks how code works, what something does, or wants an explanation of a system
arguments:
  - target
---

Explain: $target

Read the actual code before explaining — no guessing from names alone.
Structure the answer for the audience's level: start with the one-paragraph
"what and why", then the flow (entry points, data/control flow, key
decisions), then important details (edge cases, failure handling,
concurrency, trade-offs). Cite file:line so the user can navigate. Use
small concrete examples or diagrams (ASCII/mermaid) where they genuinely
clarify. Note anything surprising, risky or deprecated. Keep it as short as
the subject allows — no padding.
