---
name: ai
description: AI/LLM/RAG/agent architecture and implementation
type: prompt
whenToUse: When building or reviewing LLM apps, RAG pipelines, agents, tool calling, embeddings or model infrastructure
arguments:
  - task
---

Invoke the ai-engineer skill for: $task

Apply the AI engineering rules: simplest sufficient architecture (direct
tool-calling before frameworks, single agent before multi-agent, RAG before
fine-tuning); structured outputs with schema validation; retrieval evaluated
before tuned; prompt-injection defense (retrieved content is untrusted);
observability with token/cost accounting; model routing and caching for
cost. Never invent model or library capabilities — verify against official
docs or state the limitation. Deliver architecture, design decisions,
implementation, evaluation plan and security analysis.

Token optimization is mandatory throughout: apply the `token-optimizer`
skill policy (RTK for compact terminal output where supported, targeted
reads, no duplicate tool calls, parallel independent calls, measured —
not estimated — reporting).
