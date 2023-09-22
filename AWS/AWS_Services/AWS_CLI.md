# AWS CLI

> 자꾸 잊어서 적어놓기...
>
> [Docs](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html)

<br>

<br>

## What is the AWS Command Line Interface?

<br>

- Command-line shell 을 사용하여 AWS 서비스와 상호작용할 수 있는 **open source tool**
- AWS CLI를 사용하면 **minimal configuration**으로 원하는 terminal program 에서 browser기반 AWS Management console에서 제공하는 것과 동일한 기능을 구현하는 명령을 실행할 수 있다
  - `Linux shells`
    - **bash**, **zsh**, **tcsh** 등의 일반적인 shell program을 사용하여 **Linux** 또는 **MacOS** 에서 명령 실행  
  - `Windows command line`
    - Windows에서는 **Powershell** 또는 **Windows command prompt** 를 사용하여 명령 실행
  - `Remotely`
    - **PuTTY**, **SSH** 등의 원격 터미널 프로그램 또는 **AWS Systems Manager** 를 통해 **EC2** instance에서 명령 실행

<br>

<br>

## Installing the AWS CLI version 2 on Linux

<br>

### 1. Download the installation file

> `curl`  명령어 사용

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```

<br>

### 2. Unzip the installer

```bash
unzip awscliv2.zip
```

<br>

### 3. Run the install program

```bash
sudo ./aws/install
```

<br>

### 4.  Confirm the installation

```bash
chloe@chloe-XPS-15-9570 ~
$ aws --version
aws-cli/2.0.19 Python/3.7.3 Linux/5.3.0-61-generic botocore/2.0.0dev23
```

<br>

<br>

## Configuring the AWS CLI

<br>

### configure

```bash
$ aws configure get aws_access_key_id
default_access_key

$ aws configure get default.aws_access_key_id
default_access_key

$ aws configure get aws_access_key_id --profile testing
testing_access_key

$ aws configure get profile.testing.aws_access_key_id
testing_access_key
```

<br>

ex)

> region 확인해보기

```bash
chloe@chloe-XPS-15-9570 ~/Workspace/kendra-button/frontend/kendra-button-front
$ aws configure get region
us-west-2
```
