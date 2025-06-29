# Resizing an Amazon EBS Volume

> Amazon EBS volume size 조정하기

<br>

<br>

### 1. EBS Volume 크기 조정

: AWS Console에서 해당 disk를 필요한 사이즈로 modify volume을 한다

<br>

<br>

### 2. Linux file system 확장

- EBS volume 크기를 늘리고 난 후에는 linux file system의 크기를 늘려줘야한다
- AWS console에서 volume status가 `optimizing` 상태가 되면 file system 크기 조정을 시작 할 수 있다

<br>

#### 2-1. 해당 Instance에 접속하여 file system을 확인한다

```bash
[root@scouter ~]# df -alh 
Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme1n1     20G   20G  880M  96% /home/appuser/scouter
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

<br>

#### 2-2. xfs_growfs 명령을 사용하여 해당 volume에서 file system 을 확장한다

```bash
[root@scouter ~]# xfs_growfs /dev/nvme1n1
```

- `/dev/nvme1n1` 파티션의 volume을 늘려주는 명령어다

<br>

#### 2-3. 다시 file system 크기를 확인한다

```bash
[root@scouter ~]# df -alh
Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme1n1     30G   20G   11G  64% /home/appuser/scouter
binfmt_misc        0     0     0    - /proc/sys/fs/binfmt_misc
```

- 30G 로 file system에 늘어난 볼륨 크기가 반영된 것을 확인할 수 있다

<br>

*끝~!*
