# Project status and verification log

Last updated: 2026-11-08

## Phase: PRE-ALPHA

Documentation scaffold only. No KernelSU code, patch, kernel image, or build artifact is included.

## Investigation checklist
- [ ] Confirm exact device variant (G8141/G8142) and ROM build fingerprint.
- [ ] Match the running Pop Kernel 14-r3 build to an exact source commit.
- [ ] Record source branch, commit SHA, and local patches.
- [ ] Identify the actual defconfig used by the ROM build.
- [ ] Capture the effective kernel .config where possible.
- [ ] Audit Kprobe configuration and implementation in this exact 4.4.302 tree.
- [ ] Review and pin a specific KernelSU Next upstream revision.
- [ ] Determine whether Legacy integration works without source adaptations.
- [ ] Review any manual hook against exact source and function signatures.
- [ ] Reproduce an unmodified baseline build.
- [ ] Document image packaging and tested recovery method.
- [ ] Build and test on hardware only after recovery preparation.
- [ ] Verify boot, stability, and KernelSU Manager detection.

## Evidence required for a "working" claim
1. Exact kernel source commit and patch commit.
2. Toolchain and build configuration.
3. Build log and output artifact metadata.
4. Device model and ROM build.
5. Evidence the device boots the new kernel.
6. Evidence KernelSU is detected and functions.
7. Known limitations and recovery notes.

A successful compile is **Build-tested**, not **Device-verified**.

## Test record template
```text
Date:
Tester:
Device model:
ROM build:
Kernel source repository / branch / commit:
KernelSU Next commit:
Defconfig:
Toolchain:
Build result:
Boot result:
KernelSU Manager result:
Artifact checksums:
Known issues:
Recovery method tested:
```
