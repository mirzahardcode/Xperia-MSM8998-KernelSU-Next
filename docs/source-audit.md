# Initial upstream source audit

Date: 2026-11-08

## Candidate source

Repository: https://github.com/Arman-ATI/android_kernel_sony_msm8998  
Branch: `lineage-22.1`  
Branch head inspected: `7a4c7d73f8ec401b89bd1ab815d2b4ccf801ec3f`  
Commit date: 2025-01-17  
Commit message: `kernel: Update kernel version names`

The branch Makefile reports Linux 4.4.302. This makes it a strong candidate for the target ROM family, but it does **not** yet prove that this exact commit produced the user's installed Pop Kernel 14-r3 binary.

## Maple configuration candidates

The branch contains:
- `arch/arm64/configs/lineage-msm8998-yoshino-maple_defconfig`
- `arch/arm64/configs/lineage-msm8998-yoshino-maple_dsds_defconfig`

The user's reported device is G8141. Do not choose a defconfig solely from the model string; confirm the ROM build's actual build configuration and compare the effective running kernel config first.

## Kprobe-related options observed

The Maple defconfig contains:
- `CONFIG_KPROBES=y`
- `CONFIG_HAVE_KPROBES=y`
- `CONFIG_KPROBE_EVENT=y`

This is encouraging evidence that the kernel tree has Kprobe support configured. It is **not** proof that KernelSU Next's required hook implementation works on this exact kernel. Further source-level inspection and an integration build are required.

## Next checks

- [ ] Compare exact running kernel build identity with source commit history and ROM build scripts.
- [ ] Confirm which Maple defconfig the ROM build uses.
- [ ] Inspect Kprobe implementation and arm64 backend in this source tree.
- [ ] Inspect the pinned KernelSU Next Legacy setup script and its required symbols/hooks.
- [ ] Determine whether any required option is missing or named differently in this 4.4 tree.
- [ ] Reproduce an unmodified baseline build before integrating anything.

## References

- Kernel source branch: https://github.com/Arman-ATI/android_kernel_sony_msm8998/tree/lineage-22.1
- Candidate Maple defconfig: https://github.com/Arman-ATI/android_kernel_sony_msm8998/blob/lineage-22.1/arch/arm64/configs/lineage-msm8998-yoshino-maple_defconfig
- Candidate Maple DSDS defconfig: https://github.com/Arman-ATI/android_kernel_sony_msm8998/blob/lineage-22.1/arch/arm64/configs/lineage-msm8998-yoshino-maple_dsds_defconfig
