# Linux File System Hierarchy
**Notes by Sakshi Chavan**

---

## Why the hierarchy exists

Linux follows the **Filesystem Hierarchy Standard (FHS)** — a fixed tree structure starting at root `/`, so every distro (Ubuntu, CentOS, Debian...) looks broadly similar. This gives:

- Predictable file locations
- Easier admin & maintenance
- Better security boundaries
- Consistent tooling across distros

## Root-level directories, decoded

| Path | What lives there |
|---|---|
| `/` | Root of everything |
| `/bin` | Essential commands everyone can run (`ls`, `cp`, `mkdir`) |
| `/sbin` | Admin-only commands (`ifconfig`, `iptables`) |
| `/boot` | Bootloader + kernel images |
| `/dev` | Device files (disks, terminals, USB) |
| `/etc` | System-wide config files |
| `/home` | Personal user directories |
| `/lib` | Shared system libraries |
| `/media` | Removable media (USB drives etc.) |
| `/mnt` | Temporary mount points |
| `/opt` | Third-party/optional software |
| `/proc` | Virtual files — live process/system info |
| `/root` | Root user's home directory |
| `/run` | Runtime process data |
| `/srv` | Data served by services (e.g. web server files) |
| `/sys` | Kernel & hardware info |
| `/tmp` | Temp files, often auto-cleared |
| `/usr` | User apps, libraries, docs, shared resources |
| `/var` | Data that changes constantly — logs, caches, mail, DBs |

## Navigating around

```bash
pwd          # where am I
ls           # what's here
ls -a        # include hidden files
ls -l        # long/detailed listing
cd /home     # jump to /home
cd ..        # go up one level
cd ~         # go home
```

## Creating & managing files/dirs

```bash
mkdir documents          # new folder
touch file.txt           # new empty file
mv oldname newname        # rename
cp source.txt dest.txt    # copy a file
cp -r folder1 folder2      # copy a folder (recursive)
rm file.txt                # delete a file
rm -r folder                # delete a folder recursively
```

## Reading/editing file contents

```bash
cat file.txt      # dump whole file
less file.txt      # scroll through, page by page
head file.txt        # first few lines
tail file.txt          # last few lines
nano file.txt            # edit in a simple terminal editor
```

## Terminal shortcuts worth memorizing

| Shortcut | Effect |
|---|---|
| `Tab` | Auto-complete |
| `Ctrl+C` | Kill current command |
| `Ctrl+L` | Clear screen |
| `Ctrl+A` | Jump to line start |
| `Ctrl+E` | Jump to line end |
| `Ctrl+U` | Delete everything before cursor |
| `Ctrl+K` | Delete everything after cursor |
| `Ctrl+W` | Delete previous word |
| `Ctrl+R` | Search command history |
| `↑ / ↓` | Browse previous commands |

---
*Notes by Sakshi Chavan — for personal learning & LinkedIn sharing*
