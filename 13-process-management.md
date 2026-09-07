# Linux Process Management
**Notes by Sakshi Chavan**

---

## Process types

1. **Shell / interactive processes** — started from the command line, tied to the shell that launched them
2. **Daemons** — background services, usually start at boot, often run as root

## Process states

| State | Symbol | Meaning |
|---|---|---|
| Running | R | Actively using CPU |
| Sleeping | S | Waiting on an event |
| Uninterruptable sleep | D | Waiting on I/O, can't be interrupted |
| Stopped | T | Paused (e.g. via Ctrl+Z) |
| Zombie | Z | Finished but parent hasn't reaped it yet |

## Job control

```bash
command &      # start in background
Ctrl+Z          # pause current job
Ctrl+C            # kill current job
bg                  # resume a stopped job in the background
fg                    # bring background job to foreground
jobs                    # list current shell's jobs
```

**Example session:**
```bash
$ sleep 100 &
[1] 1234
$ sleep 200 &
[2] 1235
$ jobs
[1]-  Running    sleep 100 &
[2]+  Running    sleep 200 &

$ sleep 300
^Z
[3]+  Stopped    sleep 300
$ bg %3           # resume job 3 in background
$ fg %1            # bring job 1 to foreground
```

## Monitoring processes

```bash
ps -e         # all processes, standard syntax
ps aux          # all processes, BSD-style syntax (very common)
top                 # live interactive monitor
```

**Custom fields with `ps -eo`:**
```bash
ps -eo pid,user,ni,comm,%cpu,%mem
```

| Field | Meaning |
|---|---|
| pid | Process ID |
| user | Owner |
| ni | Nice value (priority) |
| comm | Command name |
| %cpu | CPU usage |
| %mem | Memory usage |

## Priority / nice values

- Range: **-20** (highest priority) to **19** (lowest priority)
- Default: **0**
- Lower nice value = more CPU priority
- Only root can set negative values; regular users can only make things *less* prioritized

**Start a process with a priority:**
```bash
nice -n 10 command
```

**Change priority of a running process:**
```bash
renice -n -10 -p PID
```

## Killing processes

```bash
kill -l          # list all signals
kill PID           # graceful termination (SIGTERM)
kill -9 PID           # force kill (SIGKILL)
kill -1 PID             # reload config (SIGHUP)
kill -19 PID               # stop the process
kill -18 PID                  # resume the process
kill -3 PID                     # trigger a core dump (debugging)
```

**Graceful-then-forceful pattern:**
```bash
$ sleep 1000 &
[1] 1234
$ kill 1234           # try graceful first
[1]+  Terminated      sleep 1000
$ kill -9 1234          # only if it's unresponsive
```

## Finding & identifying processes

```bash
pgrep -a sleep      # find processes matching name, with args
pidof sleep            # get PID(s) of a running command
pstree                    # visualize the process tree
```

## System-level info

```bash
uptime      # how long system's been up + load average
```

## My takeaways

- `ps aux` for a one-time snapshot, `top` for live monitoring
- `kill` before `kill -9` — give processes a chance to clean up
- `nice`/`renice` are underused — great for keeping background jobs from hogging CPU
- Zombie processes (`Z`) aren't dangerous by themselves, but a pile of them usually means the parent process has a bug in how it handles child cleanup

---
*Notes by Sakshi Chavan — for personal learning & LinkedIn sharing*
