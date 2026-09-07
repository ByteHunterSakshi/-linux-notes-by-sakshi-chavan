# Archiving & Compression
**Notes by Sakshi Chavan**

---

## Archiving vs Compression — don't mix these up

**Archiving** = bundling multiple files/folders into one file, preserving structure. Doesn't shrink anything by itself.

**Compression** = actually reducing file size by squeezing out redundant data.

> `tar` archives but does **not** compress unless you tell it to.

## Common uses for archiving

```bash
tar -cvf backup.tar /home/user/Documents     # backups
tar -cvf project.tar project/                 # packaging for transfer
tar -cvf logs_2025.tar /var/log                # organizing old data
```

## `tar` basics

```bash
tar [options] archive_name files
```

| Option | Meaning |
|---|---|
| `-c` | Create archive |
| `-x` | Extract archive |
| `-v` | Verbose |
| `-f` | Specify filename |
| `-t` | List contents |

```bash
tar -cvf archive.tar file1 file2       # create
tar -xvf archive.tar                    # extract here
tar -xvf archive.tar -C /home/user/Desktop   # extract elsewhere
tar -tvf archive.tar                          # list contents
tar -xvf archive.tar filename                  # extract just one file
```

## Why compress at all

Smaller storage footprint, faster transfers, less bandwidth, cheaper backups.

## Compression formats compared

| Format | Ext | Speed | Ratio | CPU use | Best for |
|---|---|---|---|---|---|
| gzip | `.gz` | Fast | Good | Low | General purpose |
| bzip2 | `.bz2` | Medium | Better | Medium | Backups |
| xz | `.xz` | Slow | Best | High | Software packages |

## Standalone compression commands

```bash
gzip file.txt         # → file.txt.gz, original removed
gzip -k file.txt        # keep original
gzip *.txt                 # multiple files
gunzip file.txt.gz            # decompress (or: gzip -d file.txt.gz)

bzip2 file.txt          # → file.txt.bz2
bzip2 -k file.txt         # keep original
bunzip2 file.txt.bz2         # decompress (or: bzip2 -d file.txt.bz2)

xz file.txt              # → file.txt.xz
xz -k file.txt              # keep original
unxz file.txt.xz               # decompress (or: xz -d file.txt.xz)
```

## Combining tar + compression (the practical, real-world way)

```bash
# gzip
tar -czvf archive.tar.gz directory/
tar -xzvf archive.tar.gz

# bzip2
tar -cjvf archive.tar.bz2 directory/
tar -xjvf archive.tar.bz2

# xz
tar -cJvf archive.tar.xz directory/
tar -xJvf archive.tar.xz
```

Compression flags for `tar`:

| Flag | Method |
|---|---|
| `-z` | gzip |
| `-j` | bzip2 |
| `-J` | xz |

## Quick-reference summary table

| Task | Command |
|---|---|
| Create archive | `tar -cvf archive.tar files` |
| Extract archive | `tar -xvf archive.tar` |
| List archive | `tar -tvf archive.tar` |
| gzip compress/decompress | `gzip file` / `gunzip file.gz` |
| bzip2 compress/decompress | `bzip2 file` / `bunzip2 file.bz2` |
| xz compress/decompress | `xz file` / `unxz file.xz` |
| tar+gzip | `tar -czvf archive.tar.gz dir` |
| tar+bzip2 | `tar -cjvf archive.tar.bz2 dir` |
| tar+xz | `tar -cJvf archive.tar.xz dir` |

## My takeaways

- **gzip** → fastest, my default for everyday use
- **bzip2** → better ratio, worth it for backups where speed isn't critical
- **xz** → best ratio, save it for distribution/packaging where you can afford the CPU time

---
*Notes by Sakshi Chavan — for personal learning & LinkedIn sharing*
