# Project status and verification log

Last updated: 2026-11-09

## Phase: PRE-ALPHA — manual integration patch preparation

The investigation sources and Maple defconfig are pinned. A local patch-preparation script has been generated and checked against upstream source anchors. It has **not** been run against the user's local WSL working trees from this session. No kernel build, image, boot, or device verification has occurred.

## Pinned source revisions
| Component | Branch | Commit |
|---|---|---|
| Kernel | `lineage-22.1` | `7a4c7d73f8ec401b89bd1ab815d2b4ccf801ec3f` |
| KernelSU Next | `legacy` | `b933b1f728116a456fbebf27b6a8772a640cdf23` |

Target defconfig: `arch/arm64/configs/lineage-msm8998-yoshino-maple_defconfig`.

## Investigation checklist
- [x] Identify exact kernel source commit used for this investigation.
- [x] Identify Maple defconfig.
- [x] Pin a specific KernelSU Next Legacy revision.
- [x] Audit Kprobe configuration and the unsupported-kernel warning.
- [x] Map manual hook call sites and handler signatures.
- [x] Audit ARM64 compat STAT paths.
- [x] Audit Kconfig/Kbuild integration points.
- [x] Identify automatic backports in KernelSU Kbuild and prepare explicit equivalents.
- [x] Identify and prepare a compat-aware EXEC SULOG adapter.
- [ ] Apply the patcher to the user's local WSL working trees.
- [ ] Review local diffs and run `git diff --check`.
- [ ] Reproduce an unmodified baseline build.
- [ ] Build the integrated kernel.
- [ ] Document image packaging and tested recovery method.
- [ ] Build and test on hardware only after recovery preparation.
- [ ] Verify boot, stability, and KernelSU Manager detection.

## Important implementation notes
- Manual call sites are guarded by `CONFIG_KSU_MANUAL_HOOK` to avoid duplicate calls in a dynamic-hook build.
- VFS read is hooked at `vfs_read()`, covering the normal VFS read entry path rather than only the `read(2)` wrapper.
- STAT covers native pathname handling, STAT64 pathname handling, native `newfstat`, `fstat64`, and compat `newfstat` result layout.
- EXEC SULOG must treat `argv` as `struct user_arg_ptr`, not as a kernel `char **`; the patcher adds a compat-aware reader.
- KernelSU Kbuild contains shell `sed -i` backports. The patcher applies the detected 4.4 backports explicitly so the first build should not need to mutate these source files automatically.

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
