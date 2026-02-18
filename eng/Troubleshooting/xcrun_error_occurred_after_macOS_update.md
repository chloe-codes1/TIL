# xcrun error occurred after macOS update

> Sharing the solution for an xcrun error that occurred after a macOS update on a peaceful day...

<br>

<br>

### Problem

: After a macOS update (in my case, Big Sur version 11.1 -> 11.2), the following error occurs when using git

```bash
xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools), missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun
```

<br>

### Solution

- It can be resolved by updating `Xcode Command-line Tools`!

  - Commands

    ```bash
    xcode-select --install
    ```

  - Output

    ```bash
    xcode-select: note: install requested for command line developer tools
    ```

<br>

*Done!*
