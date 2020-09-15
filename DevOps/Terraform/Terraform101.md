#  Introduction to Terraform

> Reference: [Terraform docs](https://www.terraform.io/intro/index.html), [blog.naver.com/alice_k106](https://blog.naver.com/PostView.nhn?blogId=alice_k106&logNo=221489260596&parentCategoryNo=&categoryNo=24&viewDate=&isShowPopularPosts=false&from=postView)

<br>

<br>

## What is Terraform?

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

### tf apply

- 마찬가지로 프로젝트 root 경로에서 실행한다
- Terraform project directory 내의 모든 `.tf` 파일의 내용대로 resource를 **생성**, **수정**, **삭제** 하는일을 **적용**이라고 한다
- 이 명령어를 실행하기 전에 변경 예정 사항은 위의 **plan** 명령어를 사용해 확인할 수 있다