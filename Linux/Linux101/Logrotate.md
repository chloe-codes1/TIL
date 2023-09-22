# Logrotate

> Linux log를 관리해요
>
> References: [man7.org](https://man7.org/linux/man-pages/man8/logrotate.8.html), [network.com](https://www.networkworld.com/article/3218728/how-log-rotation-works-with-logrotate.html), [server-talk.tistory.com](https://server-talk.tistory.com/271)
>
> <https://byd0105.tistory.com/29>
>

<br>

<br>

### What is Logrotate?

- Linux server의 log를 관리하도록 설정하는 기능

- 보통 기본적으로 설치되어 있다

  - 설치 확인

    ```bash
    $ rpm -qa | grep logrotate
    logrotate-3.8.6-17.el7.x86_64
    ```

- `logrotate` 는 log 파일들을 지정한 설정에 맞게 자르고, 압축하고, 삭제하는 것을 대신해준다

<br>

<br>

### How logrotate works

: logrotate는 cron을 통해 동작하는데, 관련된 file들은 아래와 같다

- `/usr/sbin/logrotate`

  - executable logrotate command

- `/etc/cron.daily/logrotate`

  - logrotate를 매일 실행하는 shell script
  - logrotate 작업 내역 log

- `/etc/logrotate.conf`

  - logrotate 설정 파일

- `/etc/logrotate.d`

  - logrotate process 설정 파일

  - `/etc/logroate.conf` 에 해당 directory를 포함시키도록 설정함

    ```sh
    # RPM packages drop log rotation information into this directory
    include /etc/logrotate.d
    ```

<br>

#### Logrotate 실행 순서

1. crontab
2. cron.daily
3. logrotate
4. logrotate.conf
5. logrotate.d

<br>
<br>

### logrotate.conf

아래는 `logrotate.conf` 의 예시이다

```sh
# see "man logrotate" for details
# rotate log files weekly
weekly

# keep 4 weeks worth of backlogs
# Log file의 개수가 3개가 되면 첫번째 생성된 Log파일 삭제 후 생성
rotate 4

# create new (empty) log files after rotating old ones
# 새로운 Log file의 생성 여부 - create: 생성o, empty: 생성x
create

# use date as a suffix of the rotated file
# 로그 파일에 날짜를 부여하는 option
dateext

# uncomment this if you want your log files compressed
#compress
# RPM packages drop log rotation information into this directory
# Log process Rㅕㅇ로
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

- rotate [숫자] : log파일이 5개 이상 되면 삭제
  - ex) rotate 5
- maxage [숫자] : log파일이 30일 이상 되면 삭제
  - ex) maxage 30
- size : 지정된 용량보다 클 경우 rotate 실행
  - ex)　size +100k
- create [권한] [유저] [그룹] : rotate 되는 로그파일 권한 지정
  - ex) create 644 root root
- notifempty : 로그 내용이 없으면 rotate 하지 않음  
- ifempty : 로그 내용이 없어도 rotate 진행
- monthly(월 단위) , weekly(주 단위) , daily(일 단위) rotate 진행
- compress : rotate 되는 log file gzip 압축
- nocompress : rotate 되는 로그파일 gzip 압축 X
- missingok : 로그 파일이 발견되지 않은 경우 에러처리 하지 않음
- dateext : 백업 파일의 이름에 날짜가 들어가도록 함  
