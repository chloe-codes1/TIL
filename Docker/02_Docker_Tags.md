# Docker Tags

> Reference: [docker docs](https://docs.docker.com/engine/reference/commandline/tag/)

<br>

<br>

## What are docker tags?

<br>

### Description

: Docker tag를 활용하여  docker image들의 version을 관리할 수 있다

<br>

### Usage

: Docker의 `tag` 명령어를 이용하여 기존에 만든 image에 추가로 tag 를 지정할 수 있다

```bash
docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```

<br>

<br>

## What happens when you don't specify a tag?

<br>

### `latest` tag

- Docker image 생성 시 `tag`명 지정을 생략하면, default  값으로 `latest` tag 가 붙는다
- `latest` tag 는 특정 **tag / version** 지정 없이 마지막으로 **build / tag** 된 image를 의미한다

<br>

### `latest` is Just a Tag, Doesn't Always Mean "Latest"

- `latest` 가 실제로 가장 최신 version 임을 의미하지 않는다

  - **:latest** tag 가 언제나 가장 최근에 push 된 image 라고 생각 할 수 있지만, 그렇지 않다
  - latest는 그저 tag 가 없는 image에 대해 default 값으로 주어진  tag 이다

- `latest` 는 동적이지 않다

  - tag 를 붙이지 않거나 tag를 **latest** 라고 지정하지 않는다면, **:latest** 는 영향을 받거나 새로 만들어지지 않는다

- Versioning을 위해 `latest` tag를 사용하지 않고, tag에 **patch number** 나 **git commit** 을 활용하는 것이 좋은  practice 이다
