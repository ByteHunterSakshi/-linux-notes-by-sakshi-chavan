# Links, sudo & umask
**Notes by Sakshi Chavan**

---

## Link counts

The link count in `ls -l` = how many names point to the same underlying data (inode).

```bash
ls -l file.txt        # basic
ls -li file.txt         # includes inode number
```

**Directories:** minimum link count is always **2** (itself + its `.` entry), plus one more for every subdirectory's `..` entry pointing back up. A folder with 3 subfolders → link count 5.

**Regular files:** default link count is **1**, goes up when you add hard links.

## Hard links vs symbolic (soft) links

```bash
ln original.txt hard_link.txt      # hard link
ln -s original.txt soft_link.txt    # symbolic link
```

| | Hard link | Soft (symbolic) link |
|---|---|---|
| Inode | Same as original | Different |
| Size | Same | Different |
| Permissions | Same | Different |
| Can point to a directory? | No | Yes |
| Survives if original deleted? | Yes (still has the data) | No (breaks / dangling link) |

## sudo — why it matters

- **Security**: controlled root access, audit trail, time-limited sessions
- **Flexibility**: fine-grained, per-user, per-command permissions
- **Accountability**: every command is logged and traceable to a person

**Regular commands** run with your own limited permissions:
```bash
ls /home
cat /etc/passwd
```

**sudo commands** run elevated:
```bash
sudo ls /root
sudo cat /etc/shadow
```

## The sudoers file

Location: `/etc/sudoers` — **always edit with `visudo`**, never directly (it validates syntax before saving).

```bash
sudo visudo
```

Syntax:
```
who where=(as_whom) what
```

Examples:
```bash
username ALL=(ALL) ALL                              # full access everywhere
username ALL=(ALL) /usr/bin/ls, /usr/bin/cat          # only specific commands
username ALL=(ALL) NOPASSWD: /usr/bin/ls                # no password prompt
%groupname ALL=(ALL) ALL                                  # whole group gets access
```

**Good practices for sudoers:**
- Use full paths to commands
- Avoid wildcards where you can
- Use `NOPASSWD` sparingly — only for genuinely low-risk commands
- Review sudo logs regularly

**Checking/debugging:**
```bash
sudo -l                          # what can I run with sudo?
sudo visudo -c                    # validate sudoers syntax
sudo cat /var/log/auth.log | grep sudo   # audit trail
```

## umask — controlling default permissions

Every new file/directory gets permissions based on a starting point minus the umask.

- Directories start at `777`
- Files start at `666` (execute bit is never set by default on new files)

```bash
umask          # view current umask
```

| User type | Default umask | Resulting dir perm | Resulting file perm |
|---|---|---|---|
| Root | 0022 | 755 | 644 |
| Standard user | 0002 | 775 | 664 |

**Math:**
```
Directory: 777 - umask = actual permission
File:      666 - umask = actual permission
```

**Changing it:**
```bash
umask 000              # temporary, session-only
```

**Permanently, system-wide** → edit `/etc/profile`:
```bash
if [ $UID -gt 199 ] && [ "`/usr/bin/id -gn`" = "`/usr/bin/id -un`" ]; then
    umask 002    # standard users
else
    umask 000    # root
fi
```

**Permanently, per-user** → edit `~/.profile` and add:
```bash
umask 002
```
> Per-user setting in `~/.profile` overrides the system-wide one for that account.

**Common umask values:**

| Umask | Dirs | Files |
|---|---|---|
| 0000 | 777 (wide open) | 666 |
| 0022 | 755 | 644 |
| 0002 | 775 | 664 |
| 0077 | 700 (locked down) | 600 |

**My takeaways:**
- `umask` only affects **newly created** files — existing files need `chmod`
- Lower umask = more permissive, higher umask = more restrictive
- 077 for anything sensitive/private, 022 for typical servers, 002 for shared dev environments

---
*Notes by Sakshi Chavan — for personal learning & LinkedIn sharing*
