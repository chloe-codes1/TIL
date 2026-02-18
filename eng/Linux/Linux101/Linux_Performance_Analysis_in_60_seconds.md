# Linux Performance Analysis in 60 seconds

> Assessing server status within 60 seconds using the CLI in a standard Linux environment
>
> Reference: [netflixtechblog.com](https://netflixtechblog.com/linux-performance-analysis-in-60-000-milliseconds-accc10403c55)

<br>

<br>

### Quick overview

```bash
$ uptime
$ dmesg | tail
$ vmstat 1
$ mpstat -P ALL 1
$ pidstat 1
$ iostat -xz 1
$ free -m
$ sar -n DEV 1
$ sar -n TCP,ETCP 1
$ top
```

<br>

<br>

## First 60 Seconds: Summary

<br>

### 1. uptime

```bash
$ uptime
23:51:26 up 21:31, 1 user, load average: 30.02, 26.43, 19.02
```

- uptime is the easiest way to check the **load average** value, which indicates how many processes are currently waiting
  - On Linux systems, this value includes not only waiting processes but also processes blocked by I/O operations such as **disk I/O**
    - This lets you see how many resources are being used, but it cannot be analyzed precisely
- The 3 numbers above (1.88 2.16 2.07) represent load averages over **1 minute**, **5 minutes**, and **15 minutes**, respectively
  - This allows you to see changes over time
    - ex)
      - When you log into the instance after hearing about a failure, if the 1-minute value is smaller than the 15-minute value,
        - it means the failure occurred and you logged in too late.
      - In the example above, the 1-minute value is about 30 and the 15-minute value is about 19, indicating a recent increase
        - A high number here carries many implications.
          - It is likely a CPU demand issue, but to confirm this, you can use commands like `vmstat` or `mpstat` described below.

<br>

### 2. dmesg | tail

```bash
$ dmesg | tail
[1880957.563150] perl invoked oom-killer: gfp_mask=0x280da, order=0, oom_score_adj=0
[...]
[1880957.563400] Out of memory: Kill process 18694 (perl) score 246 or sacrifice child
[1880957.563408] Killed process 18694 (perl) total-vm:1972392kB, anon-rss:1953348kB, file-rss:0kB
[2320864.954447] TCP: Possible SYN flooding on port 7001. Dropping request.  Check SNMP counters.
```

- **dmesg** is a command for checking system messages
  - Since all kernel messages are output starting from boot, **tail** is used to display only the last 10 lines
- Through these messages, you can find errors that may cause performance issues.
  - In the example above, you can see that `oom-killer (out of memory)` occurred and `TCP requests` were dropped.

<br>

### 3. vmstat 1

```bash
$ vmstat 1
procs ---------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
34  0    0 200889792  73708 591828    0    0     0     5    6   10 96  1  3  0  0
32  0    0 200889920  73708 591860    0    0     0   592 13284 4282 98  1  1  0  0
32  0    0 200890112  73708 591860    0    0     0     0 9501 2154 99  1  0  0  0
32  0    0 200889568  73712 591856    0    0     0    48 11900 2459 99  0  0  0  0
32  0    0 200890208  73712 591860    0    0     0     0 15898 4840 98  1  1  0  0
```

- **vmstat**, short for **virtual memory stat**, is a tool available in most environments
  - vmstat with argument 1 displays information every second
  - The first line shows average values since boot
    - **Items to check**
      - **r**
        - The number of processes running on the CPU
        - A good value for checking if CPU resource saturation is occurring
        - If the `r` value is greater than the number of CPUs, it is considered saturated.
      - **free**
        - Shows free memory in KB
        - If the free memory has too many digits, you can use `free -m` for easier reading
      - **si, so**
        - Values for swap-in and swap-out
        - If these are not 0, the system currently has **insufficient memory**
      - **us, sy, id, wa, st**
        - You can measure the average CPU time across all CPUs
        - These represent user time, system time used by the kernel, idle, wait I/O, and stolen time respectively
          - Stolen time refers to the time the real CPU was occupied while the hypervisor was servicing virtual CPUs

<br>

### 4. mpstat -P ALL 1

```bash
$ mpstat -P ALL 1
Linux 3.13.0-49-generic (titanclusters-xxxxx)  07/14/2015  _x86_64_ (32 CPU)

07:38:49 PM  CPU   %usr  %nice   %sys %iowait   %irq  %soft  %steal  %guest  %gnice  %idle
07:38:50 PM  all  98.47   0.00   0.75    0.00   0.00   0.00    0.00    0.00    0.00   0.78
07:38:50 PM    0  96.04   0.00   2.97    0.00   0.00   0.00    0.00    0.00    0.00   0.99
07:38:50 PM    1  97.00   0.00   1.00    0.00   0.00   0.00    0.00    0.00    0.00   2.00
07:38:50 PM    2  98.00   0.00   1.00    0.00   0.00   0.00    0.00    0.00    0.00   1.00
07:38:50 PM    3  96.97   0.00   0.00    0.00   0.00   0.00    0.00    0.00    0.00   3.03
[...]
```

