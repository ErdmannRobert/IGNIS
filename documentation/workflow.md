## 0 Glossary

-   Device: A self-contained unit in the IGNIS ecosystem (e.g., hub_heavy). May include electronics, firmware, and mechanical domains.
-   Domain: electronics / firmware / mechanical / manual.
-   Specification: Cross-device contract such as connector pinouts or protocols.
-   Release: Archived version with reproducible artifacts.

## 1 Git workflow -> Trunk based development

-   ### 1.1 Branches
    -   `main`
        -   Every release is tagged.  
        -   The trunk; Always buildable and working.
        -   Only squashed merges from feature branches
        -   No non-reviewed or experimental direct commits
    -   `feature/*`
        -   One branch per feature, e.g.:
        -   Merged into main when complete and tested.
        -   Deleted after merge
        -   `feature/<device>/<topic>`
        -   Has to be rebased when main is updated 
-   ### 1.2 Development Process -> one branch per feature or change
    -   Step 1 — Develop in feature/*
    -   Step 2 — Update Documentation 
    -   Step 3 — Merge `feature/*` into main
-   ### 1.3 Release Process -> one release per new version
    -   Step 1 — Archive artifacts corresponding to "4 Versioning"
    -   Step 2 — Create `changelog.md`
    -   Step 2 — Tag the release
        -   `<device>-<domain>-vX.Y`
        -   Example: hub_heavy-electronics-v1.0
-   ### 1.4 Commit Practices
    -   No generated artifacts in the development folders (they only belong in `releases/`)
-   ### 1.5 Contribution Workflow (Fork-Based)
    -   Step 1 — Fork the repo
    -   Step 2 — Create feature branch in fork
    -   Step 3 — Submit pull request into main

## 2 Folder Structure -> Active development in `<domain>/<device>/`

-   `electronics/`     → editable KiCad project sources
-   `firmware/`        → editable firmware sources
-   `mechanical/`      → CAD & 3D models
-   `manual/`          → Player-facing Puzzle solving instructions and riddle explanations. 
-   `assets/`          → branding, icons, reusable design assets
-   `specifications/`  → interface & protocol definitions
-   `releases/`        → archived production builds per domain
-   `documentation/`   → project wide documentation, as architecture and workflow
-   ### 2.1 Naming Conventions
    -   All lowercase, snake_case folders:
        -   hub_heavy
        -   module_generic
    -   Assets
        -   `assets/logo/default`
        -   `assets/logo/high_contrast`
-   ### 2.2 Libraries
    -   Domain-wide libraries in `<domain>/libraries/`
    -   Libraries are versioned inside `<domain>/libraries/<library>/vX.Y/`

## 3 Documentation

-   Project wide documentation in `documentation/`
    -   Project workflow
    -   Project architecture
    -   read `documentation/readme.md` for more information
-   Specifications in `specifications/`
    -   All used interfaces & protocols should be fully defined 
    -   Act as a contract between devices
    -   Example: Riddle module slot specs
-   Device documentation per domain in `<domain>/<device>/documentation/`
    -   Interface documentation in `documentation.md`
    -   Compatibility matrix in `compatibility.json`
        -   electronics:
            -   "specifications_compliance": {"specA": ["vX.Y"]}
        -   firmware:
            -   "compatible_electronics_versions": ["vX.Y"]
            -   "specifications_compliance": {"specA": ["vX.Y"]}
        -   mechanical:
            -   "compatible_electronics_versions": ["vX.Y"]
            -   "specifications_compliance": {"specA": ["vX.Y"]}
        -   manual:
            -   "compatible_firmware_versions": ["vX.Y"]
            -   "specifications_compliance": {"specA": ["vX.Y"]}
    -   Development requirements in `dev_requirements.md` -> Tools needed for development and artifact generation
        -   Electronics -> KiCad version: X.X.X; Required plugins: …
        -   Firmware -> Compiler toolchain: ARM GCC X.X
        -   Mechanical -> CAD software version (e.g., FreeCAD 0.21)
    -   Assembly instructions in `assembly.md` -> Instructions on how to use the artifacts to assembly the device
        -   How to use the artifacts to build the IGNIS device
        -   Skills required
        -   Instructions
    -   Inner-workings documentation separately inside source files (comments)
-   A `changelog.md` is created inside each version folder in `releases/<device>/<domain>/vX.Y/`.
    -   Version changes
    -   Date & Author

## 4 Versioning

-   ### 4.1 Devices -> Versioning per domain per device in `releases/<device>/<domain>/vX.Y/`
    -   In general
        -   Build artifacts
        -   State of the device-domain documentation at time of versioning 
            -   `documentation.md` & `compatibility.json` & `assembly.md`
            -   `dev_requirements.md` is not versioned, as it's only relevant for development and artifact creation
        -   Major version on breaking changes, otherwise minor version
        -   Each domain is versioned independently.  
            -   Electronics, mechanical, firmware and manual versions do not need to align numerically.
    -   Electronics
        -   New version whenever the PCB is sent to manufacturing.
        -   Even failed boards get their own version.
        -   KiCad gerbers, BOM, footprints
    -   Mechanical
        -   New version whenever a part is physically printed or machined.
        -   STLs, STEP
        -   When 3D printing 3MF with Slicer settings and GCODE
    -   Firmware
        -   Versioned when a known-good firmware build is ready.
        -   Firmware binaries
    -   Manual
        -   State of the manual at time of versioning
-   ### 4.2 Dependencies 
    -   Assets
        -   Assets do not have versions — only variants
        -   Minor fixes update in-place.
        -   Major redesign = new variant.
    -   Specifications
        -   Versioning in `specifications/<specification>/vX.Y/`
        -   v0.x are provisional specifications and are intended for prototyping and validation
    -   Domain-wide libraries
        -   Libraries are versioned inside `<domain>/libraries/<library>/vX.Y/`