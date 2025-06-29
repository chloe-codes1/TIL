# Introduction to Terraform

> Reference: [Terraform docs](https://www.terraform.io/intro/index.html), [blog.naver.com/alice_k106](https://blog.naver.com/PostView.nhn?blogId=alice_k106&logNo=221489260596&parentCategoryNo=&categoryNo=24&viewDate=&isShowPopularPosts=false&from=postView), [인프런] DevOps : Infrastructure as Code with Terraform and AWS 강좌 by 송주영님

<br>

<br>

## Before getting started

> 인프런 강좌를 듣고 추가한 내용

<br>

### IaC (Infrastructure as code)

- 인프라를 이루는 서버, 미들웨어, 서비스 등 인프라 구성요소들을 코드를 통해 구축하는 것
  - IaC는 코드로써의 장점
    - 작성용이성
      - 작성하는 것이 빨라진다!
    - 재사용성
    - 유지보수 등의 장점을 가진다

<br>

### Terraform by Hashicorp

> Terraform is a tool for building, changing, and versioning infrastructure safely and efficiently

- Terraform은 인프라를 만들고, 변경하고 기록하는 IaC를 위해 만들어진 도구로써
  - 문법이 쉬워 비교적 다루기 쉽고, 사용자가 매우 많아 참고할 수 있는 예제가 많다
- `.tf` 형식의 파일 확장자를 갖는다
- AWS, Azure, GCP 같은 Public Cloud 뿐만이 아닌 다양한 Provider를 지원한다

<br>

### Terraform 기본 구성 요소

- **provider**

  - Terraform으로 생성할 Infra의 종류

    - Terraform 은 정말 다양한 provider를 지원한다!

  - 보통 `provider.tf` 로 파일을 생성한다

  - ex)

    ```yaml
    provider "aws" {
     region = "ap-northeast-2"
     version = "~> 3.0"
    }
    ```

    - Provider 안에서 다양한 argument를 가진다
    - AWS resource를 다루기 위한 파일들을 다운로드하는 역할을 한다

<br>

- **resource**

  - Terraform으로 실제로 생성할 인프라 자원

  - 원하는 형태로 파일 이름을 사용한다

  - ex)

    ```yaml
    resource "aws_vpc" "example" {
     cidr_block = "10.0.0.0/16"  # cidr_block 외에도 수많은 인자가 존재한다
    }
    ```

  - Terraform으로 VPC를 생성하는 코드이다
  - VPC 역시 다양한 argument와 다른 구성요소가 존재한다

<br>

- **state**

  - Terrafrom을 통해 생성한 자원의 상태

    - 실제로 Terraform 코드를 실행한 결과물
    - `terraform.tfstate` 라는 파일명을 가짐
      - 실제로는 코드가 굉장히 길어질 수 있음

  - ex)

    ```yaml
    {
     "version": 4,
     "terraform_version": "0.12.24",
     "serial": 3,
     "lineage": "3c77xxxx-2de4-7736-1447-038974a3c187",
     "outputs": {},
     "resources": [
      {...},
      {...}
     ]
    }
    ```

    - Terraform의 state이다
      - 현재 인프라의 상태를 의미하는 것은 아님!!
        - Terraform 명령어를 사용해서 생성한 resource들의 결과물이고, 인프라의 실제 상태는 아님!!
          - 그래서 **state 파일**과 **현재 인프라의 상태**를 동일하게 유지하는 것이 중요하다!
    - state는 원격 저장소의 **backend**에 저장 될 수 있다
      - 현재 현업에서는 대부분 backend를 사용한다

<br>

- **output**

  - Terraform으로 만든 자원을 변수 형태로 state 파일에 저장하는 것

  - ex)

    ```yaml
    resource "aws_vpc" "default" {
     cidr_block = "10.0.0.0/16"  # cidr_block 외에도 수많은 인자가 존재한다
    }
    
    output "vpc_id" {
     value = aws_vpc.default.id
    }
    
    output "cidr_block" {
     value = aws_vpc.default.cidr_block
    }
    ```

    - vpc id 나 cidr값을 참조해서 `vpc_id` 라는 변수를 **state** 파일로 저장하는 것
    - output으로 추출된 부분은 이후에 `remote state` 를 활용해서 재사용 할 수 있다

<br>

- **backend**
  - terraform 상태를 저장할 공간을 지정하는 부분
    - 생성된 **output**, 즉 variable로 생성된 **state file**을 저장하는 **공간**
  - backend를 사용하면 현재 배포된 최신 상태를 외부에 저장하기 때문에 다른 사람과의 **협업**이 가능하다!
    - 대표적으로 AWS S3가 있다

