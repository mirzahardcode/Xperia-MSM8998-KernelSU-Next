# Manual Hook Integration v1 — implementation notes

## Exact source pins

- Kernel: `Arman-ATI/android_kernel_sony_msm8998`, branch `lineage-22.1`, commit `7a4c7d73f8ec401b89bd1ab815d2b4ccf801ec3f`.
- KernelSU Next: `KernelSU-Next/KernelSU-Next`, branch `legacy`, commit `b933b1f728116a456fbebf27b6a8772a640cdf23`.
- Target config: `arch/arm64/configs/lineage-msm8998-yoshino-maple_defconfig`.

These exact pins are enforced by the companion patch-preparation script. If a local checkout differs, the script refuses to continue rather than applying a patch to unreviewed source.

## What the patcher changes

### Kernel repository
- Creates `work/ksu-next-manual-hook-v1` from the pinned `lineage-22.1` branch.
- Adds the `drivers/kernelsu` symlink to the sibling KernelSU `kernel/` directory.
- Registers KernelSU in `drivers/Kconfig` and `drivers/Makefile`.
- Enables `CONFIG_KSU=y` and `CONFIG_KSU_MANUAL_HOOK=y` in the Maple defconfig.
- Adds manual hook call sites to `fs/exec.c`, `fs/open.c`, `fs/read_write.c`, `fs/stat.c`, `fs/compat.c`, and `kernel/reboot.c`.
- Applies the 4.4 SELinux, seccomp, and `path_umount` backports explicitly.

### KernelSU Next repository
- Creates `work/manual-hook-adapter-v1` from the pinned `legacy` branch.
- Adds a compat-aware SULOG adapter for the `struct user_arg_ptr` passed by the manual EXEC hook.
- Generalizes init.rc STAT result size adjustment for native `struct stat`, `struct stat64`, and `struct compat_stat`.

## Hook choices

- EXEC: `do_execveat_common()`, after the `IS_ERR(filename)` check.
- FACCESSAT: `SYSCALL_DEFINE3(faccessat)`.
- READ: `vfs_read()`, so the hook covers VFS reads beyond only the `read(2)` syscall.
- STAT: native `newfstatat`, `fstatat64`, native `newfstat`, `fstat64`, and compat `newfstat`.
- REBOOT: before the normal `CAP_SYS_BOOT` permission check.

All kernel call sites are guarded by `CONFIG_KSU_MANUAL_HOOK`; they should not be active in a dynamic-hook build.

## Run the companion script

The script is supplied as a conversation attachment named `apply_manual_hook_v1.py`. Copy it into WSL, then run its read-only preflight first:

```bash
python3 apply_manual_hook_v1.py
```

When the preflight reports both exact commits, clean worktrees, and all expected anchors, run:

```bash
python3 apply_manual_hook_v1.py --apply
```

It creates isolated branches in both local repositories, writes the source changes, and creates the local symlink. It does **not** stage, commit, build, or flash. It aborts on modified worktrees, unexpected revisions, conflicting branches, or missing source anchors.

After application, review both trees:

```bash
git -C ~/kernel-lab/msm8998-4.4.302 status --short
git -C ~/kernel-lab/msm8998-4.4.302 diff --check
git -C ~/kernel-lab/msm8998-4.4.302 diff --stat

git -C ~/kernel-lab/KernelSU-Next status --short
git -C ~/kernel-lab/KernelSU-Next diff --check
git -C ~/kernel-lab/KernelSU-Next diff --stat
```

Do not build until the full diffs have been reviewed. In particular, confirm the generated `drivers/kernelsu` symlink resolves to the intended sibling repository.

## Validation limits

- The script's Python syntax was checked.
- Its required text anchors were checked against the pinned upstream file contents.
- The patcher was **not executed against the user's local WSL filesystem** in this session.
- No kernel compilation or boot verification has been performed.
