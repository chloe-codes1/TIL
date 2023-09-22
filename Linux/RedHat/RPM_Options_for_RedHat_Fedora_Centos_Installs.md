# RPM Options for RedHat/Fedora/Centos Installs

> RPM에 대해 알아보아요

<br>

<br>

### RPM (RedHat Package Manager)

- RedHat 계열의 linux distro에서 사용하는 package management system
- FOSS (Free and open-source software)
- windows의 `setup.exe` 와 유사한 설치 파일
- 확장자명은 `*.rpm` 이며, 이를 package라고 부른다

<br>

### RPM 파일 형식

```bash
name-version-release.os.architecture.rpm
```

- where:
  - **name**
    - pacakage name
  - **version**
    - packaged software의 version
  - **release**
    - 해당 RPM package의 release 번호
      - 수정되어 배포된 횟수
  - **os**
    - 배포판(OS) version
      - CentOS를 포함한 RHEL(RedHat EnterPrise Linux)의 경우, OS version을 rpm package file 이름에 사용한다
  - **architecture**
    - RMP package의 architecture (CPU)
      - package를 설치할 수 있는 CPU를 의미한다

- ex)
  - gedit-2.6.1-1.fc11.i586.rpm
  - mysql-connector-java-5.1.25-3.el7.noarch.rpm

<br>

<br>

### RPM Commands

```bash
rpm [option] [rpm package file or rpm package 이름]
```

<br>

#### 조회

```bash
rpm -qa
rpm -qa [package 이름]
rpm -qa | grep [package 이름]
```

<br>

#### 설치

```bash
rpm -Uvh [package file]
```

- **U** option
  - package를 설치하되, 만약 이미 설치되어 있다면 upgrade 하라
- **v** option
  - pcakge 설치 시 설치 과정을 출력하라
- **h** option
  - 설치 진행률을 `#` 로 채워서 화면에 출력하라

<br>

#### 삭제

```bash
rpm -e [package name]
```

- erase option을 사용하여 삭제한다

<br>

#### 설치된 package들의 consistency 확인

```bash
rpm -aV --nofiles --nodigest
```

<br>

#### "broken" package 삭제

```bash
rpm -e -vv --allmatches --nodeps --noscripts --notriggers package_name
```
