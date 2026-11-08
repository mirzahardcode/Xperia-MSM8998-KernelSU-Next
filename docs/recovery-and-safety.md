# Recovery and device safety

Kernel development can make a device temporarily unbootable. This repository does not yet provide a tested flashing recipe.

Before any device write:
- Confirm exact model and partition layout.
- Keep a known-good original boot/kernel image and verify its provenance.
- Confirm a working recovery/restore path for the installed ROM.
- Ensure battery and host connection are reliable.
- Determine whether the ROM uses a boot image, AnyKernel-style package, or another format.
- Never use an image built for another Maple variant or ROM base.
- Do not proceed if the original image or restore path is uncertain.

An unlocked bootloader does not prevent failed flashes or data loss. Back up important data independently.
