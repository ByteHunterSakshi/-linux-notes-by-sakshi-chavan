# Navigating the Linux Landscape
**Notes by Sakshi Chavan**

---

## What is an Operating System?

The OS is the middle-man between you and the hardware. It manages memory, storage, running apps, I/O devices, security, and file/process organization. No OS = computer doesn't function.

## Types of Operating Systems

- **Batch OS** — processes jobs in groups, no live interaction
- **Time-Sharing OS** — multiple users share one system simultaneously
- **Distributed OS** — spans multiple connected machines
- **Real-Time OS** — used in embedded/control systems where timing is critical
- **Mobile OS** — phones, tablets
- **Desktop OS** — personal computers

## Where OSes show up in daily life

Opening apps, browsing, banking apps, media/documents, smart home devices — the OS is invisible but shapes speed, security, and usability everywhere.

## Windows vs Unix vs Linux

| | Windows | Unix | Linux |
|---|---|---|---|
| Made by | Microsoft | AT&T Bell Labs (originally) | Linus Torvalds + open-source community |
| Best known for | GUI, wide software support | Stability, enterprise use | Flexibility, free, customizable |
| Cost | Paid license | Often commercial/expensive | Free (GPL / open-source) |
| Source code | Closed | Varies | Open — anyone can inspect/modify |

Linux was created by **Linus Torvalds in 1991**, then grown by a global open-source community.

## Security angle

Linux is favored for security because:
- Strong permission model baked in
- Widely used on servers where stability/security is critical
- Open code = more eyes finding vulnerabilities fast

Windows has solid security too, but its sheer popularity makes it a bigger malware target.

## User Interfaces

- **GUI** — windows, icons, menus (GNOME, KDE, XFCE on Linux)
- **CLI** — text commands, faster for admins, essential for servers

Linux supports both — desktop environments for regular use, terminal for real power.

## What's a server?

A machine that provides a service to other machines/users over a network — web server, file server, DB server, mail server, app server. Built to run 24/7 and handle load.

## Desktop OS vs Server OS

| Desktop OS | Server OS |
|---|---|
| Ease of use, personal productivity | Reliability, security, networking, multitasking at scale |

Linux dominates server-side because it's stable, efficient, and scales well.

## Linux Architecture (4 layers)

```
User / Applications
        ↓
      Shell (Bash, Zsh, Sh)
        ↓
   Kernel / OS
        ↓
    Hardware
```

- **Hardware** — CPU, RAM, storage, peripherals
- **Kernel** — the core: manages processes, memory, drivers, syscalls
- **Shell** — command interpreter, your way of talking to the kernel
- **User/Apps** — browsers, editors, DBs, everything you actually use

---
*Notes by Sakshi Chavan — for personal learning & LinkedIn sharing*
