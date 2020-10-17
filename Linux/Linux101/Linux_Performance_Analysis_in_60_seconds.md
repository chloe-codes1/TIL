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

*계속 정리중...*