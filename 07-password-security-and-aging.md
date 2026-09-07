# Password Security, Aging & Groups (Deep Dive)
**Notes by Sakshi Chavan**

---

## Why password security matters

Passwords are the first line of defense on any account. Rules of thumb:
- Long, unique, never reused across systems
- Enforce minimum length + expiration + lockout policies
- Never stored in plain text — Linux hashes them in `/etc/shadow`

## `passwd` command, all the flags I actually use

```bash
passwd                       # change my own password
sudo passwd username         # change someone else's password
sudo passwd -l username      # lock the account
sudo passwd -u username      # unlock the account
sudo passwd -e username      # force password change at next login
```

Only root (or someone with the right privileges) can touch another user's password.

## Password policy — `/etc/login.defs`

| Setting | Meaning |
|---|---|
| `PASS_MAX_DAYS` | Max password age before forced change |
| `PASS_MIN_DAYS` | Min days before it can be changed again |
| `PASS_WARN_AGE` | Days of warning before expiry |

**PAM modules** enforce password *quality*:
- `pam_pwquality.so` — strength checks
- `pam_unix.so` — standard auth
- Install `libpam-pwquality` to enforce strong passwords system-wide.

## Locking / unlocking / expiring accounts

```bash
sudo passwd -l username                    # lock
sudo usermod -L username                    # lock (alt method)

sudo passwd -u username                     # unlock
sudo usermod -U username                     # unlock (alt method)

sudo usermod -e 2026-12-31 username           # expire account on a date
sudo chage -E 2026-12-31 username              # same, via chage
```

A **locked** account can't authenticate at all until unlocked. An **expired** account is cut off from logging in past its expiry date.

## Decoding `/etc/shadow`

Each line = 9 colon-separated fields:

```
username:hash:last_change:min_days:max_days:warn:inactive:expire:reserved
```

| # | Field | Meaning |
|---|---|---|
| 1 | Username | Login name |
| 2 | Password hash | Never the plain password, only its hash |
| 3 | Last changed | Days since Jan 1 1970 |
| 4 | Min days | Cooldown before changing again |
| 5 | Max days | Forced expiry window (`99999` ≈ never) |
| 6 | Warn days | Heads-up window before expiry |
| 7 | Inactive days | Grace period after expiry before disable |
| 8 | Account expiry | Hard cutoff date, empty = never |
| 9 | Reserved | Unused |

## `chage` — the go-to tool for aging rules

```bash
chage -l username              # view current aging settings
chage -m 7 username             # min 7 days between changes
chage -M 90 username             # force change every 90 days
chage -W 7 username               # warn 7 days before expiry
chage -E 2026-12-31 username       # set expiry date
chage -d 0 username                  # force change at next login
```

## Groups, one level deeper

`/etc/group` format:
```
groupname:password:GID:user1,user2,...
```

`/etc/gshadow` format:
```
groupname:encrypted_password:admins:members
```

**Group types:** primary (your main group), secondary (extra memberships), system (used by daemons), regular (user-organizing).

**Create / delete:**
```bash
sudo groupadd developers
sudo groupdel developers      # fails if it's still someone's primary group
```

**Rename / renumber:**
```bash
sudo groupmod -n devteam developers   # rename
sudo groupmod -g 1500 devteam          # change GID
```

**Membership:**
```bash
sudo usermod -aG developers alice      # add (append!)
sudo gpasswd -d alice developers        # remove
sudo gpasswd -a alice developers         # add, alt method
```

⚠️ Same gotcha as before: **always use `-a` with `-G`** or you wipe out other group memberships.

**Viewing:**
```bash
cat /etc/group
getent group
cat /etc/gshadow
```

Prefer `groupadd` / `groupmod` / `groupdel` / `gpasswd` / `usermod` over hand-editing these files directly.

---
*Notes by Sakshi Chavan — for personal learning & LinkedIn sharing*
