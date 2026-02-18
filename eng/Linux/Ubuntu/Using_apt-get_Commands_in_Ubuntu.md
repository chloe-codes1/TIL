# Using apt-get Commands in Ubuntu

> A summary for Ubuntu beginners
>
> References: [It's FOSS](https://itsfoss.com/apt-get-linux-guide/), [ttend.tistory.com](https://ttend.tistory.com/316)

<br>

<br>

## What is `apt-get` ?

<br>

- Ubuntu is an operating system derived from `Debian Linux`

  - Ubuntu's core utilities come from Debian!

- Debian uses the `dpkg packaging system`

  - What is a **packaging system**?

    - One of the methods for installing and maintaining software on a system

    - Using a packaging system means you don't need to receive the source code and build the program yourself!

    - Linux has the **Debian family** which uses `deb` packages and the **RedHat family (.rpm)** which uses `rpm` packages

      - Debian family

        : Debian, Ubuntu, Linspire, Xandros

      - RedHat family

        : Fedora, CentOS, RHEL, openSUSE, Mandirva

<br>

### APT (Advanced Package Tool)

- A command line tool for interacting with the packaging system
  - You can also use the `dpkg` command, but `apt` is more user-friendly for handling packages!
- You can install, upgrade, and clean packages with `apt`
- It is a high level tool

<br>

<br>

### High Level & Low Level Tool

![image-20200712152926617](../../kor/images/image-20200712152926617.png)

<br>

#### Low level package tool

- Manages the tasks of installing and removing package files
  - ex) `dpkg` for Debian family, `rpm` for RedHat family

<br>

#### High level package tool

- Manages metadata search and dependency resolution tasks

<br>

<br>

### Main Tools of APT

: The main tools of apt are `apt-get` and `apt-cache`

<br>

#### apt-get

- Used to install, upgrade, and clean packages

<br>

#### apt-cache

- Used to find new packages

<br>

<br>

## Using apt-get commands

<br>

### Updating packages with apt-get

<br>

#### Command

```bash
sudo apt-get update
```

<br>

#### Result

![image-20200712152852441](../../kor/images/image-20200712152852441.png)

- `Hit`
  - Means there is no change in the package version
- `Ign`
  - Means the package was ignored
    - There can be various reasons
      - ex)
        - When it is so up-to-date that there is no need to check for a newer version
        - When an error occurred while searching for the package but it was a minor error so it was ignored
          - In conclusion, it is not an error so no need to worry!

- `Get`
  - When there is a new version of the package, **apt-get** downloads that information
    - The new version information, not the package itself!

<br>

<br>

### Upgrading packages with apt-get

- Once you have an updated package database through `$ sudo apt-get update`, you can now upgrade the packages

<br>

#### Command

> Upgrade all packages

```bash
sudo apt-get upgrade
```

- Adding `-y` at the end means you don't need to separately type `y` when asked whether to upgrade

> Upgrade a specific package

```bash
sudo apt-get upgrade [package name]
```

<br>

#### Result

![image-20200712211408819](../../kor/images/image-20200712211408819.png)

<br>

<br>

## Using apt-cache commands

<br>

### Searching for packages with apt-cache

- Useful for finding specific libraries

<br>

#### Command

> When you know the exact package name

```bash
apt-cache search [package name]
```

> When searching for packages starting with a specific name

``` bash
apt-cache pkgnames [package name]
```

<br>

#### Result

![image-20200712214241701](../../kor/images/image-20200712214241701.png)

<br>

<br>
