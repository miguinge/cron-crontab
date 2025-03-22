# cron DAEMON
`cron` is a  daemon to execute scheduled commands at fixed times, dates, or intervals.

## Checking whether `cron` is running

Since `cron` is started automatically from /etc/init.d it must be running so you can check as following

```bash 
$ systemctl status cron
```

The output must show:

> $ systemctl status cron\
> $${\color{lightgreen}●}$$ cron.service - Regular background program processing daemon\
>    Loaded: loaded (/usr/lib/systemd/system/cron.service; $${\color{green}enabled}$$; preset: $${\color{green}enabled}$$)\
>    Active: $${\color{green}active (running)}$$ since Fri 2025-03-21 23:12:25 CST; 48min ago

- The following directories must exist in **`/etc`** directory:

```
/etc/cron.hourly
/etc/cron.daily
/etc/cron.weekly
/etc/cron.monthly
```
The directories above are set up for the commands within them to be executed as their name states (hourly, daily, weekly, monthly)

The file `/etc/crontab` contains system-wide information about jobs to be run.

```
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the `crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.

SHELL=/bin/sh
# You can also override PATH, but by default, newer versions inherit it from the environment
#PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name command to be executed
17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || { cd / && run-parts --report /etc/cron.daily; }
47 6    * * 7   root    test -x /usr/sbin/anacron || { cd / && run-parts --report /etc/cron.weekly; }
52 6    1 * *   root    test -x /usr/sbin/anacron || { cd / && run-parts --report /etc/cron.monthly; }
```

# Scheduling user-level cron jobs using ***`crontab`***

There are two main modes:
- crontab -e
- sudo crontab -e

The former edits or creates the current user's crontab.\
The latter edits or creates the root's crontab.

Both modes create a file in which the time must be specified at the last line.

    # m h dom mon dow coomand

Where:
- m --> minute
- h --> hour
- dom --> day of month
- mon --> month
- dow --> day of week
- command --> commands or scripts to be run at specified time.

The star key `*` character stands for "any time"

For more information visit the great web page [crontab guru][guru]

[guru]: https://crontab.guru