- This command measures CPU time per individual CPU
  - This method allows you to check for **imbalanced states** across CPUs,
    - where only one CPU is working, meaning the application is running as a **single thread**

<br>

### 5. pidstat 1

```bash
$ pidstat 1
Linux 3.13.0-49-generic (titanclusters-xxxxx)  07/14/2015    _x86_64_    (32 CPU)

07:41:02 PM   UID       PID    %usr %system  %guest    %CPU   CPU  Command
07:41:03 PM     0         9    0.00    0.94    0.00    0.94     1  rcuos/0
07:41:03 PM     0      4214    5.66    5.66    0.00   11.32    15  mesos-slave
07:41:03 PM     0      4354    0.94    0.94    0.00    1.89     8  java
07:41:03 PM     0      6521 1596.23    1.89    0.00 1598.11    27  java
07:41:03 PM     0      6564 1571.70    7.55    0.00 1579.25    28  java
07:41:03 PM 60004     60154    0.94    4.72    0.00    5.66     9  pidstat

07:41:03 PM   UID       PID    %usr %system  %guest    %CPU   CPU  Command
07:41:04 PM     0      4214    6.00    2.00    0.00    8.00    15  mesos-slave
07:41:04 PM     0      6521 1590.00    1.00    0.00 1591.00    27  java
07:41:04 PM     0      6564 1573.00   10.00    0.00 1583.00    28  java
07:41:04 PM   108      6718    1.00    0.00    0.00    1.00     0  snmp-pass
07:41:04 PM 60004     60154    1.00    4.00    0.00    5.00     9  pidstat
```

- **pidstat** is similar to running the `top` command per process
  - However, the difference is that instead of displaying on the full screen, it continuously shows changing conditions, making it great for **recording changes**
    - Looking at the example above, the CPU usage of two Java processes is enormous
      - The `%CPU` item represents the total usage across all CPUs
        - Therefore, the Java processes using 1591% indicate that they are using close to 16 CPUs.

<br>

### 6. iostat -xz 1

```bash
$ iostat -xz 1
Linux 3.13.0-49-generic (titanclusters-xxxxx)  07/14/2015  _x86_64_ (32 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
          73.96    0.00    3.73    0.03    0.06   22.21

Device:   rrqm/s   wrqm/s     r/s     w/s    rkB/s    wkB/s avgrq-sz avgqu-sz   await r_await w_await  svctm  %util
xvda        0.00     0.23    0.21    0.18     4.52     2.08    34.37     0.00    9.98   13.80    5.42   2.44   0.09
xvdb        0.01     0.00    1.02    8.94   127.97   598.53   145.79     0.00    0.43    1.78    0.28   0.25   0.25
xvdc        0.01     0.00    1.02    8.86   127.79   595.94   146.50     0.00    0.45    1.82    0.30   0.27   0.26
dm-0        0.00     0.00    0.69    2.32    10.47    31.69    28.01     0.01    3.23    0.71    3.98   0.13   0.04
dm-1        0.00     0.00    0.00    0.94     0.01     3.78     8.00     0.33  345.84    0.04  346.81   0.01   0.00
dm-2        0.00     0.00    0.09    0.07     1.35     0.36    22.50     0.00    2.55    0.23    5.62   1.78   0.03
[...]
```

- A great tool for understanding how `block devices (HDD, SSD, ...)` are performing
  - **Items to check**
    - **r/s, w/s rkB/s, wkB/s**
      - Shows read requests, write requests, read kB/s, and write kB/s
      - An important metric for checking which type of requests are most frequent
        - Performance issues can sometimes be caused by excessive requests.
    - **await**
      - The average I/O processing time expressed in milliseconds
      - For applications, this is the time to queue an I/O request and receive service, so the application waits during this time
      - If it is longer than the normal request processing time of the device, it indicates that there is a problem with the block device itself, or that the device is saturated

<br>

### 7. free -m

```bash
$ free -m
             total       used       free     shared    buffers     cached
Mem:        245998      24545     221453         83         59        541
-/+ buffers/cache:      23944     222053
Swap:            0          0          0
```