- **module**

  - 공통적으로 활용할 수 있는 code를 말그대로 module 형태로 정의하는 것

    - 재사용 하는데 강점이 있다

  - 일종의 **함수**라고 생각하면 편하다

    - 여러 terraform code를 **변수**만 바꾸어서 **하나의 module**로 생성하는 것을 의미
  
  - ex)
  
    ```yaml
    module "vpc" {
     source = ":./_modulesvpc"
   
     cidr_block = "1.0.0.0/16"
    }
    ```
  
    - 한 번 만들어진 Terraform 코드로 같은 형태를 반복적으로 만들어낼 때 주로 사용

<br>

- **remote state**

  - 다른 경로의 state를 참조하는 것

    - 원격 참조 개념
    - `output`  변수를 불러올 때 주로 사용

  - remote state를 사용하면 `VPC`, `IAM` 등과 같은 공용 service를 다른 service 에서 참조할 수 있다

    - **tfstate 파일 (최신 terraform 상태 정보)** 이 저장되어 있는 backend 정보를 명시하면,
      - 해당 backend에서 output 정보들을 가져온다
  
  - ex)
  
    ```yaml
    data "terraform_remote_state" "vpc"{
     backend = "remote"
     
     config = {
      bucket  = "terraform-s3-bucket"
    region  = "ap-northeast-2"
      key    = "terraform/vpc/terraform.tfstate"
     }
    }
    ```
  
    - remote state 는  key 값에 명시한 **state** 에서 output을 통해 생성된 변수를 가져온다

<br>

### Terraform 작동 원리

- Terraform에는 3가지 형상이 존재한다
  1. **Local code**
     - 현재 개발자가 작성/수정하고 있는 code
  2. **AWS 실제 인프라**
     - 실제로 AWS에 배포되어 있는 인프라
  3. **Backend에 저장된 상태**
     - 가장 최근에 배포한 terraform code 형상
       - `tfstate` 파일
- 여기서 가장 중요한 것은 `AWS 실제 인프라` 와 `Backend에 저장된 상태` 가 **100% 일치하도록 만드는 것** 이다!!!
  - Terraform을 운영하면서 최대한 이 두가지가 100% 동일하도록 유지하는 것이 중요한데,
    - Terraform에서는 이를 위해 **import**, **state** 등 여러 명령어를 제공한다
- 인프라 정의는 먼저 `Local code` 에서 시작한다
  - 개발자는 local에서 terraform code를 정의한 후에
  - 해당 코드를 실제 인프라로 프로비전한다
    - 이 때, backend를 구성하여 최신 코드를 저장한다

<br>

### Terraform 기본 명령어

#### init

- Terraform 명령어 사용을 위한 각종 설정을 진행
  - 지정한 backend에 상태 저장을 위한 `.tfstate` 파일을 생성한다
    - 여기에는 가장 마지막에 적용한 terraform 내역이 저장된다
  - init 작업을 완료하면, local에는 `.tfstate`  에 정의된 내용을 담은 `.terraform` 파일이 생성된다
  - 기존에 다른 개발자가 이미 `.tfstate` 에 인프라를 정의해 놓은 것이 있다면, 다른 개발자는 **init** 작업을 통해서 local에 **sync**를 맞출 수 있다

#### plan

- Terraform으로 작성한 코드가 실제로 어떻게 만들어질지에 대한 예측 결과를 보여줌
  - 단, plan을 한 내용에 error가 없어도, 실제 적용되었을 때는 error가 발생 할 수 있으므로 유의해야 한다!
  - **Plan 명령어는 어떠한 형상에도 변화를 주지 않는다**

#### apply

- Terraform 코드를 바탕으로 실제로 인프라를 생성하는 명령어
  - **apply**를 완료하면 AWS 상에 실제로 해당 인프라가 생성되고,
    - 작업 결과가 backend의 `.tfstate` 파일에 저장된다
      - 해당 결과는 local의 `.terraform` 파일에도 저장된다
  - 실제 인프라에 영향을 끼치는 명령어이기때문에 주의깊게 실행해야함!
    - 그래서 `apply` 전에 꼭 `plan` 을 해야함!

#### import

