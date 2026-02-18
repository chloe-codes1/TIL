# Deploying a SpringBoot-React application on AWS EC2 using NGINX

> At SSAFY, they gave us 1 EC2 instance (no AWS Console access either....) so I deployed in a similar manner to [the previous time](https://chloe-codes1.gitbook.io/til/server/deployment/deploying_a_django-vue_application_on_aws_ec2_using_nginx)
>
> - Port `80` - React.js frontend serve
> - Port `8000` - SpringBoot backend serve

<br>

<br>

## Frontend Deployment

- The Frontend deployment is the same method as when deploying the `Django-Vue` project, so follow steps 1-9 from [this link](https://chloe-codes1.gitbook.io/til/server/deployment/deploying_a_django-vue_application_on_aws_ec2_using_nginx)
  - Of course, when installing required packages, skip steps that are unrelated to this project, such as Python installation!

<br>

<br>

## Backend Deployment

<br>

### 1. Install Java

#### 1-1. Install

```bash
sudo apt-get install openjdk-11-jdk
```

- This command also installs the `openjdk-11-jre` package which contains the Java runtime environment!

#### 1-2. Check version

```bash
$ java -version
openjdk version "11.0.8" 2020-07-14
OpenJDK Runtime Environment (build 11.0.8+10-post-Ubuntu-0ubuntu118.04.1)
OpenJDK 64-Bit Server VM (build 11.0.8+10-post-Ubuntu-0ubuntu118.04.1, mixed mode, sharing)
```

<br>

### 2. Install Maven

#### 2-1. Install `Maven`

```bash
sudo apt-get install maven
```

#### 2-2. Install `maven-wrapper`

```bash
mvn -N io.takari:maven:wrapper
```

#### 2-3.  Build

> Navigate to the location where `mvnw` is visible and execute the following command

```bash
./mvnw clean package
```

- Executing this command cleans the previous build records of the mvnw file in the current directory and builds a new package
  - This takes a long time! FYI!
- If you see the `BUILD SUCCESS` message, it was successful!

<br>

### 3. Execute the `.jar` file

#### 3-1. Execute

> Go into the `target` directory and execute the following command

```  bash
nohup java -jar [generated jar file name] &
```

- `nohup`
  - A program in Linux/Unix that runs shell script files (*.sh) in daemon mode
    - Keeps running even when the terminal session is disconnected
- Adding `&` after the command means separating the current command from other commands!
  - You can execute other commands while the server is running from the jar file
  - The jar file runs in the **background**!

<br>

### 4. Grant MySQL external access permissions

```bash
mysql> CREATE USER 'root'@'[server address]' IDENTIFIED BY '[root account password]';

mysql> GRANT ALL PRIVILEGES ON . TO 'root'@'[server address]' WITH GRANT OPTION;

mysql> FLUSH PRIVILEGES;
```

<br>

<br>

`+`

## Redeployment

> As I wrote in the previous deployment notes, this is very inefficient!!! Planning to apply CI/CD!!!
>
> -> [Applied it!](https://github.com/chloe-codes1/TIL/blob/master/Infra/CI-CD/Configuring_GitLab_CI-CD_with_AWS_EC2.md)

<br>

### When backend is modified

<br>

#### 1. Check the running port

```bash
$ lsof -i :8000
COMMAND  PID   USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
java    3972 ubuntu   22u  IPv6 325640      0t0  TCP *:8000 (LISTEN)
```

<br>

#### 2. Kill the port

```bash
sudo kill -9 [pid number confirmed above]
```

<br>

#### 3. Pull the project via git

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
java -jar [generated jar file name] &
```

<br>

<br>

### When frontend is modified

``` bash
git pull origin master

cd frontend

npm run build

sudo service nginx restart
```
