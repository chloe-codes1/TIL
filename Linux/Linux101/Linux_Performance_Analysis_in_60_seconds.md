# Linux Performance Analysis in 60 seconds

> 표준적인 Linux 환경에서 CLI를 이용해 서버 상황을 60초안에 파악하기
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

- uptime은 현재 대기중인 process가 얼마나 있는지 나타내는 **load average** 값을 확인하는 가장 쉬운 방법이다
  - Linux system에서 이 값은 대기중인 process 뿐만 아니라 **disk I/O** 같은 I/O 작업으로 block된 process까지 포함되어 있다
    - 이를 통해서 얼마나 많은 resource가 사용되는지 확인할 수 있지만, 정확하게 분석할 수는 없다
- 위에 있는 3개 숫자 (1.88 2.16 2.07)는 각각 **1분**, **5분**, **15분**에 load average한 값이다
  - 이를 통해서 시간의 변화를 알 수 있다
    - ex)
      - 장애가 발생했다는 소식을 듣고 해당 instance에 로그인 했을때 1분 동안의 값이 15분 값에 비해서 작다면, 
        - 이것은 장애가 발생하고, 너무 늦게 로그인했음을 알 수 있다. 
      - 위 예제에서는 1분 값이 약 30이고 15분 값이 19 정도 되는것으로 볼때 최근에 상승한것을 알 수 있다
        - 여기서 숫자가 높은 것은 많은 의미를 갖고 있다. 
          - 아마도 CPU 수요에 문제가 있을거라 추측되지만 이 의미를 확인하기 위해선 뒤에 나오는 `vmstat`이나 `mpstat`같은 command를 이용해서 확인할 수 있다.

<br>

### 2. dmes | tail

```bash
$ dmesg | tail
[1880957.563150] perl invoked oom-killer: gfp_mask=0x280da, order=0, oom_score_adj=0
[...]
[1880957.563400] Out of memory: Kill process 18694 (perl) score 246 or sacrifice child
[1880957.563408] Killed process 18694 (perl) total-vm:1972392kB, anon-rss:1953348kB, file-rss:0kB
[2320864.954447] TCP: Possible SYN flooding on port 7001. Dropping request.  Check SNMP counters.
```

- **dmesg**는 system message를 확인할 수 있는 command이다
  - 부팅시부터 시작해서 모든 Kernel message가 출력되기 때문에 **tail** 을 이용해서 마지막 10줄만 출력한 것이다
- 이 메세지를 통해서 성능에 문제를 줄 수 있는 에러를 찾을 수 있는데, 
  - 위의 예제에서는 `oom-killer(out of memory)`와 `TCP request`가 drop된것을 알 수 있다.

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

- **virtual memory stat**의 약자인 **vmstat**은 왠만한 환경에서 사용 가능한 툴이다
  - 1을 인자로 준 vmstat은 1초마다 정보를 보여준다
  - 첫번째 라인은 부팅된 뒤에 평균적인 값을 나타낸다
    - **확인해봐야할 항목**
      - **r**
        - CPU에서 동작중인 프로세스의 숫자이다
        - CPU 자원이 포화(saturation)가 발생하는지 확인할때에 좋은 값이다 
        - `r` 값이 CPU의 값보다 큰 경우에 포화되어 있다고 해석된다.
      - **free**
        - free memory를 kb단위로 나타낸다
        - free memory가 너무 자리수가 많은 경우 `free -m`를 이용하면 편하게 확인할 수 있다
      - **si, so**
        - swap-in과 swap-out에 대한 값이다 
        - 0이 아니라면 현재 시스템에 **메모리가 부족**한것이다
      - **us, sy, id, wa, st**
        - 모든 CPU의 평균적인 CPU time을 측정할 수 있다
        - 각각 user time, 커널에서 사용되는 system time, idle, wait I/O 그리고 stolen time순이다
          - stolen time은 hypervisor가 가상 CPU를 서비스 하는 동안 실제 CPU를 차지한 시간을 이야기한다

<br>

### 4. mpstat -p ALL 1

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

- 이 명령어는 CPU time을 CPU 별로 측정할 수 있다
  - 이 방법을 통하면 각 CPU별로 **불균형한 상태**를 확인할 수 있는데, 
    - 한 CPU만 일하고 있는것은 application이 **single thread**로 동작하고 있다는 뜻이다

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

