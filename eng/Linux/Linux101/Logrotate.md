# Logrotate

> Managing Linux logs
>
> References: [man7.org](https://man7.org/linux/man-pages/man8/logrotate.8.html), [network.com](https://www.networkworld.com/article/3218728/how-log-rotation-works-with-logrotate.html), [server-talk.tistory.com](https://server-talk.tistory.com/271)
>
> <https://byd0105.tistory.com/29>
>

<br>

<br>

### What is Logrotate?

- A feature for configuring log management on Linux servers

- Usually installed by default

  - Check installation

    ```bash
    $ rpm -qa | grep logrotate
    logrotate-3.8.6-17.el7.x86_64
    ```

- `logrotate` handles splitting, compressing, and deleting log files according to the specified configuration

<br>

<br>

### How logrotate works

: logrotate operates through cron, and the related files are as follows

- `/usr/sbin/logrotate`

  - executable logrotate command

- `/etc/cron.daily/logrotate`

  - shell script that runs logrotate daily
  - logrotate operation log

- `/etc/logrotate.conf`

  - logrotate configuration file

- `/etc/logrotate.d`

  - logrotate process configuration files

  - Set to include this directory in `/etc/logrotate.conf`

    ```sh
    # RPM packages drop log rotation information into this directory
    include /etc/logrotate.d
    ```

<br>

#### Logrotate Execution Order

1. crontab
2. cron.daily
3. logrotate
4. logrotate.conf
5. logrotate.d

<br>
<br>

### logrotate.conf

Below is an example of `logrotate.conf`

```sh
# see "man logrotate" for details
# rotate log files weekly
weekly

# keep 4 weeks worth of backlogs
# When the number of log files reaches 3, delete the first created log file and create a new one
rotate 4

# create new (empty) log files after rotating old ones
# Whether to create a new log file - create: yes, empty: no
create

# use date as a suffix of the rotated file
# Option to add date to log files
dateext

# uncomment this if you want your log files compressed
#compress
# RPM packages drop log rotation information into this directory
# Log process configuration path
include /etc/logrotate.d

# no packages own wtmp and btmp -- we'll rotate them here
/var/log/wtmp {
    monthly
    create 0664 root utmp
        minsize 1M
    rotate 1
}
/var/log/btmp {
    missingok
    monthly
    create 0600 root utmp
    rotate 1
}


# system-specific logs may be also be configured here.
```

<br>

<br>

### Options

- rotate [number] : Delete when there are more than 5 log files
  - ex) rotate 5
- maxage [number] : Delete log files older than 30 days
  - ex) maxage 30
- size : Execute rotation when the file is larger than the specified size
  - ex) size +100k
- create [permissions] [user] [group] : Set permissions for rotated log files
  - ex) create 644 root root
- notifempty : Do not rotate if the log is empty
- ifempty : Rotate even if the log is empty
- monthly (monthly), weekly (weekly), daily (daily) rotation
- compress : gzip compress rotated log files
- nocompress : Do not gzip compress rotated log files
- missingok : Do not raise an error if the log file is not found
- dateext : Add date to the backup file name
