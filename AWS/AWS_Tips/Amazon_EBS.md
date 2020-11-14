# Amazon EBS

> Amazon Elastic Block Store (EBS) 에 대해 알아보아요

<br>

<br>

## EBS volume size 조정하기

<br>

### 1. Console에서 해당 disk를 필요한 사이즈로 modify volume을 한다

### 2. 해당 Instance에 접속하여 아래의 명령어를 입력한다

```bash
[root@scouter ~]# df -alh 
Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme1n1     20G   20G  880M  96% /home/appuser/scouter
binfmt_misc        0     0     0    - /proc/sys/fs/binfmt_misc

[root@scouter ~]# xfs_growfs /dev/nvme1n1
[root@scouter ~]# df -alh
Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme1n1     30G   20G   11G  64% /home/appuser/scouter
binfmt_misc        0     0     0    - /proc/sys/fs/binfmt_misc
```

- `df -alh`
  - df
    - disk free command
  - -alh
    - `-a`
      - all
    - `-l`
      - local
    - `-h`
      - human-readable

### 3. xfs_growfs 명령을 사용하여 해당 volume에서 file system 을 확장한다

