# Resetting the permission in /usr/local

> Sharing the solution for a permission issue that occurred after a macOS update

<br>

<br>

### Problem

: The following error is thrown when executing the `brew cleanup` command

```bash
Error: Permission denied @ apply2files - /usr/local/lib/node_modules/serverless/node_modules/.bin/detect-libc
```

<br>

<br>

### Cause

: Reportedly a problem that occurs after upgrading macOS to Mojave 10.14.X or higher

[Reference - Homebrew github issue](https://github.com/Homebrew/homebrew-core/issues/45009#issuecomment-543795948)

<br>

<br>

### Solution

: Execute the following command to reset the permissions granted to `/usr/local`

```bash
sudo chown -R $(whoami):admin /usr/local/* \
&& sudo chmod -R g+rwx /usr/local/*
```

<br>

<br>

*Resolved!*
