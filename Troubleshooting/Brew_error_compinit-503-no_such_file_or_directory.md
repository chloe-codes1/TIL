# BREW ERROR : compinit:503: no such file or directory: /usr/local/share/zsh/site-functions/_brew_cask

> macOS update 후 발생한 brew error... 해결 방법을 공유해요

<br>

<br>

### Problem

: terminal 실행시 아래와 같은 error 가 출력됨

```bash
compinit:503: no such file or directory: /usr/local/share/zsh/site-functions/_brew_cask
compinit:503: no such file or directory: /usr/local/share/zsh/site-functions/_brew_cask
```

<br>

<br>

### Cause

: symlink 때문에 발생한 error

<br>

<br>

### Solution

: update 후 필요 없는 이전 version의 package를 삭제하는 아래의 명령어를 실행했다

```bash
brew cleanup
```

<br>

`+`

brew cleanup 명령어를 **dry run** 하고 싶으면 `-n` option을 주면 된다

```bash
brew cleanup -n
```

<br>

<br>*해결 완료!*
