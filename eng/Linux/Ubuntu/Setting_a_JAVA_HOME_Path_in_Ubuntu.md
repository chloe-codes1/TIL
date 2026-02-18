# Setting a JAVA_HOME Path in Ubuntu

> Notes from reconfiguring `JAVA_HOME` while switching from OpenJDK 8 to 11

<br>

### 1.  Install

```bash
sudo apt-get install openjdk-11-jdk
```

- This command also installs the `openjdk-11-jre` package which contains the Java runtime environment!

<br>

### 2. Check the version

```bash
chloe@chloe-XPS-15-9570 ~
$ java -version
openjdk version "11.0.8" 2020-07-14
OpenJDK Runtime Environment (build 11.0.8+10-post-Ubuntu-0ubuntu118.04.1)
OpenJDK 64-Bit Server VM (build 11.0.8+10-post-Ubuntu-0ubuntu118.04.1, mixed mode, sharing)
```

<br>

### 3. Find where JDK is installed

- You can find the installed JDKs by navigating to the `/usr/lib/jvm/` path

  ```bash
  chloe@chloe-XPS-15-9570 ~
  $ cd /usr/lib/jvm/

  chloe@chloe-XPS-15-9570 /usr/lib/jvm
  $ ls
  default-java     java-11-openjdk-amd64     java-8-openjdk-amd64
  java-1.11.0-openjdk-amd64  java-1.8.0-openjdk-amd64  openjdk-11

  ```

<br>

### 4. Set environment variable

> Open `/etc/environment` with vim

```bash
sudo vi /etc/environment
```

> Add the following environment variable

```
JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
export JAVA_HOME
```

> Apply the modified values immediately using the `source` command

```bash
source /etc/environment
```

<br>

### 5. Check the environment variable

#### 5-1. Check the configured environment variable using the `echo` command

```bash
chloe@chloe-XPS-15-9570 /usr/lib/jvm
$ echo $JAVA_HOME
/usr/lib/jvm/java-11-openjdk-amd64
```

#### 5-2. Check using the `printenv` command

```bash
chloe@chloe-XPS-15-9570 /usr/lib/jvm
$ printenv | grep "java"
JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
```

- Using `grep` allows you to search for a specific string!
  - Here we are searching for "java"!

<br>

<br>

*Done!*

<br>

<br>

<br>

`+`

### When you want to switch between alternatives and build with a specific version

``` bash
chloe@chloe-XPS-15-9570 ~
$ sudo update-alternatives --config java
[sudo] password for chloe:
There are 2 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                            Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      auto mode
  1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      manual mode
  2            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode

Press <enter> to keep the current choice[*], or type selection number:

```

- You can change to the desired version by entering its number
