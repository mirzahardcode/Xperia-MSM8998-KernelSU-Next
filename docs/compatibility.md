# Compatibility investigation

## Scope
Initial target: Sony Xperia XZ Premium (Maple), Qualcomm MSM8998, Linux 4.4.302 kernel family.

This is an investigation plan, not a compatibility claim.

## Questions
- Does the exact source match the running Pop Kernel 14-r3 build?
- Which Kprobe configuration and implementation exist in this tree?
- Are required symbols and hook points available in this build?
- Are kernel-version-specific adaptations or backports required?
- What are the device-specific boot image, DTB/DTBO, and packaging requirements?

## Integration modes
KernelSU Next documents non-GKI integration and a Legacy mode. Inspect and pin the current upstream instructions and source before selecting a method.

### Kprobe
Audit the actual kernel configuration and implementation. Enabling a config symbol alone does not prove the required hooks work.

### Manual integration
Review each proposed hook against the exact source and function signatures. Do not blindly copy examples from a different kernel version.

## Compatibility labels
- **Unknown:** not investigated.
- **Source-audited:** exact source and configuration inspected.
- **Build-tested:** proposed integration compiles.
- **Device-boot-tested:** device boots the resulting kernel.
- **Verified:** KernelSU is detected and tested on the stated device/ROM.

Labels apply only to the exact tested combination.
