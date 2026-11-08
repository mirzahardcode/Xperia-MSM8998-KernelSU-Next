# Build guide (planned)

This guide remains a checklist until the exact source revision and build system are confirmed.

## Host environment
Initial maintainer environment: Windows with WSL Ubuntu. Required packages and toolchain must be derived from the target kernel tree and its build instructions.

## Before building
1. Confirm the exact source commit matching the installed kernel.
2. Read the kernel repository README and build scripts.
3. Identify the correct defconfig and toolchain version.
4. Record environment variables and build commands.
5. Build the unmodified kernel as a baseline.
6. Preserve build logs and artifact checksums.

## Do not assume
- A generic Android NDK is necessarily the correct kernel compiler.
- A defconfig can be guessed from the device codename.
- A successful build will boot.
- An image can be flashed before packaging and recovery are confirmed.

Detailed commands will be added only after reproduction against a pinned source revision.
