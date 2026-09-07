# Text Processing: find, grep, sort, uniq
**Notes by Sakshi Chavan**

---

## `find` — search files/dirs by condition

```bash
find <search_path> <options> <required-parameters>
```

| Option | What it filters by | Example |
|---|---|---|
| `-name` | filename | `find /etc -name passwd` |
| `-perm` | permission bits | `find /home -perm 644` |
| `-size` | file size | `find / -size +100M` |
| `-user` | owner | `find / -user cbz` |
| `-uid` | user ID | `find / -uid 1005` |
| `-group` | group | `find / -group admin` |
| `-gid` | group ID | `find / -gid 1006` |
| `-amin` | access time (min) | `find /boot -amin -1` |
| `-mmin` | modify time (min) | `find /etc -mmin -1` |
| `-atime` | access time (days) | `find / -atime -7` |
| `-mtime` | modify time (days) | `find / -mtime -7` |
| `-empty` | empty files | `find / -empty` |
| `-executable` | executable files | `find / -executable` |
| `-type` | file type | `find / -type f` |
| `-exec` | run a command on results | `find / -exec rm {} \;` |

**`-type` values:** `f` file, `d` directory, `l` symlink, `c` char device, `b` block device, `s` socket, `p` named pipe.

### Examples I actually use

**By name:**
```bash
find /etc -name passwd
find /home -name "*.txt"
find /home -iname "*.txt"        # case-insensitive
```

**By permission:**
```bash
find /home -perm 644              # exact match
find /home -perm -644              # at least these bits
find /home -perm /u=x                # any exec bit set for owner
```

**By size:**
```bash
find / -size +100M      # bigger than 100MB
find / -size -1M          # smaller than 1MB
find / -size 100M           # exactly 100MB
```

**By time:**
```bash
find /etc -mmin -1        # modified in the last minute
find / -atime -7            # accessed in last 7 days
find / -mtime +30             # modified more than 30 days ago
```

**By owner:**
```bash
find / -user cbz
find / -group admin
find / -nouser              # orphaned files, no valid owner
```

**Combining conditions:**
```bash
find /home -name "*.txt" -mtime -7        # recent txt files
find / -size +100M -user cbz                # big files owned by cbz
find / -type d -empty                         # empty directories
```

**Acting on results with `-exec`:**
```bash
find / -name authorized_keys -exec cp -rv {} /home \;
find / -type f -name passwd -exec rm -rf {} \;
find /home -type f -name "*.txt" -exec chmod 644 {} \;
```

> ⚠️ **Careful:** always test `find` commands *without* `-exec`/`-delete` first before running destructive actions — one wrong flag can wipe the wrong files.

---

## `sort` — sort lines of text

```bash
sort flower.txt          # alphabetical, default
sort -r flower.txt          # reverse order
sort -n numbers.txt           # numeric sort
sort -u flower.txt              # sort + remove duplicates
```

## `grep` — search for patterns

```bash
grep "pattern" file.txt         # basic search
grep -i "pattern" file.txt        # case-insensitive
grep -n "pattern" file.txt          # show line numbers
grep -c "pattern" file.txt            # count matches
grep -v "pattern" file.txt              # invert match (show non-matches)
grep -C 2 "pattern" file.txt              # show 2 lines of context around match
```

## `uniq` — dedupe lines (adjacent only!)

```bash
uniq flower.txt          # remove consecutive duplicate lines
uniq -c flower.txt          # count occurrences of each line
uniq -d flower.txt            # show only duplicated lines
uniq -u flower.txt              # show only unique (non-duplicated) lines
sort flower.txt | uniq             # sort first, then dedupe (catches ALL dupes)
```

> `uniq` only catches duplicates that are next to each other, so pairing it with `sort` first is the standard pattern for catching every duplicate in a file.

## Chaining commands together

```bash
sort flower.txt | grep "pattern"
```

## My takeaways

- `grep` is my go-to for quick pattern hunting in logs
- `sort | uniq -c` is the classic combo for "count how many times each line appears"
- Always quote patterns in `grep` to stop the shell from expanding wildcards before grep even sees them
- `find ... -exec` is powerful but dangerous — dry-run first

---
*Notes by Sakshi Chavan — for personal learning & LinkedIn sharing*
