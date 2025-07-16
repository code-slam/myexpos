# MyExpos Operating System

**MyExpos** is a pedagogical operating system built from scratch for a simulated environment. Inspired by the design of UNIX-style kernels, this project explores the core principles of operating systems through hands-on implementation — from bootstrapping to user management and virtual memory.

> 🚀 All 27 stages of the MyExpos roadmap were implemented — progressing from bare-metal boot code to a full-featured, multiprogramming OS with demand paging and a working shell.

---

## 🎯 Project Objective

This project was a deep dive into OS internals — not just learning, but **building everything from the ground up**:
- Custom bootloader
- Timer and disk interrupt handlers
- Round-robin scheduler
- File system with block-level access
- Shell and user programs
- Process management, semaphores, signals
- Multi-user login and virtual memory paging

---

## 📍 Development Methodology

The project followed the **27-stage roadmap** outlined by the [eXpOS specification](https://exposnitc.github.io/), which incrementally guides you through constructing a full OS. These stages include preparatory, intermediate, and advanced tasks such as:

- Boot and ABI setup
- Writing interrupt handlers (INT 4–15)
- Process creation (`Fork`, `Exec`, `Exit`)
- File handling and system call interface
- User management and paging

⚠️ While the roadmap was followed **completely**, the repository doesn't preserve each stage as a separate commit or folder. Instead:

- **All stages were developed and tested offline.**
- The repo reflects the **final OS version**, with select intermediate artifacts retained (`STAGE 22`, `STAGE 23`, etc.).
- All features through **Stage 27 (Pager Module)** are implemented.

---

## 🧠 Key Features

- ✅ Bootstrapping and OS loading via `boot_module.spl`
- ✅ Custom round-robin scheduler and process control
- ✅ Timer, disk, and software interrupt handling (INT 4 to INT 15)
- ✅ File system implementation with inode structures
- ✅ Shell (`shell.expl`) for command execution
- ✅ 20+ system calls across file, process, memory, and signal management
- ✅ Multi-user login and authentication
- ✅ Virtual memory with demand paging (`pager.spl`)

---

## 🛠️ Technologies

- **SPL (System Programming Language)** – Kernel-level modules
- **ExpL (Experimental Language)** – User-level programs
- **XSM Simulator** – Simulated hardware platform
- **XFS Interface** – Load compiled binaries to disk
- **Lex/Yacc, C** – Backend tooling for compilers and translators

---

## 📁 Repository Structure



.
├── spl/ # SPL kernel modules and utility code
│ └── spl_progs/ # All SPL programs (.spl) and compiled binaries (.xsm)
├── expl/ # ExpL compiler, user programs, and generated binaries
│ └── expl_progs/ # User programs in .expl format and compiled .xsm output
├── STAGES/ # Snapshots of code at various development stages
├── xsm/ # XSM simulator source (for debugging and customization)
├── xfs-interface/ # Interface to load binaries to the XSM disk
├── Makefile, *.txt # Configuration and support files
└── README.md # Project documentation


### 📌 Relevant File Types

- `*.spl` — Kernel modules and interrupt handlers (written in SPL)
- `*.expl` — User programs (written in ExpL)
- `*.xsm` — Compiled binaries for the XSM machine
- `library.lib` — Precompiled user library with system call implementations
- `boot_module.spl` — The system boot logic
- `scheduler.spl`, `disk.spl`, `exhandler.spl`, `console.spl` — Core kernel subsystems

---

## ✅ Key Kernel Modules

| SPL File   | Module Name                | Responsibility                               |
| ---------- | -------------------------- | -------------------------------------------- |
| `mod0.spl` | Resource Manager           | File descriptors, semaphores, memory blocks  |
| `mod1.spl` | Process Manager            | Process control blocks and scheduling queues |
| `mod2.spl` | Memory Manager             | Page tables, frame allocation                |
| `mod3.spl` | File Manager               | File operations logic                        |
| `mod4.spl` | Device Manager             | Console and disk interface                   |
| `mod5.spl` | Scheduler / Context Switch | Round-robin scheduler and context switching  |
| `mod6.spl` | Pager Module               | Demand paging and page fault handling        |
| `mod7.spl` | Boot Module                | Kernel bootstrap and module loader           |


---
| SPL File    | Purpose / System Calls Handled                     |
| ----------- | -------------------------------------------------- |
| `int4.spl`  | `Create`, `Delete` file operations                 |
| `int5.spl`  | `Open`, `Close`, `Seek` file operations            |
| `int6.spl`  | `Read` system call                                 |
| `int7.spl`  | `Write` system call                                |
| `int8.spl`  | `Fork` process creation                            |
| `int9.spl`  | `Exec` program execution                           |
| `int10.spl` | `Exit` system call                                 |
| `int11.spl` | `Getpid`, `Getppid`, `Wait`, `Signal`              |
| `int12.spl` | `Logout` user system call                          |
| `int13.spl` | `Semget`, `Semrelease` semaphore operations        |
| `int14.spl` | `SemLock`, `SemUnLock` semaphore locking           |
| `int15.spl` | `Shutdown` system call                             |
| `int16.spl` | `Newusr`, `Remusr`, `Setpwd`, `Getuname`, `Getuid` |
| `int17.spl` | `Login` system call                                |


---
| SPL File        | Purpose                                                |
| --------------- | ------------------------------------------------------ |
| `os_startup.spl`| OS startup code                                        |
| `disk.spl`      | Disk controller interrupt handler                      |
| `console.spl`   | Console I/O interrupt handler                          |
| `exhandler.spl` | Exception handler (invalid memory, illegal operations) |
| `timer.spl`     | Timer interrupt handler (for scheduling)               |


## ⚙️ Development Stages (Completed)

The OS was implemented across **27 progressive stages**, starting from basic bootloading and culminating in a feature-rich, multi-user OS:

- **Stages 1–12:** Setup, filesystem, bootstrap, interrupt/timer handling, ExpL programming, SPL debugging.
- **Stages 13–19:** Scheduler, loader, resource manager, disk/console handling, exception management.
- **Stages 20–27:** Process lifecycle (Fork/Exec/Exit), signal handling, semaphores, full file system support, user login & permissions, demand paging.

> ⚡ Final push includes all features up to Stage 27, after extensive offline development and validation.

---

## 💡 Example User Programs

You can find sample user programs in `expl/samples/` and `expl/expl_progs/`. These demonstrate system calls, file operations, process creation, synchronization, and more:

| Program | Function |
|---------|----------|
| `cat.expl` | Reads and prints file contents |
| `login.expl` | Multi-user login simulation |
| `gcd.expl` | Compute GCD of two numbers |
| `fork4.expl` | Demonstrates process forking |
| `read.expl`, `write.expl` | File I/O examples |
| `shell.expl` | A command-line shell implementation |

---

## 🧪 Testing and Debugging

- **XSM Debugger:** Used extensively to test program flow, memory layout, register values.
- **Unit Testing:** Performed for system calls and modules independently.
- **Stage Snapshots:** Intermediate code checkpoints preserved under `STAGES/`.

---

## 🎯 Future Work

- GUI-based shell for user interaction
- Extending paging to support swapping
- Implementing custom scheduling policies
- Multi-core support (Stage 28, not implemented yet)

---

## 👤 Author

**Ameen Aslam**  
🛠 [GitHub](https://github.com/yourusername) • 🔗 [LinkedIn](https://linkedin.com/in/yourprofile)

---

## 📜 Acknowledgements

While the system draws structural guidance from eXpOS and XSM resources, all design, implementation, testing, and tool development in this repository were carried out independently to explore and master systems-level programming.

---

## 📄 License

MIT License – feel free to explore and learn from this project.

