---
name: benchmark
description: Benchmark latency, memory, tokens and throughput with real measurements
type: prompt
whenToUse: When measuring performance, throughput, latency, memory or token consumption
arguments:
  - target
---

Invoke the performance-engineer skill and, for AI workloads, the
token-optimizer skill to benchmark: $target

Method: define the metric and environment; warm up; run enough iterations
for a stable p50/p95/p99; report latency, throughput, error rate, memory and
(where relevant) token usage/cost. State the environment honestly —
synthetic local numbers are labeled as such. Compare against a stated
baseline or accept the numbers as the new baseline. Never invent numbers;
if a benchmark cannot run here, say so and provide the exact harness to run.
