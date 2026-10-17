# JigsawEngine

**Build worlds with complicated rules. Keep every millisecond accountable.**

JigsawEngine is an **experimental, performance-first game-engine project** for CPU-intensive games, simulation-heavy worlds and interactive experiences with many interconnected systems. A shooter with sophisticated AI, destruction, ballistics and streaming can be just as demanding as a large open world. Both are within the design target.

> [!IMPORTANT]
> **Early architecture stage.** JigsawEngine is not yet a complete or benchmark-validated game engine. The goals below are design targets, not shipped features, performance guarantees or evidence that JigsawEngine outperforms existing engines.

## The ambition

Make ambitious games without making their systems fight each other for CPU time.

- **Frame-time discipline over headline FPS.** Design for stable p95/p99 frame times, observable stalls and explicit budgets.
- **Data locality first.** Prefer contiguous, iteration-friendly data for hot systems; profile before choosing specialized representations.
- **Parallelism with boundaries.** Schedule independent work while making dependencies, ownership and synchronization visible.
- **Systems that compose.** AI, physics, gameplay, streaming, animation, rendering preparation and audio should have explicit contracts.
- **Optimization with evidence.** Benchmark representative workloads, record hardware and configurations, and require correctness tests before accepting low-level optimizations.
- **Scale both ways.** Support dense small arenas and large streamed environments without assuming every game needs the same architecture.

## What it is today

This repository currently contains a **fork of the [BRUTAL framework](https://github.com/ahwootech/BRUTAL)**. BRUTAL provides low-level C#/.NET building blocks including memory management, concurrency, native interop, Vulkan bindings, physics integrations and other systems. It is **not** a complete editor, scene system or JigsawEngine runtime.

JigsawEngine's planned engine-specific layers, benchmarks and sample game are described in the documents below. **They have not been implemented by this documentation overhaul.** Existing `Brutal.*` libraries are inherited foundation code; do not attribute the original framework or its production claims to JigsawEngine.

## Intended technical direction

| Area | Approach |
| --- | --- |
| **Primary language** | C# / .NET 10 for engine orchestration and gameplay systems; selective native interop only where measurement justifies it |
| **Foundation** | Existing BRUTAL fork, initially preserved rather than aggressively rewritten |
| **Scheduling** | Explicit task graph, dependencies and worker-thread budgets, built on evaluated existing primitives |
| **Simulation** | Fixed-step simulation where appropriate, with configurable substeps and deterministic testing for selected systems |
| **World representation** | Data-oriented storage for high-frequency components; stable handles and clear structural-change rules |
| **Rendering** | Evaluate the inherited Vulkan interfaces; keep render preparation and GPU work separated from simulation |
| **Instrumentation** | CPU scopes, allocation counts, job wait time, frame-time percentiles and reproducible scenario benchmarks |
| **Target games** | Systems-heavy shooters, immersive simulations and large-scale streamed games |

A job system or ECS is **not** a substitute for measurement. Performance comes from understanding the workload, data access and synchronization costs.

## Start here

- [Engine architecture](docs/JIGSAW_ARCHITECTURE.md) — module boundaries, execution model and technical decisions
- [Performance charter](docs/PERFORMANCE_CHARTER.md) — budgets, profiling rules and benchmark design
- [Delivery roadmap](docs/JIGSAW_ROADMAP.md) — phased work and acceptance criteria
- [BRUTAL upstream](https://github.com/ahwootech/BRUTAL) — original foundation and documentation

## First playable proof

The first proposed validation project is a **systems-heavy shooter testbed**: agents with perception and decision-making, projectiles, collision queries, animation state, streaming pressure and debug overlays. It should stress interacting systems—not just draw thousands of inert objects.

The milestone is successful when it can be built and run reproducibly, produces a per-system frame-time breakdown and meets a documented baseline on named hardware. No target FPS is promised before a baseline exists.

## Building the existing foundation

The upstream framework's libraries use .NET 10 and may require native dependencies, SDKs or hardware depending on the package. See the [original BRUTAL documentation](https://github.com/ahwootech/BRUTAL) for usage and prerequisites. There is not yet a single supported `dotnet run` command for a JigsawEngine editor or playable game.

## Origins, credits and licensing

JigsawEngine is being developed **from a fork of BRUTAL**, not as an independently authored replacement for it. The original framework, its authors and contributors deserve explicit credit. Existing `LICENSE.txt`, `NOTICE.txt`, third-party licenses and upstream source notices remain in place and govern the inherited material. Any future JigsawEngine-specific contributions must respect those terms. BRUTAL's existing product claims and examples belong to BRUTAL, not JigsawEngine.

**Build complex worlds. Measure everything.**
