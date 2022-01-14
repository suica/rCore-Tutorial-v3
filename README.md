# rCore-Tutorial-v3
rCore-Tutorial version 3.5. See the [Documentation in Chinese](https://rcore-os.github.io/rCore-Tutorial-Book-v3/).

Official QQ group number: 735045051

## news
- 2021.11.20: Now we are updating our labs. Please checkout chX-dev Branches for our current new labs. (Notice: please see the [Dependency] section in the end of this doc)

## Overview

This project aims to show how to write an **Unix-like OS** running on **RISC-V** platforms **from scratch** in **[Rust](https://www.rust-lang.org/)** for **beginners** without any background knowledge about **computer architectures, assembly languages or operating systems**.

## Features

* Platform supported: `qemu-system-riscv64` simulator or dev boards based on [Kendryte K210 SoC](https://canaan.io/product/kendryteai) such as [Maix Dock](https://www.seeedstudio.com/Sipeed-MAIX-Dock-p-4815.html)
* OS
  * concurrency of multiple processes each of which contains mutiple native threads
  * preemptive scheduling(Round-Robin algorithm)
  * dynamic memory management in kernel
  * virtual memory
  * a simple file system with a block cache
  * an interactive shell in the userspace
* **only 4K+ LoC**
* [A detailed documentation in Chinese](https://rcore-os.github.io/rCore-Tutorial-Book-v3/) in spite of the lack of comments in the code(English version is not available at present)

## Run our project

TODO:

## Working in progress

Our first release 3.5.0 (chapter 1-7) has been published.

There will be 9 chapters in our next release 3.6.0, where 2 new chapters will be added:
* chapter 8: synchronization on a uniprocessor
* chapter 9: I/O devices

Current version is 3.6.0-alpha.1 and we are still working on it.

Here are the updates since 3.5.0:

### Completed

* [x] automatically clean up and rebuild before running our project on a different platform
* [x] fix `power` series application in early chapters, now you can find modulus in the output
* [x] use `UPSafeCell` instead of `RefCell` or `spin::Mutex` in order to access static data structures and adjust its API so that it cannot be borrowed twice at a time(mention `& .exclusive_access().task[0]` in `run_first_task`)
* [x] move `TaskContext` into `TaskControlBlock` instead of restoring it in place on kernel stack(since ch3), eliminating annoying `task_cx_ptr2`
* [x] replace `llvm_asm!` with `asm!`
* [x] expand the fs image size generated by `rcore-fs-fuse` to 128MiB
* [x] add a new test named `huge_write` which evaluates the fs performance(qemu\~500KiB/s k210\~50KiB/s)
* [x] flush all block cache to disk after a fs transaction which involves write operation
* [x] replace `spin::Mutex` with `UPSafeCell` before SMP chapter
* [x] add codes for a new chapter about synchronization & mutual exclusion(uniprocessor only)
* [x] bug fix: we should call `find_pte` rather than `find_pte_create` in `PageTable::unmap`
* [x] clarify: "check validity of level-3 pte in `find_pte` instead of checking it outside this function" should not be a bug
* [x] code of chapter 8: synchronization on a uniprocessor

### Todo(High priority)

* [ ] review documentation, current progress: 5/9
* [ ] switch the code of chapter 6 and chapter 7
* [ ] code of chapter 9: device drivers based on interrupts, including UART and block devices
* [ ] use old fs image optionally, do not always rebuild the image
* [ ] add new system calls: getdents64/fstat
* [ ] shell functionality improvement(to be continued...)
* [ ] give every non-zero process exit code an unique and clear error type
* [ ] effective error handling of mm module

### Todo(Low priority)

* [ ] rewrite practice doc and remove some inproper questions
* [ ] provide smooth debug experience at a Rust source code level
* [ ] format the code using official tools
* [ ] support other platforms


### Crates

We will add them later.
