---
name: optimize
description: Performance and resource optimization — profile first, then fix the measured bottleneck
type: prompt
whenToUse: When the user asks to make something faster, leaner or more efficient
arguments:
  - target
---

Invoke the performance-engineer skill for: $target

Measure first: define the metric (p95/p99 latency, throughput, CPU/memory)
and profile before changing anything. Fix in order of impact: algorithmic
complexity, database/indexes/N+1, caching (with invalidation strategy),
concurrency, allocations. Verify with the same measurement and report
before/after numbers. Every optimization ships with the evidence that
justified it.
