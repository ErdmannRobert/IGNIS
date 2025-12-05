# Assembling an IGNIS Device

This document is intended for users who want to assemble an IGNIS device without participating in the development.

Reading `documentation/architecture.md` before starting assembly is recommended for a conceptual overview. 

## What is a Release?

A release is a frozen, reproducible snapshot of a device. Releases are structured by device > domain > version (for the domains electronics, firmware, mechanical and manual). 

All files in `releases/` are intended to be directly manufacturable or usable.

## Choosing Compatible Versions

IGNIS devices are versioned per domain. To find a set of compatible versions consult the `releases/<device>/<domain>/vX.Y/documentation/compatibility.json`. It defines which versions of other domains it is compatible with.

To assemble a device, choose:
1. Electronics version compliant with the same version of specifications as the rest of your IGNIS devices.
2. Mechanical and firmware version compatible with the electronics version.
3. Manual version compatible with the firmware version.

Usually the latest version of each domain is the best choice, nevertheless check compatibility before deciding. Additionally, make sure that the different IGNIS devices you want to build, all comply with the same version of the specifications.

- compatible_\<domain>_versions -> Compatibility of domain versions for assembling one device
- specifications_compliance -> Compatibility between different devices

## Manufacture and assemble

Assembly includes PCB assembly, mechanical assembly, and firmware flashing.
To assemble an IGNIS device, choose one version per domain and use the instructions in `releases/<device>/<domain>/vX.Y/documentation/assembly.md` to manufacture parts and assemble the device. 

## Required Skills

These are skills usually required for assembling an IGNIS device. 
- Soldering
- 3D printing
- Firmware flashing