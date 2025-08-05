# Resizing an Amazon EBS Volume

> Adjusting Amazon EBS volume size

<br>

<br>

### 1. EBS Volume Size Adjustment

: In the AWS Console, modify the volume of the corresponding disk to the required size

<br>

<br>

### 2. Linux File System Expansion

- After increasing the EBS volume size, you need to expand the size of the Linux file system
- You can start adjusting the file system size when the volume status becomes `optimizing` in the AWS console

<br>

#### 2-1. Connect to the Instance and Check the File System

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

#### 2-2. Use the xfs_growfs Command to Expand the File System on the Volume

```bash
[root@scouter ~]# xfs_growfs /dev/nvme1n1
```

- This is the command to expand the volume of the `/dev/nvme1n1` partition

<br>

#### 2-3. Check the File System Size Again

```bash
[root@scouter ~]# df -alh
Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme1n1     30G   20G   11G  64% /home/appuser/scouter
binfmt_misc        0     0     0    - /proc/sys/fs/binfmt_misc
```

- You can confirm that the expanded volume size is reflected in the file system at 30G

<br>

*Done!* 
