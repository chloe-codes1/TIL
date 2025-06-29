# Resetting the permission in /usr/local

> macOS update 후 발생한 권한 문제 해결 방법을 공유해요

<br>

<br>

### Problem

: `brew cleanup` 명령어 실행 시 아래의 error를 뱉음

```bash
Error: Permission denied @ apply2files - /usr/local/lib/node_modules/serverless/node_modules/.bin/detect-libc
```

<br>

<br>

### Cause

: macOS to Mojave 10.14.X 이상 version으로 upgrade 후 발생하는 문제라고 함

[Reference - Homebrew github issue](https://github.com/Homebrew/homebrew-core/issues/45009#issuecomment-543795948)

<br>

<br>

### Solution

: `/usr/local` 에 부여된 권한을 reset하는 아래의 명령어를 실행한다

```bash
sudo chown -R $(whoami):admin /usr/local/* \
&& sudo chmod -R g+rwx /usr/local/*
```

<br>

<br>

*해결 완료!*