- **pidstat**은 process당 `top`명령을 수행하는것과 비슷하다
  - but, 차이점은 스크린 전체에 표시하는것이 아니라 지속적으로 변화하는 상황을 띄워주기 떄문에 **상황 변화**를 기록하기 좋다
    - 위 예제를 보면 두개의 java process의 CPU 사용량이 엄청나다
      - `%CPU` 항목은 모든 CPU의 전체 사용량을 의미한다
        - 따라서 1591%를 사용중인 java process들은 16CPU 가까이 사용중임을 나타내는 것이다.

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

- `block device(HDD, SSD, …)`가 어떻게 동작하는지 이해하기 좋은 툴이다
  - **확인해봐야할 항목**
    - **r/s, w/s rkB/s, wkB/s**
      - read 요청과 write 요청, read kB/s, write kB/s를 나타낸다
      - 어떤 요청이 가장 많이 들어오는지 확인해볼 수 있는 중요한 지표다
        - 성능 문제는 생각보다 과도한 요청때문에 발생하는 경우도 있기 때문이다.
    - **await**
      - I/O처리 평균 시간을 밀리초로 표현한 값이다
      - application한테는 I/O요청을 queue하고 서비스를 받는데 걸리는 시간이기 때문에 application이 이 시간동안 대기하게 된다
      - 일반적인 장치의 요청 처리 시간보다 긴 경우에는 block장치 자체의 문제가 있거나, 장치가 포화된 상태임을 알 수 있다

<br>

### 7. free -m

```bash
$ free -m
             total       used       free     shared    buffers     cached
Mem:        245998      24545     221453         83         59        541
-/+ buffers/cache:      23944     222053
Swap:            0          0          0
```

- **확인해봐야할 항목**
  - buffers: Block 장치 I/O의 buffer 캐시, 사용량
  - cached: 파일 시스템에서 사용되는 [page cache](https://brunch.co.kr/@alden/25)의 양
    - 위 값들이 0에 가까워 지면 안된다
      - 이는 곧 높은 Disk I/O가 발생하고 있음을 의미한다 (`iostat`으로 확인 가능)
        - 위 예제는 각각 59MB, 541MB로 괜찮은 정도에 속한다

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

- 이 툴을 사용하면 **network throughput(Rx, Tx KB/s)**을 측정할수 있다
  - 위 예제에서는 `eth0`의 수신량이 약 22Mbytes/s(21999.10rxkB/s)이다
    - 이것은 176Mbits/s인데 한계인 1Gbit/s에 아직 많이 못 미치는 값이다
  - 위 값중 `%ifutil`은 [nicstat](https://github.com/scotte/nicstat)로도 측정 가능한 네트워크 장치 사용률이다
    - but, nicstat에서도 그렇듯 정확한 값을 가져오는게 어려워서 위 예제에서도 잘 작동하지 않는다

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

- TCP 통신량을 요약해서 보여준다.
  - active/s: 로컬에서부터 요청한 초당 TCP 커넥션 수를 보여준다 (예를들어, connect()를 통한 연결).
  - passive/s: 원격으로부터 요청된 초당 TCP 커넥션 수를 보여준다 (예를들어, accept()를 통한 연결).
  - retrans/s: 초당 TCP 재연결 수를 보여준다.
- `active`와 `passive` 수를 보는것은 서버의 부하를 대략적으로 측정하는데에 편리하다
  - 위 설명을 보면 active를 outbound passive를 inbound 연결로 판단할 수 있는데, 꼭 그렇지만은 않다. 
    - ex) localhost에서 localhost로 연결같은 connection
- `retransmits`은 **네트워크**나 **서버**의 **issue**가 있음을 이야기한다
  - **신뢰성이 떨어지는 네트워크 환경**이나(공용인터넷), **서버가 처리할 수 있는 용량 이상의 커넥션**이 붙어서 패킷이 drop되는것을 이야기한다
    - 위 예제에서는 초당 하나의 TCP 서버가 들어오는것을 알 수 있다.

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

- `top` 명령어는 위에서 체크해본 다양한 측정치를 쉽게 체크할 수 있다.
  - 시스템 전반적으로 값을 확인하기 쉽다는 장점이 있다
    - but, 화면이 지속적으로 바뀌는 점 떄문에 패턴을 찾는것이 어렵다
      - 일시적으로 멈추는 현상을 잡기 위해서도 화면을 주기적으로 빠르게 멈춰주지 않으면 찾기 힘들다
        - ex) ctrl+S는 업데이트를 중지시키고, Ctrl+Q는 다시 시작시킨다. 그리고 화면이 지워져버린다