# BREW ERROR : compinit:503: no such file or directory: /usr/local/share/zsh/site-functions/_brew_cask

> Sharing the solution for a brew error that occurred after a macOS update...

<br>

<br>

### Problem

: The following error is displayed when launching the terminal

```bash
compinit:503: no such file or directory: /usr/local/share/zsh/site-functions/_brew_cask
compinit:503: no such file or directory: /usr/local/share/zsh/site-functions/_brew_cask
```

<br>

<br>

### Cause

: Error caused by a symlink

<br>

<br>

### Solution

: Executed the following command which removes outdated packages from previous versions after the update

```bash
brew cleanup
```

<br>

`+`

If you want to **dry run** the brew cleanup command, add the `-n` option

```bash
brew cleanup -n
```

<br>

<br>*Resolved!*
