# JigsawEngine — staged delivery roadmap

**Status:** proposal, without release dates or completed milestone claims.

| Stage | Deliverable | Acceptance evidence |
| --- | --- | --- |
| **0 — Audit** | Map inherited BRUTAL packages, dependencies, licensing and build paths | Dependency inventory, clean-build instructions and tests on named host OS |
| **1 — Runtime** | Minimal executable Jigsaw host with deterministic frame lifecycle | Runs a blank window/headless loop; fixed-step tests and clean shutdown |
| **2 — Diagnostics** | Frame markers, allocation and scheduling counters, reproducible benchmark harness | Exportable traces and comparable p50/p95/p99 frame-time results |
| **3 — Scheduling** | Dependency-aware task orchestration on top of evaluated primitives | Correctness/stress tests and benchmark vs serial execution |
| **4 — World** | Measured component storage, stable handles and batched structural changes | Spawn/despawn and iteration benchmarks; lifetime safety tests |
| **5 — Shooter testbed** | AI, combat, collision, animation and streaming stress scenario | Playable reproducible workload with per-system timings |
| **6 — Scale** | Streaming budgets, LOD/visibility policies and scalable content workflows | Sustained traversal and hitch analysis on reference hardware |
| **7 — Tools** | Developer diagnostics, content workflows and editor decisions driven by testbed needs | Repeatable asset iteration and documented debugging workflows |

## Release philosophy

A stage is not complete because its code compiles. It needs tests, representative performance evidence and documentation of limitations. Revisit architecture after each stage; do not prematurely build a broad editor or promise a production release.

## Immediate next implementation PR

Start with Stage 0: establish clean build commands, map the current BRUTAL dependencies and identify which libraries JigsawEngine will use directly. Then add a tiny runnable host and baseline measurements before introducing a custom ECS or scheduler.
