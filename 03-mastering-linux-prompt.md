# Mastering the Linux Prompt
**Notes by Sakshi Chavan**

---

## Reading the prompt

A typical prompt:

```bash
user@hostname:~$
```

Breaking it down:
- `user` → who you're logged in as
- `hostname` → the machine's name
- `~` → current directory (`~` = home)
- `$` → regular user | `#` → root user

Example: `student@devbox:~/Documents$` → user `student`, machine `devbox`, currently inside `~/Documents`, regular privileges.

## Basic terminal workflow

| Step | Command | Purpose |
|---|---|---|
| 1 | Open terminal | Start your session |
| 2 | `pwd` | Where am I? |
| 3 | `ls` / `ls -l` | What's here? |
| 4 | `cd <dir>` | Move around |
| 5 | `touch file.txt` / `mkdir folder` | Create stuff |
| 6 | `rm file.txt` / `rmdir folder` | Delete stuff |
| 7 | `exit` | Close session |

## Core commands cheat sheet

| Command | Does |
|---|---|
| `pwd` | Show current directory |
| `ls` | List files/folders |
| `cd` | Change directory |
| `mkdir` | Make a directory |
| `touch` | Make an empty file |
| `cp` | Copy files |
| `mv` | Move/rename files |
| `rm` | Delete files |
| `cat` | Print file contents |
| `clear` | Wipe the terminal screen |

## Good terminal habits

- Type carefully, read the output
- `Tab` → auto-complete file/command names
- `↑` arrow → recall previous commands (huge time-saver)
- Use the terminal for anything repetitive/scriptable — it's built for automation

## System info commands worth knowing

```bash
uname -a     # kernel info
whoami       # who am I logged in as
hostname     # machine name
date         # current date/time
uptime       # how long has this box been running
df -h        # disk usage, human-readable
free -h      # memory usage, human-readable
```

---
*Notes by Sakshi Chavan — for personal learning & LinkedIn sharing*
