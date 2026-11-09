# Xperia MSM8998 KernelSU Next

> **Status: PRE-ALPHA — integration patch preparation in progress.**
>
> No integrated kernel has been built, booted, or verified on hardware. The local WSL checkouts are not modified by this documentation repository.

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

## Pinned investigation sources
| Component | Branch | Commit |
|---|---|---|
| Kernel | `lineage-22.1` | `7a4c7d73f8ec401b89bd1ab815d2b4ccf801ec3f` |
| KernelSU Next | `legacy` | `b933b1f728116a456fbebf27b6a8772a640cdf23` |
| Maple defconfig | `lineage-msm8998-yoshino-maple_defconfig` | In the kernel source above |

The patch-preparation script refuses to operate on different source commits. Update the pins only after re-auditing the changed upstream source.

## Current status
| Work item | Status |
|---|---|
| Repository scaffold | Complete |
| Kernel source commit identified | Complete |
| Maple defconfig identified | Complete |
| KernelSU Next revision pinned | Complete |
| Kprobe/manual-hook feasibility audit | Complete |
| Manual hook patcher prepared | Prepared; not applied to the local WSL trees |
| Kernel built / device boot verified | Not tested |

See [docs/status.md](docs/status.md) and [docs/implementation-v1.md](docs/implementation-v1.md).

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
