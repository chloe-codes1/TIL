# Ways to Check Linux OS Version in Command Line

> Looked it up out of curiosity

<br>

<br>

### Checking Linux Kernel version

: The Linux Kernel version is managed in `/proc/version`

```bash
$ cat /proc/version
Linux version 3.10.0-957.21.3.el7.x86_64 (mockbuild@kbuilder.bsys.centos.org) (gcc version 4.8.5 20150623 (Red Hat 4.8.5-36) (GCC) ) #1 SMP Tue Jun 18 16:35:19 UTC 2019
```

<br>

#### Checking the current kernel version

- Use the `-a` option for detailed information

```bash
$ uname -r
3.10.0-957.21.3.el7.x86_64

$ uname -a
Linux 3.10.0-957.21.3.el7.x86_64 #1 SMP Tue Jun 18 16:35:19 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux

```

<br>

<br>

### Checking Linux Distro version

: The method for checking the distro version differs for each distro

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
