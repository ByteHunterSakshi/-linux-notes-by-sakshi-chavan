# Cron & Job Scheduling
**Notes by Sakshi Chavan**

---

## What is CronTab?

A time-based job scheduler built into Unix-like systems. Runs recurring tasks automatically — no manual trigger needed. Can be system-wide or per-user.

## The 5-field syntax

```
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of week (0-6, Sunday=0)
│ │ │ └──── Month (1-12)
│ │ └────── Day of month (1-31)
│ └──────── Hour (0-23)
└────────── Minute (0-59)
```

## Special characters

| Symbol | Meaning |
|---|---|
| `*` | every value |
| `,` | list of values |
| `-` | range of values |
| `/` | step values |

## Managing the cron service

**Modern way — `systemctl`:**
```bash
systemctl status cron.service
systemctl start cron.service
systemctl stop cron.service
systemctl restart cron.service
systemctl enable cron.service     # start on boot
systemctl disable cron.service
journalctl -u cron.service         # view logs
```

**Older way — `service`:**
```bash
apt update && apt install cron
service cron status
service cron start
service cron stop
service cron restart
```

`systemctl` is the newer systemd-based approach with richer status info, dependency management, and boot control. `service` is more portable to older/traditional init systems but simpler and more limited.

## Editing crontabs

```bash
crontab -e             # edit your crontab
crontab -l              # list your entries
crontab -r               # wipe all your entries
sudo vim /etc/crontab      # edit the system-wide crontab
```

## Basic scheduling examples

```bash
* * * * * command          # every minute
0 * * * * command            # every hour, on the hour
0 0 * * * command              # every day at midnight
0 0 * * 0 command                # every Sunday at midnight
0 0 1 * * command                  # 1st of every month
```

## Using `*` (every value)

```bash
* * * * * touch /tmp/minute_file.txt          # every minute
0 * * * * mkdir -p /tmp/hourly_dir              # every hour
0 0 * * * tar -czf /backup/daily.tar.gz /data     # every day
0 0 1 * * touch /tmp/monthly_file.txt               # every month
```

## Using `,` (value list)

```bash
0 2,14 * * * touch /tmp/twice_daily.txt         # 2 AM and 2 PM
0 0 * * 1,5 mkdir -p /tmp/weekly_backup           # Mon and Fri
0 0 1,15 * * tar -czf /backup/biweekly.tar.gz /data  # 1st & 15th
0 9,12,15 * * * touch /tmp/three_times.txt             # 9AM, noon, 3PM
0 0 * * 6,0 mkdir -p /tmp/weekend_backup                 # Sat & Sun
```

## Using `-` (range)

```bash
0 9-17 * * * touch /tmp/business_hours.txt        # every hour, 9AM-5PM
0 0 * * 1-5 mkdir -p /tmp/workday_backup             # Mon-Fri
0 0-6 * * * mkdir -p /tmp/nightly_backup               # midnight-6AM
```

## Using `/` (step values)

```bash
*/5 * * * * touch /tmp/five_min.txt              # every 5 min
0 */2 * * * mkdir -p /tmp/two_hour_backup          # every 2 hrs
0 0 */3 * * tar -czf /backup/three_day.tar.gz /data  # every 3 days
*/30 * * * * touch /tmp/half_hour.txt                  # every 30 min
0 */4 * * * mkdir -p /tmp/four_hour_backup               # every 4 hrs
```

## Nth-weekday-of-month trick

Cron doesn't have a native "2nd Saturday" concept — you fake it with day-of-month ranges:

```bash
# 1st Saturday
0 10 1-7 * 6 root /opt/myscript.sh

# 2nd Saturday
0 10 8-14 * 6 root /opt/myscript.sh

# 3rd Saturday
0 10 15-21 * 6 root /opt/myscript.sh

# 4th Saturday
0 10 22-28 * 6 root /opt/myscript.sh

# 5th Saturday (only exists some months)
0 10 29-31 * 6 root /opt/myscript.sh
```

**Why this works:** the Nth Saturday of any month always falls within a fixed 7-day window (1–7, 8–14, 15–21, 22–28), so combining the day-of-month range with the weekday field pins it down reliably — even the 22–28 range works in every month regardless of length.

---
*Notes by Sakshi Chavan — for personal learning & LinkedIn sharing*
