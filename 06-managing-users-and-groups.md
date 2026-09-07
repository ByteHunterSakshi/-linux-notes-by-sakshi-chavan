# Managing Users & Groups in Linux
**Notes by Sakshi Chavan**

---

## Types of users

| Type | Notes |
|---|---|
| **Root** | UID 0, unrestricted access to everything |
| **System users** | Created for services/daemons, usually no login shell |
| **Regular users** | Real humans, have home dirs, limited access |

## Creating a user — `adduser`

```bash
sudo adduser alice
```
This is the friendly, interactive wrapper (as opposed to raw `useradd`) — it prompts for password/full name, auto-creates a home directory, applies default shell + system templates.

Useful variants:
```bash
sudo adduser --home /home/alice alice
sudo adduser --shell /bin/bash alice
sudo adduser --ingroup developers alice
```

## Setting passwords — `passwd`

```bash
sudo passwd alice        # set/change alice's password
sudo passwd -l alice     # lock the account
sudo passwd -u alice     # unlock the account
```

## Groups

Groups exist so you don't have to assign permissions to every single user one by one.

```bash
sudo groupadd developers              # create a group
sudo usermod -aG developers alice     # add alice to it (-a = append, -G = supplementary groups)
groups alice                          # check alice's groups
sudo gpasswd -d alice developers      # remove alice from the group
```

⚠️ **Important:** always use `-aG` together. If you drop the `-a`, `usermod` will *replace* the user's supplementary groups instead of adding to them — easy way to accidentally lock someone out of things.

## Deleting a user

```bash
sudo deluser alice                    # remove user
sudo deluser --remove-home alice      # also wipes their home directory
```

## Files that actually store this stuff

| File | Contains |
|---|---|
| `/etc/passwd` | Basic account info |
| `/etc/shadow` | Encrypted password hashes + aging data |
| `/etc/group` | Group membership |
| `/etc/gshadow` | Secure group admin/password info |

## Home directories

- Default: `/home/username`
- Auto-created by `adduser`
- Common hidden config files inside: `.bashrc`, `.profile`, `.bash_logout`

## `/etc/passwd` format

```
username:x:UID:GID:comment:home:shell
```

## `/etc/group` format

```
groupname:x:GID:user1,user2
```

## Switching users

**`su`** — switch account:
```bash
su - bob          # switch to bob, "-" loads bob's full environment
sudo su -          # become root
```

**`sudo`** — run a single command with elevated rights, using *your own* password (not root's), fully audited:
```bash
sudo apt update
sudo -i            # get a root shell
```

Grant sudo rights:
```bash
sudo usermod -aG sudo alice
```

> 💡 My takeaway: prefer `sudo` over logging in as root directly — it's safer and every action gets logged against a real user.

---
*Notes by Sakshi Chavan — for personal learning & LinkedIn sharing*
