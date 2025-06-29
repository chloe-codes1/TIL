# Ways to Check Linux OS Version in Command Line

> 궁금해서 급 찾아봄

<br>

<br>

### Linux Kernel version 확인

: Linux Kernel version은 `/proc/version`에서 관리되고 있다

```bash
$ cat /proc/version
Linux version 3.10.0-957.21.3.el7.x86_64 (mockbuild@kbuilder.bsys.centos.org) (gcc version 4.8.5 20150623 (Red Hat 4.8.5-36) (GCC) ) #1 SMP Tue Jun 18 16:35:19 UTC 2019
```

<br>

#### 현재 kernel version 확인

- 상세 정보는 `-a` option을 사용한다

```bash
$ uname -r
3.10.0-957.21.3.el7.x86_64

$ uname -a
Linux 3.10.0-957.21.3.el7.x86_64 #1 SMP Tue Jun 18 16:35:19 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux

```

<br>

<br>

### Linux Distro version 확인

: Distro version 확인 방법은 각 distro마다 다르다

<br>

#### CentOS / RedHat Enterprise

```bash
# cat /etc/redhat-release
CentOS release 6.3 (Final)
```

<br>

#### Ubuntu

```bash
$ cat /etc/lsb-release 
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=12.04
DISTRIB_CODENAME=precise
DISTRIB_DESCRIPTION="Ubuntu 12.04 LTS"
```

<br>

#### Debian

```bash
$ cat /etc/debian_version
4.0
```

<br>

#### Fedora

```bash
cat /etc/fedora-release
```
