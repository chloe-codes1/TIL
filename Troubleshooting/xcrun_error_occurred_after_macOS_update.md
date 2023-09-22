# xrun error occurred after macOS update

> 평화로운 어느날 macOS update 후 발생한 xrun error... 해결 방법을 공유해요

<br>

<br>

### Problem

: macOS update (나는 Big Sur version 11.1 -> 11.2) 후에 git 사용시 아래와 같은 에러 발생

```bash
xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools), missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun
```

<br>

### Solution

- `Xcode Command-line Tools`를 update 하면 해결 가능하다!

  - Commands

    ```bash
    xcode-select --install
    ```

  - Output

    ```bash
    xcode-select: note: install requested for command line developer tools
    ```

<br>

*끝!*
