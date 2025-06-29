# Amazon ECR (Elastic Container Registry)

> Reference: [AWS docs](https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html)

<br>

<br>

## What is Amazon Elasitc Container Registry?

<br>

- Amazon ECR(Elastic Container Registry)는 **안전**하고 **확장 가능** 하며 **신뢰** 할 수 있는 **Fully-managed Docker Container Image Registry Service** 이다
- ECR은 `AWS IAM` 을 활용한 **resource-based permission** 을 제공한다
  - How?
    - 특정 user 혹은  EC2 instance만 ECR repository와 image 에 접속 할 수 있다

- 개발자는 Preferred CLi를 사용하여 **Docker image**, **OCI (Open Container Initiative) image** 및 OCI 호환 artifact를 push, pull 및 관리 할 수 있다

<br>

<br>

## Components of Amazon ECR

<br>

### Registry

- Amazon ECR Registry 는 각 계정마다 만들 수 있고, Registry 안에 **image repository** 를 만들어서 image들을 저장할 수 있다

<br>

### Authorization token

- Amazon ECR registry에 인증된  AWS user만이 ECR에 image들을 **Push / Pull** 할 수 있다

<br>

### Repository

- Amazon ECR image repository에 **Docker iamge** 들을 보관할 수 있다

<br>

### Repository policy

- Repository와 image 들에 대한 접근 권한을 **repository policy** 로 관리 할 수 있다

<br>

### Image

- Repository에 Container image들을 **Push / Pull** 할 수 있다

<br>

<br>

## Features of Amazon ECR

<br>

- **Lifecycle policy**를 활용하여 repository 내의 image들에 대한 lifecycle 관리를 할 수 있다
  - 정책을 생성하여 사용되지 않는 image 들을 제거할 수 있다
- **Image scanning** 을 활용하여 image 의 **소프트웨어 취약성** 를 식별하는 데 도움을 줄 수 있다
