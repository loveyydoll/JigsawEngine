# Third-party licensing review — initial inventory

**Status:** preliminary repository-source review; not legal advice, not a complete dependency audit. Confirm requirements with counsel before commercial distribution.

## BRUTAL — inherited source

The repository's root `LICENSE.txt` is **BRUTAL License v1.0**, copyright © 2024 Ahwoo Limited. It is not the standard MIT license. The text grants broad use, modification and distribution rights subject to conditions. Relevant conditions in the checked-in text include:

- Retain copyright and permission notices in copies or substantial portions.
- For distributed products incorporating, linking to or built using the software or a substantial portion: include BRUTAL copyright in credits or equivalent.
- Display the specified unaltered BRUTAL logo before gameplay or primary function unless written permission or the stated non-graphics exception applies.
- Distribute `NOTICE.txt` alongside copies of the product.
- Preserve applicable licenses for redistributed third-party components.
- Review contribution terms and the New Zealand governing-law clause.

**Do not remove the root BRUTAL license or NOTICE while inherited BRUTAL code remains.** Do not describe the entire Community repository as MIT-licensed or automatically OSI-approved.

## Godot

Godot's main engine license is MIT, subject to its copyright/license notice requirements. Godot's `COPYRIGHT.txt` documents additional component-specific licenses. The .NET integration, runtime, native libraries, exported templates, addons and redistributed assets require version-specific checks. Using Godot .NET does not imply that all Jigsaw-authored gameplay code must be open-sourced.

References:
- https://github.com/godotengine/godot/blob/master/LICENSE.txt
- https://github.com/godotengine/godot/blob/master/COPYRIGHT.txt

## Jigsaw-authored code

Copyright in independently authored Jigsaw code can be retained by its lawful owner. A proprietary Studio edition and an open-source Community edition are possible, but public code should carry an explicit license chosen by its rights holders. **No new blanket license is applied by this document.** Contributions by other authors may require additional permission or a contributor agreement for proprietary relicensing.

## Required follow-up inventory

Before distribution, inventory and inspect each BRUTAL library's third-party license files, Godot version and export templates, NuGet dependency graph, native binaries, media assets, fonts, shader tools and packaging notices. Record component, version, source URL, license, modifications, attribution, distribution requirements and reviewer approval.

## Release gate

No public package or proprietary game should be marked legally cleared solely because this document exists. Require an actual dependency inventory, artifact inspection, and review of the final packaging and distribution model.