- **Items to check**
  - buffers: Buffer cache for block device I/O, usage amount
  - cached: Amount of [page cache](https://brunch.co.kr/@alden/25) used by the file system
    - These values should not approach 0
      - This indicates high Disk I/O is occurring (can be confirmed with `iostat`)
        - In the example above, the values are 59MB and 541MB respectively, which are acceptable

<br>

### 8. sar -n DEV 1

``` bash
$ sar -n DEV 1
Linux 3.13.0-49-generic (titanclusters-xxxxx)  07/14/2015     _x86_64_    (32 CPU)

12:16:48 AM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s   %ifutil
12:16:49 AM      eth0  18763.00   5032.00  20686.42    478.30      0.00      0.00      0.00      0.00
12:16:49 AM        lo     14.00     14.00      1.36      1.36      0.00      0.00      0.00      0.00
12:16:49 AM   docker0      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00

12:16:49 AM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s   %ifutil
12:16:50 AM      eth0  19763.00   5101.00  21999.10    482.56      0.00      0.00      0.00      0.00
12:16:50 AM        lo     20.00     20.00      3.25      3.25      0.00      0.00      0.00      0.00
12:16:50 AM   docker0      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
```

- This tool allows you to measure **network throughput (Rx, Tx KB/s)**
  - In the example above, the receive volume of `eth0` is approximately 22 Mbytes/s (21999.10 rxkB/s)
    - This is 176 Mbits/s, which is still far below the 1 Gbit/s limit
  - The `%ifutil` value is the network device utilization, which can also be measured with [nicstat](https://github.com/scotte/nicstat)
    - However, as with nicstat, it is difficult to get accurate values, and it does not work well in the example above either

<br>

### 9. sar -n TCP,ETCP 1

```bash
$ sar -n TCP,ETCP 1
Linux 3.13.0-49-generic (titanclusters-xxxxx)  07/14/2015    _x86_64_    (32 CPU)

12:17:19 AM  active/s passive/s    iseg/s    oseg/s
12:17:20 AM      1.00      0.00  10233.00  18846.00

12:17:19 AM  atmptf/s  estres/s retrans/s isegerr/s   orsts/s
12:17:20 AM      0.00      0.00      0.00      0.00      0.00

12:17:20 AM  active/s passive/s    iseg/s    oseg/s
12:17:21 AM      1.00      0.00   8359.00   6039.00

12:17:20 AM  atmptf/s  estres/s retrans/s isegerr/s   orsts/s
12:17:21 AM      0.00      0.00      0.00      0.00      0.00
```

- Shows a summary of TCP traffic.
  - active/s: Shows the number of TCP connections per second initiated locally (e.g., connections via connect()).
  - passive/s: Shows the number of TCP connections per second requested from remote (e.g., connections via accept()).
  - retrans/s: Shows the number of TCP retransmissions per second.
- Viewing the `active` and `passive` counts is convenient for roughly measuring server load
  - Based on the description above, you might think active is outbound and passive is inbound connections, but that is not always the case.
    - ex) Connections like localhost to localhost
- `retransmits` indicate that there are **network** or **server** **issues**
  - This refers to an **unreliable network environment** (public internet) or **connections exceeding the server's capacity** causing packet drops
    - In the example above, you can see one TCP connection coming in per second.

<br>

### 10. top

```bash
$ top
top - 00:15:40 up 21:56,  1 user,  load average: 31.09, 29.87, 29.92
Tasks: 871 total,   1 running, 868 sleeping,   0 stopped,   2 zombie
%Cpu(s): 96.8 us,  0.4 sy,  0.0 ni,  2.7 id,  0.1 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem:  25190241+total, 24921688 used, 22698073+free,    60448 buffers
KiB Swap:        0 total,        0 used,        0 free.   554208 cached Mem

   PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
 20248 root      20   0  0.227t 0.012t  18748 S  3090  5.2  29812:58 java
  4213 root      20   0 2722544  64640  44232 S  23.5  0.0 233:35.37 mesos-slave
 66128 titancl+  20   0   24344   2332   1172 R   1.0  0.0   0:00.07 top
  5235 root      20   0 38.227g 547004  49996 S   0.7  0.2   2:02.74 java
  4299 root      20   0 20.015g 2.682g  16836 S   0.3  1.1  33:14.42 java
     1 root      20   0   33620   2920   1496 S   0.0  0.0   0:03.82 init
     2 root      20   0       0      0      0 S   0.0  0.0   0:00.02 kthreadd
     3 root      20   0       0      0      0 S   0.0  0.0   0:05.35 ksoftirqd/0
     5 root       0 -20       0      0      0 S   0.0  0.0   0:00.00 kworker/0:0H
     6 root      20   0       0      0      0 S   0.0  0.0   0:06.94 kworker/u256:0
     8 root      20   0       0      0      0 S   0.0  0.0   2:38.05 rcu_sched
```

- The `top` command makes it easy to check the various metrics reviewed above.
  - It has the advantage of being easy to check overall system values
    - However, since the screen changes continuously, it is difficult to find patterns
      - To catch intermittent pauses, you need to quickly freeze the screen periodically
        - ex) Ctrl+S pauses updates, and Ctrl+Q resumes them. Then the screen gets cleared
