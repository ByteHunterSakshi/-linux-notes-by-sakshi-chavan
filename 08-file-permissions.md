# File Permissions in Linux
**Notes by Sakshi Chavan**

---

## Why permissions exist

- **Security** — control who touches what
- **Privacy** — keep sensitive data protected
- **Integrity** — stop unauthorized changes
- **Multi-user** — safely share resources between many users

## The 3 user categories

1. **Owner (u)** — whoever created/owns the file
2. **Group (g)** — anyone in the file's group
3. **Others (o)** — literally everyone else

## The 3 permission levels

| Permission | Symbol | Number | On a file | On a directory |
|---|---|---|---|---|
| Read | `r` | 4 | Open/view contents | List directory contents |
| Write | `w` | 2 | Modify contents | Create/delete/modify items inside |
| Execute | `x` | 1 | Run as a program/script | `cd` into it |

## Permission dependencies (the part people forget)

**To access a directory's contents:**
- Need `r` to *list* what's inside
- Need `x` to actually *access* files inside
- No `x` → you can see filenames but can't touch the files
- No `r` → you can access files if you already know their exact names, but can't browse

**To modify a directory's contents:**
- Need both `w` AND `x`
- Without `x`, `w` alone won't let you create/delete anything

**To execute a file:**
- Need `x` on the file itself
- AND `x` on every parent directory in the path

**To modify a file:**
- Need `w` on the file
- AND `x` on its parent directory

## Reading `ls -l` output

```
-rwxr-xr-- 1 john developers 4096 Mar 15 14:30 script.sh
```

| Part | Meaning |
|---|---|
| `-` | File type (`-`=file, `d`=directory, `l`=symlink...) |
| `rwx` | Owner permissions |
| `r-x` | Group permissions |
| `r--` | Others permissions |
| `1` | Hard link count |
| `john` | Owner |
| `developers` | Group |
| `4096` | Size in bytes |
| `Mar 15 14:30` | Last modified |
| `script.sh` | Filename |

**File type symbols:**

| Symbol | Type | Example |
|---|---|---|
| `-` | Regular file | `/etc/passwd` |
| `d` | Directory | `/home` |
| `l` | Symlink | `/etc/grub.conf` |
| `b` | Block device | `/dev/vdb` |
| `c` | Character device | `/dev/pts/0` |
| `s` | Socket | `/dev/log` |
| `p` | Named pipe | `/dev/initctl` |

## Changing ownership — `chown` / `chgrp`

```bash
chown john script.sh                     # change owner
chown john:developers file.txt            # change owner + group together
chown -R john /home/project                # recursive
chown --reference=file1 file2               # copy owner from another file

chgrp developers script.sh                 # change group only
chgrp -R developers /home/project           # recursive
```

Note: `chown`/`chgrp` only touch **ownership** — they never change the actual rwx permissions.

## Changing permissions — `chmod`

### Symbolic notation
```bash
chmod [who][operator][permission] file
```
- **who:** `u` owner, `g` group, `o` others, `a` all
- **operator:** `+` add, `-` remove, `=` set exactly
- **permission:** `r`, `w`, `x`

```bash
chmod u+x script.sh          # owner gets execute
chmod g+rw file.txt           # group gets read+write
chmod o-w file.txt              # others lose write
chmod a=rx file.txt               # everyone gets exactly read+execute
chmod u+w,g-x,o=r file.txt          # multiple changes at once
chmod -R g+w directory/               # recursive
```

### Numeric notation

| Value | Perm |
|---|---|
| 4 | r |
| 2 | w |
| 1 | x |

| Number | Combo |
|---|---|
| 7 | rwx |
| 6 | rw- |
| 5 | r-x |
| 4 | r-- |
| 3 | -wx |
| 2 | -w- |
| 1 | --x |
| 0 | --- |

```bash
chmod 755 script.sh     # owner: rwx, group: r-x, others: r-x
chmod 644 file.txt        # owner: rw-, group: r--, others: r--
chmod 600 secret.txt        # only owner can read/write
chmod -R 755 directory/       # recursive
```

## Common combos to just memorize

| Perm string | Numeric | Typical use |
|---|---|---|
| `-rw-------` | 600 | Private file, owner only |
| `-rw-r--r--` | 644 | Standard file, readable by all |
| `-rwx------` | 700 | Private script/dir |
| `-rwxr-xr-x` | 755 | Standard shared script/dir |

## Security notes to self

- Never use `777` unless you truly have no other option
- Always apply the **principle of least privilege**
- Double-check before running `chmod`/`chown` with `-R` — it hits *everything* underneath

---
*Notes by Sakshi Chavan — for personal learning & LinkedIn sharing*
