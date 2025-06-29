# Use SCP Command to Securely Transfer Files

<br>

## SCP (Secure Copy)

<br>

### SCP Command

- **SSH** 를 이용해  network로 연결된 host간에 파일을 주고 받는 명령어
  - SSH를 사용하기 때문에 **SSH key file**과 같은 **Identity File**을 이용해 파일을 송수신 할 수 있다
- `Local` to `Remote` (보내기)
- `Remote` to `Local` (가져오기)
- `Remote` to `Remote`  (Host 끼리 전송) 모두 가능하다

<br>

### Syntax

```bash
scp [options ...] [source] [target]
```

<br>

### Options

- `-r`
  - 재귀적으로 모든 폴더들을 복사
  - 폴더를 복사할 때 사용하는 옵션
    - 전송하고자 하는 대상은 폴더로 지정하면 된다
      - symbolic link가 있는 경우에는 target에 symbolic link를 생성하지 않고 symbolic link가 가리키는 파일 혹은 폴더를 복사한다
- `-P`
  - ssh 포트를 지정하는 옵션
- `-i`
  - ssh 키파일과 같은 identity file의 경로를 지정하는 옵션
- `-v`
  - verbose 모드로 상세내용을 보며 디버깅을 할 때 사용한다
- `-p`
  - 파일의 수정 시간과 권한을 유지한다

<br>

<br>

`+`

### SCP로 AWS EC2에 파일 전송하기

ex)

```bash
scp -i [pem key 경로] [업로드할 파일 경로] [ec2 주소]:~
```
