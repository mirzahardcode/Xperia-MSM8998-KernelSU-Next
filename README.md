# Xperia MSM8998 KernelSU Next

> **Status: PRE-ALPHA — documentation and preparation only.**
>
> KernelSU Next has **not** been integrated, built, booted, or verified in this project.

Community investigation for KernelSU Next Legacy on Sony Xperia XZ Premium (Maple, Qualcomm MSM8998), targeting the Linux 4.4.302 kernel family.

## Goals
- Identify the exact kernel source revision and configuration used by the target ROM.
- Evaluate Kprobe feasibility and the manual integration path for this exact tree.
- Maintain reproducible build notes, reviewable patches, and device-specific recovery guidance.
- Publish compatibility claims only after real-device verification.

## Initial device notes (unverified)
| Item | Reported value |
|---|---|
| Device | Sony Xperia XZ Premium |
| Codename | Maple |
| SoC | Qualcomm Snapdragon 835 / MSM8998 |
| ROM | Unofficial LineageOS 22.1 |
| Kernel release | `4.4.302-linckandrea-Pop-Kernel-14-r3-p/81bff733` |
| Bootloader | Unlocked |

These are initial notes from one device, not a guarantee for every Maple variant or ROM build.

## Current status
| Work item | Status |
|---|---|
| Repository scaffold | In progress |
| Exact source commit identified | Not yet |
| Matching defconfig identified | Not yet |
| KernelSU Next revision pinned | Not yet |
| Kprobe support audited | Not yet |
| Manual integration reviewed | Not yet |
| Kernel built / device boot verified | Not tested |

See [docs/status.md](docs/status.md).

## Safety
- Do not flash an unverified kernel image.
- Preserve a known-good original image and a tested recovery path.
- Confirm exact model, partition layout, ROM packaging, and source revision first.
- A successful compile does not prove the kernel will boot.
- KernelSU integration does not guarantee third-party apps will accept a rooted device.

## Upstream references
- [KernelSU Next](https://github.com/KernelSU-Next/KernelSU-Next)
- [Non-GKI integration guide](https://kernelsu-next.github.io/webpage/pages/how-to-integrate-for-non-gki.html)
- [Arman-ATI MSM8998 kernel](https://github.com/Arman-ATI/android_kernel_sony_msm8998)
- [Arman-ATI Maple device source](https://github.com/Arman-ATI/android_device_sony_maple)

No upstream kernel source is vendored here.

## Contributions
See [CONTRIBUTING.md](CONTRIBUTING.md). Include exact commits, build logs, device/ROM details, and test evidence. Untested work must be labeled experimental.

## Licensing
See [LICENSE-NOTES.md](LICENSE-NOTES.md) before adding code. Preserve upstream license notices and attribution.
