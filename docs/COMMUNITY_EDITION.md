# JigsawEngine Community Edition — public architecture

**Status: proposal, not an implemented distribution or license grant.**

JigsawEngine Community is intended to be a streamlined, publicly developed edition of a separately maintained proprietary JigsawEngine Studio. The private Studio repository is the development source of truth; eligible code may be extracted into Community through reviewed releases. Nothing in this document implies that a private repository has been created.

## Public architecture boundaries

- **Godot .NET** is the intended editor, scene, rendering, input and presentation host. Start with the standard .NET-enabled Godot editor rather than an independent Godot fork.
- **Jigsaw.Core** is a proposed independent C# simulation/orchestration library, with explicit fixed-step execution, contiguous data storage, stable handles and diagnostics.
- **Jigsaw.Godot** is a proposed integration adapter: publish bounded simulation state to Godot on safe threads, avoiding direct Godot scene-tree calls from arbitrary workers.
- **BRUTAL** is an inherited third-party foundation, not original JigsawEngine code. Evaluate selected libraries rather than importing redundant rendering, physics or scheduler subsystems by default.
- **Jigsaw.Diagnostics** and a reproducible sample game are required before performance claims.

These projects do not yet exist in the current repository unless separately implemented. The current repository is primarily inherited BRUTAL source and architecture documents.

## Proposed release process

1. Review every candidate file's authorship, license and dependency closure.
2. Export only explicitly allowlisted source files and necessary build assets; never mirror the private repository automatically.
3. Scan for secrets, internal URLs, confidential assets, game-specific proprietary logic and unpublished documentation.
4. Retain upstream notices and required license files, including third-party assets and binary dependencies.
5. Verify that the resulting edition is genuinely redistributable under its stated licenses; do not label all inherited code MIT.
6. Build, test and package the public edition independently.
7. Record the source revision, provenance, dependency versions and approvals for each release.

Community contributors' terms must be settled before accepting contributions intended for reuse in Studio. An open-source license alone does not automatically grant relicensing rights for every contribution.

## Next engineering milestone

Create a small .NET Godot integration sample backed by a standalone Jigsaw.Core library. Audit the actual BRUTAL build structure first: the current `Brutal.Core` and `Brutal.Maths` directories do not contain the previously assumed project files at their roots. Build reproducibility and performance measurements precede micro-optimization.
