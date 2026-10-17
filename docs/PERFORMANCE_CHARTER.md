# JigsawEngine — performance charter

**Status:** planned engineering policy; no verified JigsawEngine performance baseline exists yet.

## Optimize frame time, not marketing numbers

At 60 FPS, the whole frame has about **16.67 ms**. At 120 FPS, about **8.33 ms**. Those are total frame budgets, not CPU-only budgets. Present/driver waits and CPU/GPU overlap mean subsystem times cannot simply be summed to predict FPS.

Initial performance targets must be measured on explicitly named reference hardware and workloads, with graphics settings and build configuration recorded. Do not publish performance comparisons without reproducible data.

## Required measurements

- Frame times: median, p95, p99, worst-frame context and distributions over sustained runs.
- CPU: per-system wall time, CPU utilization, worker occupancy, queue latency, scheduling overhead and time blocked on dependencies.
- Memory: allocations per frame, managed GC events/pause times, working set, high-water marks and asset residency.
- Rendering: render-thread preparation, submission cost, GPU timings where supported and synchronization stalls.
- Streaming: I/O latency, decode time, asset upload time and frame hitches.
- Correctness: replay/checksum or equivalent validation for workloads requiring stable simulation behavior.

## Benchmark matrix

| Scenario | What it exposes |
| --- | --- |
| Empty frame / minimal scene | Baseline overhead and framework costs |
| Dense shooter arena | AI, combat, spatial queries, physics and animation contention |
| High-entity simulation | Data layout, update scaling and scheduler granularity |
| Streaming traversal | I/O, decompression, asset residency and hitch behavior |
| Rapid spawn/despawn | Structural changes, memory churn and lifetime bugs |
| Slow/fast CPU configurations | Oversubscription, worker scaling and budget behavior |

Run warm-up and measured phases; record build SHA, OS, CPU, GPU, memory, runtime version, power mode, resolution, scene seed and measurement method. Compare against the same baseline under the same conditions.

## Optimization gate

Every proposed micro-optimization should include:

1. A reproducible bottleneck and hypothesis.
2. A baseline measurement with variance.
3. A correctness or regression test.
4. An after measurement under equivalent conditions.
5. A complexity and maintenance-cost assessment.

Prefer algorithmic improvements and data locality before instruction-level tuning. SIMD, pooling, unsafe code, native interop and manual memory layouts are tools, not goals.

## Safety rails

No silent unbounded allocations in critical loops. Avoid locks and blocking calls on real-time-sensitive paths; if unavoidable, measure and document them. Use bounded queues and explicit overload behavior. Keep telemetry low-overhead and capable of being disabled or sampled in release builds.

**Performance claims are provisional until the testbed and benchmark harness exist.**
