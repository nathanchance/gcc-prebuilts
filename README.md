# DEPRECATION NOTICE

This repo will no longer be updated as I don't have the time. You can compile these toolchains yourself with either [crosstool-NG](https://crosstool-ng.github.io) or my [build-tools-gcc](https://github.com/nathanchance/build-tools-gcc) repo. For Linaro toolchains, you can download their prebuilts on [their releases site](https://releases.linaro.org/components/toolchain/binaries/).

# Prebuilt GCC toolchains

These are my personal toolchains, cross compiled for arm and arm64. They will always be up to date with the latest stable GCC (currently 7.1.1). I use them for compiling [Flash Kernel](https://github.com/nathanchance/angler). They are compiled with [crosstool-NG](http://crosstool-ng.github.io).


## Supported operating systems

Most if not all versions of 64-bit Linux should work with these as they are statically linked. Let me know if there are any issues following the questions section below.


## Variants

* A standard GNU version, build straight from the [gcc-7-branch](https://git.linaro.org/toolchain/gcc.git/log/?h=gcc-7-branch)
* A Linaro version, currently compiled from the [linaro-local/gcc-7-integration-branch](https://git.linaro.org/toolchain/gcc.git/log/?h=linaro-local/gcc-7-integration-branch) branch

| Architecture | GCC source | Branch             | Prefix                        | Tarball link |
| ------------ | ---------- | ------------------ | ----------------------------- | ------------ |
| arm          | GNU        | arm-gnu-7.x        | arm-gnu-linux-androideabi-    | [Link](https://raw.githubusercontent.com/nathanchance/gcc-prebuilts/tarballs-7.x/arm-gnu-linux-androideabi.tar.xz) |
| arm          | Linaro     | arm-linaro-7.x     | arm-linaro-linux-androideabi- | [Link](https://raw.githubusercontent.com/nathanchance/gcc-prebuilts/tarballs-7.x/arm-linaro-linux-androideabi.tar.xz) |
| arm64        | GNU        | aarch64-gnu-7.x    | aarch64-gnu-linux-android-    | [Link](https://raw.githubusercontent.com/nathanchance/gcc-prebuilts/tarballs-7.x/aarch64-gnu-linux-android.tar.xz) |
| arm64        | Linaro     | aarch64-linaro-7.x | aarch64-linaro-linux-android- | [Link](https://raw.githubusercontent.com/nathanchance/gcc-prebuilts/tarballs-7.x/aarch64-linaro-linux-android.tar.xz) |


## Using these toolchains

To use these toolchains, you first need to do a shallow clone (to avoid pulling too much history):

```bash
git clone -b <branch> --depth=1 https://github.com/nathanchance/gcc-prebuilts
```

Then point your cross compiler to the toolchain. For kernels, you can do the following:

```bash
export CROSS_COMPILE=$(pwd)/gcc-prebuilts/bin/<prefix>
```

Alternatively, if you are really short on space and don't want to clone a git repo, you can fetch the latest toolchain using the link above either via curl or wget directly to your terminal.

For kernels, you must have the following four commits:
+ [Makefile: Fix device not booting with GCC 7.x and above](https://github.com/nathanchance/angler/commit/406d54a7f006142372157d4fb49d7e76a5564d00)
+ [Revert "scripts: gcc-wrapper: Use wrapper to check compiler warnings"](https://android.googlesource.com/kernel/msm/+/e7fb62baa7c8b803d7e3b3f3d8bf4e2b916b659d)
+ [kernel: use the gnu89 standard explicitly](https://github.com/torvalds/linux/commit/51b97e354ba9fce1890cf38ecc754aa49677fc89)
+ [compiler-gcc: integrate the various compiler-gcc\[345.h\] files](https://github.com/torvalds/linux/commit/cb984d101b30eb7478d32df56a0023e4603cba7f)

The last two commits are from Linux upstream. The first is only needed if your version is 3.10.79 or earlier. The second is needed for both 3.10 (3.10.101 or earlier) and 3.18 (3.18.31 or earlier). I do [recommend upstreaming your kernels](https://forum.xda-developers.com/android/software-hacking/reference-how-to-upstream-android-kernel-t3626913) but if you choose not to, just pick that commit.


## Compiling these toolchains

If you would like to learn how to compile these toolchains, please give [this README](https://github.com/nathanchance/build-tools-gcc/blob/master/README.md) a glance.


## Questions?

If you have any questions or issues, please open an issue on this repo or the [build-tools-gcc](https://github.com/nathanchance/build-tools-gcc) repo OR make a post in [the XDA thread](https://forum.xda-developers.com/android/development/toolchains-gnu-linaro-5th-2017-t3606941) and I'll do my best to assist you.
