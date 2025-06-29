# Deploying a SpringBoot-React application on AWS EC2 using NGINX

> SSAFY에서 EC2 인스턴스를 1개 줘서 (AWS Console 도 없음....) [지난 번](https://chloe-codes1.gitbook.io/til/server/deployment/deploying_a_django-vue_application_on_aws_ec2_using_nginx)과 유사한 방식으로 배포 했다
>
> - `80` 번 포트 - React.js frontend serve
> - `8000` 번 포트 - SpringBoot backend serve

<br>

<br>

## Frontend 배포

- Frontend는 `Django-Vue`  프로젝트 배포 시 했던 방식과 동일하므로 [이 링크](https://chloe-codes1.gitbook.io/til/server/deployment/deploying_a_django-vue_application_on_aws_ec2_using_nginx)에서 1~9 번을 진행하면 된다
  - 물론 필요한 패키지 설치 시, 해당 프로젝트와 관련 없는 파이썬 설치 등은 건너 뛰자!

<br>

<br>

## Backend 배포

<br>

### 1. Java 설치

#### 1-1. Install

```bash
sudo apt-get install openjdk-11-jdk
```

- 이 명령어로 Java runtime environment를 갖고있는 `openjdk-11-jre` package 까지 설치된다!

#### 1-2. version 확인

```bash
$ java -version
openjdk version "11.0.8" 2020-07-14
OpenJDK Runtime Environment (build 11.0.8+10-post-Ubuntu-0ubuntu118.04.1)
OpenJDK 64-Bit Server VM (build 11.0.8+10-post-Ubuntu-0ubuntu118.04.1, mixed mode, sharing)
```

<br>

### 2. Maven 설치

#### 2-1. Install `Maven`

```bash
sudo apt-get install maven
```

#### 2-2. Install `maven-wrapper`

```bash
mvn -N io.takari:maven:wrapper
```

#### 2-3.  Build

> `mvnw` 가 보이는 위치로 들어가서 아래의 명령어를 실행한다

```bash
./mvnw clean package
```

- 이 명령어를 실행하면, 현재 디렉토리에 있는 mvnw 파일의 이전 기록들을 clean 하고 새로 package로 빌드한다
  - 시간 오래 걸린다! 참고!
- `BUILD SUCCESS` message가 뜨면 성공한 것!

<br>

### 3. `.jar` 파일 실행

#### 3-1. Execute

> `target` directory 안으로 들어가서 아래의 명령어를 실행한다

```  bash
nohup java -jar [생성된 jar 파일 이름] &
```

- `nohup`
  - Linux, Unix에서 shell script 파일 (*.sh)을 demon 형태로 실행시키는 프로그램
    - terminal session이 끊겨도 계속 동작하게 함
- 명령어 뒤에 `&`를 붙이면 현재의 명령과 다른 명령을 분리한다는 의미!
  - jar 파일로 서버를 실행하고도 다른 명령어들을 수행할 수 있다
  - **background** 에서 jar 파일이 실행된다!

<br>

### 4. mysql 외부 접속 허용 권한 부여

```bash
mysql> CREATE USER 'root'@'[서버 주소]' IDENTIFIED BY '[root 계정 비밀번호]';

mysql> GRANT ALL PRIVILEGES ON . TO 'root'@'[서버 주소]' WITH GRANT OPTION;

mysql> FLUSH PRIVILEGES;
```

<br>

<br>

`+`

## 재배포

> 지난번 배포 기록에서도 적었지만 매우 비효율적이다!!! CI/CD 적용할 예정!!!
>
> -> [적용 했다!](https://github.com/chloe-codes1/TIL/blob/master/Infra/CI-CD/Configuring_GitLab_CI-CD_with_AWS_EC2.md)

<br>

### backend 수정 시

<br>

#### 1. 작동중인 포트 확인

```bash
$ lsof -i :8000
COMMAND  PID   USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
java    3972 ubuntu   22u  IPv6 325640      0t0  TCP *:8000 (LISTEN)
```

<br>

#### 2. 포트 종료시키기

```bash
sudo kill -9 [위에서 확인한 pid번호]
```

<br>

#### 3. git으로 프로젝트 Pull 받기

```bash
git pull origin master
```

<br>

#### 4. build

```bash
./mvnw clean package
```

#### 5. run

```bash
java -jar [생성된 jar 파일 이름] &
```

<br>

<br>

### frontend 수정 시

``` bash
git pull origin master

cd frontend

npm run build

sudo service nginx restart
```
