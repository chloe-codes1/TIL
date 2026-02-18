# Use SCP Command to Securely Transfer Files

<br>

## SCP (Secure Copy)

<br>

### SCP Command

- A command for transferring files between network-connected hosts using **SSH**
  - Since it uses SSH, files can be sent and received using **Identity Files** such as **SSH key files**
- `Local` to `Remote` (send)
- `Remote` to `Local` (retrieve)
- `Remote` to `Remote`  (transfer between hosts) are all possible

<br>

### Syntax

```bash
scp [options ...] [source] [target]
```

<br>

### Options

- `-r`
  - Recursively copy all folders
  - Option used when copying folders
    - Specify the folder as the target to transfer
      - If there are symbolic links, instead of creating a symbolic link at the target, it copies the file or folder that the symbolic link points to
- `-P`
  - Option to specify the SSH port
- `-i`
  - Option to specify the path to an identity file such as an SSH key file
- `-v`
  - Verbose mode, used for debugging with detailed output
- `-p`
  - Preserve file modification time and permissions

<br>

<br>

`+`

### Transferring Files to AWS EC2 via SCP

ex)

```bash
scp -i [pem key path] [file path to upload] [ec2 address]:~
```
