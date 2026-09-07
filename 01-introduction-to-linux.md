# Introduction to Linux
**Notes by Sakshi Chavan**

---

## What is Linux?

Linux is a **free, open-source, Unix-like operating system**. It sits between your hardware and every application you run — managing memory, processes, files, and devices so software doesn't have to talk to the hardware directly.

Unlike Windows or macOS, Linux isn't owned by one company. Its source code is public, so anyone can read it, modify it, and redistribute it.

## Where Linux came from

- Created by **Linus Torvalds in 1991**, originally as a personal/hobby project
- Built on Unix principles (Unix itself dates back to AT&T Bell Labs)
- Grew into a global open-source project maintained by thousands of contributors worldwide
- Released under the **GPL (GNU General Public License)** — free to use, study, modify, and share

## Why "Linux" isn't really one thing

Technically, **Linux is just the kernel** — the core piece that talks to hardware. What people call "a Linux system" is the kernel + a huge collection of tools (many from the GNU Project) + a package manager + (optionally) a desktop environment, all bundled together into a **distribution (distro)**.

## Popular Linux distributions

| Distro | Known for |
|---|---|
| Ubuntu | Beginner-friendly, huge community, great documentation |
| Debian | Rock-solid stability, the base many other distros build on |
| CentOS / RHEL / Rocky/Alma | Enterprise & server environments |
| Fedora | Cutting-edge features, sponsored by Red Hat |
| Arch Linux | Minimal, build-it-yourself, for advanced users |
| Kali Linux | Security testing / penetration testing |

All of them share the same kernel underneath — the differences are in packaging, defaults, and philosophy.

## Where Linux actually runs

- Personal computers & laptops
- **Servers** (the vast majority of the internet's web servers run Linux)
- **Cloud platforms** (AWS, Azure, GCP all run heavily on Linux under the hood)
- **Android** — Android's core is built on the Linux kernel
- Embedded systems & IoT devices (routers, smart TVs, cars, etc.)
- Supercomputers — nearly all of the world's fastest supercomputers run Linux

## Why Linux is so widely used

- **Free and open source** — no licensing cost, full transparency
- **Highly customizable** — swap out almost any component
- **Strong security model** — permissions, user isolation, and open code that many eyes can audit
- **Stability & uptime** — servers can run for months/years without a reboot
- **Large, active community** — help is almost always a search away
- **Efficient on resources** — runs well even on modest hardware

## Core architecture, in one picture

```
User / Applications   → browsers, editors, servers, databases
        ↓
      Shell            → Bash, Zsh, Sh — how you talk to the system
        ↓
   Kernel              → manages processes, memory, drivers, syscalls
        ↓
    Hardware           → CPU, RAM, disk, network, peripherals
```

- **Kernel** — the heart of Linux. Handles process scheduling, memory management, device drivers, and system calls.
- **Shell** — the command interpreter between you and the kernel. This is what you're actually typing into in a terminal.
- **Applications** — everything you actually use day to day.

## Linux philosophy — the ideas that shape everything else

- **Everything is a file** — devices, processes, sockets, all represented as files you can interact with
- **Small tools that do one thing well** — chained together with pipes (`|`) to build powerful workflows
- **Multi-user by design** — built from the ground up to support many users on one machine safely
- **Text-based configuration** — most system config lives in readable text files, not hidden binary settings

## Command Line vs GUI

Linux gives you both:
- **GUI (Graphical User Interface)** — desktop environments like GNOME, KDE, XFCE for everyday use
- **CLI (Command Line Interface)** — the terminal, where real system administration and automation happens

Most serious Linux work (servers, DevOps, scripting) happens entirely through the CLI — no desktop environment needed at all.

## My takeaways

- Linux ≠ a single OS, it's a *kernel* + an ecosystem of distros built around it
- Almost everything I'll learn going forward (permissions, processes, users, shell) applies across every distro, because the kernel and core philosophy stay the same
- Getting comfortable in the terminal is non-negotiable if you want to actually work with Linux professionally

---
*Notes by Sakshi Chavan — for personal learning & LinkedIn sharing*
