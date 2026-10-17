# Private Studio bootstrap guide

**This public document is setup guidance only.** Do not store proprietary source, private tokens, internal architecture details or unreleased game assets here.

1. Create a **private** repository named `loveyydoll/JigsawEngine-Studio` through GitHub repository creation. Initialize with a README; do not select a blanket license yet.
2. Confirm repository visibility is private before uploading any confidential material. Restrict access to trusted collaborators and enable branch protections and secret scanning where available.
3. Establish Studio's original-code ownership, third-party source boundaries and license manifest. Do not assume BRUTAL becomes proprietary because its source is copied into a private repository.
4. Integrate Godot .NET as the editor/presentation host and evaluate BRUTAL libraries selectively. Pin dependency versions and retain required notices.
5. Build a minimal executable integration sample and automated tests before implementing complex simulation systems.
6. Maintain a reviewed allowlist for future Community exports; use clean export commits rather than a direct mirror or automatic public push.
7. Seek qualified legal review before commercial distribution or a contribution/relicensing program.

The existing `loveyydoll/JigsawEngine` repository remains public and is the intended future Community repository. Previously public material does not become secret by moving a copy into Studio.
