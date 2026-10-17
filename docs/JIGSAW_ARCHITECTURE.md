# JigsawEngine — proposed architecture

**Status:** design proposal; not an inventory of implemented engine modules.

## Guiding constraints

1. CPU work is budgeted per frame and measured by subsystem, not optimized by intuition.
2. Stable frame times and latency matter more than an isolated peak-throughput number.
3. Hot-path data ownership and mutation rules must be explicit.
4. A task is parallelized only if its granularity and synchronization costs justify it.
5. No blocking disk/network calls, unbounded queues or accidental allocations on latency-sensitive paths.
6. Preserve BRUTAL as an upstream foundation initially; add JigsawEngine-specific layers separately.

## Proposed layering

```text
Game / Testbed / Tools
          |
Gameplay + Simulation (AI, combat, physics integration, animation)
          |
World state + handles + event/command buffers
          |
Frame orchestration + dependency-aware task graph
          |
Platform / Memory / Interop / Rendering backends
          |
Existing BRUTAL libraries and native dependencies
```

These layers are planned interfaces. They are not claimed to exist today.

## Main-thread and worker model

- **Main/coordinator thread:** owns frame boundaries, input snapshots, lifecycle, synchronization points and final state publication.
- **Worker pool:** executes bounded tasks from an explicit dependency graph; avoid a thread per system or entity.
- **Simulation:** use a fixed timestep where it improves stability and testability, with a bounded catch-up policy to avoid a spiral of death.
- **Render preparation:** consume a defined snapshot of simulation state, generate draw/visibility work, and coordinate submission with backend-specific thread constraints.
- **I/O and streaming:** use asynchronous staging, cancellation and memory budgets; publish completed assets only at safe synchronization points.

### Example dependency graph

```text
Input snapshot
     |
Perception / spatial queries
     |
AI decisions  ----> Gameplay commands
     |                    |
Animation state      Physics step
     \                    /
      World-state commit
              |
       Render preparation
```

This is a conceptual graph; real dependencies must be established from read/write sets and measured on actual workloads.

## World-state representation

Evaluate archetype/chunk or sparse-set storage for high-frequency components. Do **not** commit to a universal ECS before a profiling testbed exists.

- Use stable generation-checked handles instead of long-lived raw pointers into movable storage.
- Batch structural changes at well-defined barriers.
- Keep hot arrays contiguous where access patterns benefit.
- Avoid false sharing with appropriate partitioning and padding, verified with profiles.
- Define serialization and versioning separately from in-memory layout.
- Treat gameplay extensibility and tooling as requirements alongside throughput.

## Engine-specific module candidates

| Proposed module | Responsibility |
| --- | --- |
| `Jigsaw.Runtime` | Frame loop, lifecycle, service boundaries |
| `Jigsaw.Tasks` | Dependency graph, scheduling policies, instrumentation |
| `Jigsaw.World` | Entity handles, component storage, state snapshots |
| `Jigsaw.Simulation` | Simulation orchestration, time stepping, event/command boundaries |
| `Jigsaw.Streaming` | Asset requests, residency budgets, background loading |
| `Jigsaw.Diagnostics` | Frame markers, counters, traces and benchmark output |
| `Jigsaw.Testbed` | Representative shooter workload and regression scenarios |

**None of these module names implies an existing project or API.** Add them incrementally with tests and an executable sample.

## Deliberate non-goals for the first phase

- Building a full visual editor before a runnable runtime and profiling baseline.
- Rewriting every BRUTAL library.
- Promising lock-free implementations for every data structure.
- Claiming deterministic simulation across hardware without dedicated validation.
- Treating Vulkan or native code as an automatic performance advantage.

## Open decisions

Benchmark task-graph integration against existing `Brutal.Concurrency`; evaluate whether ECS-style storage improves the target workload; choose the render pipeline after a minimal measured prototype; establish supported OS and hardware tiers after repeatable builds.