- 이미 만들어진 자원을 `terraform state` 파일로 옮겨주는 명령어

  - 이미 만들어진 자원을 code로 옮기고 싶을 때 사용

  - local의 `.terraform` 에 해당 resource의 **상태 정보**를 저장해주는 역할을 한다

    - 단, **code를 생성해주지 않는다!!**
      - apply 전까지는 backend에 저장되지 않는다
      - import 이후에 plan 을 하면 **local에 해당 코드가 없기 때문에** resource가 삭제 또는 변경된다는 결과를 보여준다
        - 이 결과를 바탕으로 code를 작성할 수 있다

  - ex)

    ```bash
    terraform import [options] ADDRESS ID
    ```

#### state

- Terraform state를 다루는 명령어

  - 실제로 생성된 인프라를 볼 수 있다

    - ex)

      ```bash
      terraform state list
      ```

  - 하위 명령어로 mv, push 같은 명령어가 있음

#### destroy

- 생성된 자원들을 state 파일 기준으로 모두 삭제하는 방법

#### workspace

- workspace를 관리할 때 쓰이는 명령어

  - ex1)

    ```bash
    $ terraform workspace list
      default
    * product
    ```

    - workspace 목록을 보여준다
    - 현재 사용중인 workspace는 asterisk(`*`)로 표시된다

  - ex2)

    ```bash
    terraform workspace select [NAME]
    ```

    - 다른 workspace로 이동 할 때 사용한다

  - ex3)

    ```bash
    terraform workspace new [NAME]
    ```

    - 새로운 workspace를 생성할 때 사용한다

<br>

<br>

## What is Terraform?

> Terraform docs와 블로그를 참고하여 정리한 내용

<br>

- Infrastructure를 안전하고 효율적으로 **빌드**, **수정**하고 **versioning** 할 수 있는 tool
- Terraform이 `Ansible` 이나 `Chef` 와 비슷하다고 생각할 수 있으나, Terraform은 **특정 Cloud 환경** 에 초점이 맞춰져 있다는 것이 다르다
  - `Ansible` 은 일반 서버, 가상 머신, 심지어 라즈베리파이에서도 SSH를 통해 **동일한 환경** 을 배포할 수 있는 반면,
  - `Terraform` 은 AWS, GCP 등의 Cloud platform 위에서 환경을 배포할 때 주로 사용한다
    - Code 로서 Infra를 정의한다는 개념 자체는 `Ansible` 과 같은 환경 배포 tool과 동일하며,
    - 일반 **Bare Metal Server** 가 아닌 특정 **Cloud Platform** 에 맞는 환경을 code로서 배포한다는 점이 다르다

<br>

### Code로서 Infra를 정의하기 & 재현 가능한 Infra

- 테라폼의 웹페이지에서 강조하는 것이
  - **Infrastructure as a Code (코드로서 인프라를 정의하기)**
  - **Reproducible Infrastructure (재현 가능한 인프라)** 이다
- AWS든, GCP든, Azure든 Cloud Infra 환경을 코드로서 정의해 사용함으로써 **동일한 인프라**를 재현할 수 있다는 뜻이다
  - 동일 클라우드 내에서!

- 클라우드 인프라를 코드로 명시적으로 정의하니 수십번을 실행해도 **동일한 환경**이 생성될것이다.

<br>

### Terraform 도입 시  workflow

- 미리 준비한  Terraform template들을 사용하면 원하는 환경을 cloud에 배포할 수 있다
  - 예를들어 VPC는 `vpc.tf` 라는 파일에, EC2 instance는 `instance.tf` 파일에, subnet은 `subnet.tf` 파일에 저장한 뒤 **Terraform** 을 실행시키기만 하면 동일한 환경을 cloud에서 완벽하게 재현할 수 있다
  - 이러한 cloud 환경 설정은 사람이 직접 일일이 작업하는 것이 아니라, **HCL (Hashicorp Configuration Language)** 라는 언어로 작성된 코드를 Terraform에 입력함으로써 구성된다
- 모든 cloud 설정은 code에 의해 명시적으로 작성되기 때문에 cloud infra를  **동일하게 배포**하는 것이 가능해진다
- 다양한 요구사항에 맞도록 여러 version의 code를 작성해 cloud infra의 **revision** 을 관리할 수도 있다
  - 미리 준비해둔 Terrafrom 설정 파일을 Terraform에서 사용하기만 하면 복잡한 AWS cloud 환경을 한꺼번에 생서앟고 한꺼번에 삭제할 수도 있다

<br>

<br>

## Terraform Quickstart

<br>

### 0. Terraform 파일의 구성

- Terraform 파일인 `.tf` 파일은 일반적으로 아래와 같이 구성된다

