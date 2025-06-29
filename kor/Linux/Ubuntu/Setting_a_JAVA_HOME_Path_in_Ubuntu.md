# Setting a JAVA_HOME Path in Ubuntu

> open jdk 8에서 11로 바꾸면서 `JAVA_HOME` 재설정 한 것 정리해용

<br>

### 1.  Install

```bash
sudo apt-get install openjdk-11-jdk
```

- 이 명령어로 Java runtime environment를 갖고있는 `openjdk-11-jre` package 까지 설치된다!

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

- `/usr/lib/jvm/`경로에 가면 설치한 JDK 들을 확인할 수 있다

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

> vim으로  `/etc/environment` 열기

```bash
sudo vi /etc/environment
```

> 아래의 환경변수를 추가하기

```
JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
export JAVA_HOME
```

> `source` 명령어로 수정된 값 바로 적용하기

```bash
source /etc/environment
```

<br>

### 5. Check the environment variable

#### 5-1. `echo` 명령어로 설정한 환경변수 확인하기

```bash
chloe@chloe-XPS-15-9570 /usr/lib/jvm
$ echo $JAVA_HOME
/usr/lib/jvm/java-11-openjdk-amd64
```

#### 5-2. `printenv` 명령어로 확인하기

```bash
chloe@chloe-XPS-15-9570 /usr/lib/jvm
$ printenv | grep "java"
JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
```

- `grep` 을 사용하면 특정 문자열을 찾을 수 있다!
  - 여기서는 "java" 를 찾는 것!

<br>

<br>

*끝~!*

<br>

<br>

<br>

`+`

### Alternatives 중에 필요한 버전으로 바꾸어서 Build 하고싶을 때

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

- 원하는 version의 번호를 입력하면 변경 가능하다
