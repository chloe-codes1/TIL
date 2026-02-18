# RPM Options for RedHat/Fedora/Centos Installs

> Let's learn about RPM

<br>

<br>

### RPM (RedHat Package Manager)

- Package management system used by RedHat-based Linux distros
- FOSS (Free and open-source software)
- An installation file similar to Windows' `setup.exe`
- The file extension is `*.rpm`, which is called a package

<br>

### RPM File Format

```bash
name-version-release.os.architecture.rpm
```

- where:
  - **name**
    - package name
  - **version**
    - version of the packaged software
  - **release**
    - Release number of the RPM package
      - Number of times it has been modified and distributed
  - **os**
    - Distribution (OS) version
      - For RHEL (RedHat Enterprise Linux) including CentOS, the OS version is used in the rpm package file name
  - **architecture**
    - Architecture (CPU) of the RPM package
      - Refers to the CPU on which the package can be installed

- ex)
  - gedit-2.6.1-1.fc11.i586.rpm
  - mysql-connector-java-5.1.25-3.el7.noarch.rpm

<br>

<br>

### RPM Commands

```bash
rpm [option] [rpm package file or rpm package name]
```

<br>

#### Query

```bash
rpm -qa
rpm -qa [package name]
rpm -qa | grep [package name]
```

<br>

#### Install

```bash
rpm -Uvh [package file]
```

- **U** option
  - Install the package, and if it is already installed, upgrade it
- **v** option
  - Print the installation process when installing the package
- **h** option
  - Display the installation progress filled with `#` on screen

<br>

#### Remove

```bash
rpm -e [package name]
```

- Use the erase option to remove

<br>

#### Check consistency of installed packages

```bash
rpm -aV --nofiles --nodigest
```

<br>

#### Remove "broken" packages

```bash
rpm -e -vv --allmatches --nodeps --noscripts --notriggers package_name
```