![image-20200921011906162](../../images/image-20200921011906162.png)

- **resource**
  - Terraform 파일에서 사용되는 object 종류
    - 변수를 나타내는 `resource`
    - Data를 나타내는 `data` 등이 있다
- **aws_key_par**
  - AWS의 SSH key pair를 위한 resource 이름
    - AWS에서 사용되는 object를 terraform에서 부르는 이름
    - 이러한 이름들은 Terraform 공식 docs 에 정리되어 있다
- **terraform-key**
  - Terraform 파일에서 이 object를 고유하게 식별하게 될 이름
    - 가능하면 모든 파일 내에서 고유한 이름을 사용하는 것이 좋다

<br>

### 1. tf init

- terraform project의 root에서 실행한다

- Terraform을 사용하기 위해서는 Terraform **초기화** 작업이 필요하다

  - **terraform init** 명령어를 사용해 terraform directory를 초기화한다

- 사용하는 경우

  1. 처음 프로젝트를 시작한 경우
  2. `module` 이 변경된 경우

- ex)

  ```bash
  ~/workspace/monocoque/dev-musinsa-main master* ⇣ 17s
  ❯ tf init        
  Initializing modules...
  
  Initializing the backend...
  
  Initializing provider plugins...
  
  Terraform has been successfully initialized!
  
  You may now begin working with Terraform. Try running "terraform plan" to see
  any changes that are required for your infrastructure. All Terraform commands
  should now work.
  
  If you ever set or change modules or backend configuration for Terraform,
  rerun this command to reinitialize your working directory. If you forget, other
  commands will detect it and remind you to do so if necessary.
  ```

<br>

### 2. tf workspace

- 마찬가지로 해당 프로젝트의 root 경로에서 실행한다

- Commands

  - `tf workspace list`

    - workspace 목록 보기

      ex)

      ```bash
      ~/workspace/monocoque/dev-musinsa-main master* ⇣
      ❯ tf workspace list
      * default
        main
      ```

  - `tf workspace select main`

    - workspace 선택하기

      ex)

      ```bash
      ~/workspace/monocoque/dev-musinsa-main master* ⇣
      ❯ tf workspace select main
      Switched to workspace "main".
      ```

<br>

### 3. tf plan

- 마찬가지로 해당 프로젝트의 root 경로에서 실행한다

- Terraform project directory 내의 모든 `.tf` 파일의 내용을 실제로 적용 가능한지 **확인**하는 작업을 계획 이라고 한다

- **terraform plan** 명령어를 실행하면

  - 어떤 resource가 생성되고
  - 수정되고
  - 삭제될지 계획을 보여준다

- ex)

  ```bash
      ~/workspace/monocoque/dev-musinsa-main master*
      ❯ tf plan
      Refreshing Terraform state in-memory prior to plan...
      The refreshed state will be used to calculate this plan, but will not be
      persisted to local or remote state storage.
  
    ...
      
      Plan: 6 to add, 0 to change, 0 to destroy.
  
      ------------------------------------------------------------------------
  
      Note: You didn't specify an "-out" parameter to save this plan, so Terraform
      can't guarantee that exactly these actions will be performed if
      "terraform apply" is subsequently run.
  ```
  
- 실행 결과를 보고, 계획한 대로 생성되는 지 확인한다

<br>

### 4. tf apply

- 마찬가지로 프로젝트 root 경로에서 실행한다
- Terraform project directory 내의 모든 `.tf` 파일의 내용대로 resource를 **생성**, **수정**, **삭제** 하는일을 **적용**이라고 한다
- 이 명령어를 실행하기 전에 변경 예정 사항은 위의 **plan** 명령어를 사용해 확인할 수 있다

<br>

### 5. tf force-unlock [ID]

- terraform state lock 걸렸을 때 사용
- 아래의 error message 출력 시 ID 값을 tf force-unlock 뒤에 입력한다

```bash
Error: Error locking state: Error acquiring the state lock: ConditionalCheckFailedException: The conditional request failed
Lock Info:
  ID:        ID 값
  Path:      PATH
  Operation: OperationTypePlan
  Who:       chloe@Chloes-MacBookPro.local
  Version:   0.12.26
  Created:   2021-02-05 03:26:02.065859 +0000 UTC
  Info:      


Terraform acquires a state lock to protect the state from being written
by multiple users at the same time. Please resolve the issue above and try
again. For most commands, you can disable locking with the "-lock=false"
flag, but this is not recommended.
```
