<div align="center">
<img src="https://repository-images.githubusercontent.com/825143915/95735661-0205-4029-97d5-fcfa347c8067" width="45%" height="45%>


# 

[![License](https://img.shields.io/github/license/SafaOS/SafaOS?color=red)](https://github.com/SafaOS/SafaOS/blob/main/LICENSE) ![Org's Stars](https://img.shields.io/github/stars/SafaOS?style=flat-square)
</div>

An open-source non-Unix-like OS, written from scratch in Rust for fun.
<details>
  <summary>Screenshots</summary>

  ## Screenshots
  ![aarch64](https://safiworks.github.io/imgs/screenshots/SafaOS-3.0.1-aarch64.png "aarch64 on v0.3.1")

  ![real-hardware](https://safiworks.github.io/imgs/screenshots/SafaOS-3.0.1-rlhw.jpg "real hardware running v0.3.1 with a connected USB Keyboard")  

  ![x86_64](https://safiworks.github.io/imgs/screenshots/SafaOS-3.0.1-x86_64.png "x86_64 on v0.3.1")

  ![running lua](https://safiworks.github.io/imgs/screenshots/SafaOS070525.png "running lua on v0.2.1")

  ![running tests](https://safiworks.github.io/imgs/screenshots/SafaOS-3.0.1-tests.png "running tests on v0.3.1")
</details>

## See also
- [SafaOS](https://github.com/SafaOS/SafaOS): the main repo, also contains the kernel implementition.
- [safa-api](https://github.com/SafaOS/safa-api): an API over the SafaOS kernel, also contains documenation.
- [salibc](https://github.com/SafaOS/libc): a libc implementition over the `safa-api`.
- [rust](https://github.com/SafaOS/rust/tree/stable): rust port (currently only the rust standard library is ported which internally uses the `safa-api`).

## Overview
### What makes SafaOS a unique (hobby OS)?
I am trying my best to stay as unique as possible in the hobby OS space, altough SafaOS is currently not that interesting here is what i tried too far:

- **not unix or NT like**
- **multi-architecture**:
SafaOS is a multi-architecture OS unlike most hobby OSes, supporting both `x86_64` and `aarch64`

- **rust first design**:
it isn't unix-like and therefore allows for a more rust-like design, for example syscall arguments don't relay on null termination and expect a length, pointer arguments has references' requirements, also the rust standard library doesn't relay on a libc internally but rather the `safa-api` which is written in 100% rust.

### Architectures
- AArch64: Only tested `qemu-virt` but it should work on any machine with: GICV3, a GICITS, a generic timer, PCIe(optional), and UEFI
- x86_64: tested on both real hardware and qemu

### Drivers
- XHCI
- USB HID Keyboard
- PS/2 Keyboard (x86_64 only)
- labeled VFS which includes these filesystems
  - `proc:/`: similar to unix's `/proc`, contains read-only data of mostly json that the kernel provides for example: `cpuinfo`, `meminfo`, `kernelinfo`, `eve-journal`, and process related information `[PID]/info`
  - `dev:/`: similar to unix's `/dev`, contains a read-write interface over some of the system drivers such as the TTY `dev:/tty`, altough i have plans to revmap or remove both `proc` and `dev` 
  - `sys:/`: contains system files, and global binaries in `sys:/bin`
  - `ram:/`: a playground ramdisk
- more architecture specific drivers, such as the `ACPI` for x86_64, and the `GIC` for aarch64
