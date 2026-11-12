---
name: token
description: Audit and optimize AI token consumption across tools and workflows
type: prompt
whenToUse: When the user asks about token usage, cost optimization, or to audit the token-optimization setup
arguments:
  - target
---

Invoke the token-optimizer skill for: $target

If no target given, run a token-efficiency audit of the current setup:
verify which local tools are actually active (rtk via `rtk gain`, headroom
via `headroom doctor`, LiteLLM via its proxy port), inspect recent
tool-call patterns for duplicated reads and unfiltered output, and report
measured savings plus concrete policy adjustments. Never claim a tool is
active unless verified in this session. Protect answer quality: no
compression that loses code, errors or security evidence.

Token optimization is mandatory throughout: apply the `token-optimizer`
skill policy (RTK for compact terminal output where supported, targeted
reads, no duplicate tool calls, parallel independent calls, measured —
not estimated — reporting).
