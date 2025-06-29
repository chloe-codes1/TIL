# Amazon Athena

> Amazon Athena에 대해 알아보아요
>
> Reference: [aws docs](https://docs.aws.amazon.com/athena/latest/ug/what-is.html)

<br>

<br>

## What is Amazon Athena?

<br>

- Amazon Athena는 `Amazon S3 (Amazon Simple Storage Service)`에서 **표준 SQL** 을 사용하여 data를 바로 쉽게 분석할 수 있는 **대화형 쿼리 서비스** 이다
- AWS Management Console에서 몇 가지 작업을 수행하면
  - `Amazon S3` 에 저장된 data에서 **Athena** 를 가리키고,
  - **표준 SQL** 을 사용하여 임시 쿼리를 실행하고,
  - 몇 초 안에 결과를 얻을 수 있다

- Athena는 **serverless**이므로
  - 설정하거나 관리할 infra가 없으며,
  - 실행한 쿼리에 대해사먼 지불한다
- 큰 dataset의 복잡한 쿼리에서도 결과가 빠르다

<br>
