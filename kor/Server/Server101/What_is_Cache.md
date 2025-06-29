# What is Cache?

> Cache에 대해 알아보아요
>
> References: [jehovah's brunch](https://brunch.co.kr/@jehovah/20)

<br>

<br>

## Cache란?

- 한 번 읽어온 data를 **임의의 공간**에 저장하여,
  - 다음에 읽을 때는 **빠르게** 결과값을 받을 수 있도록 도와주는 공간
    - 같은 요청이 여러번 들어오는 경우 **Cache Server** 에서 바로 결과값을 반환해주기 때문에 DB 부하를 줄일 수 있다
- 프로그램이 수행될 때 나타나는 **지역성**을 이요하여 memory나 disk 에서 사용되었던 내용을 빠르게 접근할 수 있는 곳에 **보관**하고, **관리**함으로써 다음에 필요할 때 빠르게 참조할 수 있도록 하는 것
  - 즉, *사용되었던 data 는 다시 사용되어질 가능성이 높다*  라는 개념을 이용한 것
    - 다시 사용될 확률이 높은 data들을 **좀 더 빠르게** 접근 가능한 저장소를 사용하는 것이다!

<br>

<br>

## 사용 패턴

<br>

### Cache 사용 패턴 1 - Data Cache

- Client가 web server에 request를 보내면, web server는 **DB**에서 data를 가져오기 전에 **Cache** 에 data가 있는지 확인한다
  - **Cache server에 data가 있으면,**
    - Data를 DB에 요청하지 않고, client에 cache된 data를 반환한다
      - 이것을 `Cache hit` 라고 한다
  - **Cache server에 data가 없으면,**
    - `Cache miss` 의 상황이며, DB에 해당 data를 요청한다
      - DB는 사용자가 원하는 data를 반환해주고,
      - Web Server는 반환된 data를 다음에 사용할 수 있도록 **cache**에 저장한 후 client에 반환한다
        - 이후에 같은 요청이 올 때 **cache**에 저장된 data를 반환할 수 있으므로 `Cache hit` 이 발생한다

- 이 구조는 **Static assets**를 cache 해주는 **CDN service**와 동일한 구조이다
  - `Amazon CloudFront`와 같은 CDN service들은 data 원본을 가지고 있는 origin (ex. Amazon S3) 의 data를 cache해서,
  - 다음에 같은 요청이 있을 때 origin data를 요청하지 않고 바로 결과를 반환할 수 있다

<br>

### Cache 사용 패턴 2 - 동시다발적인 쓰기가 발생하는 경우

- **동시다발적 쓰기**가 발생하는 경우 DB에 갑자기 쓰기 요청이 몰려서 DB가 터질 수 있는데, 이럴 때 Cache를 활용할 수 있다
  - Client는 web server에 쓰기 요청을 하고,  
    - web server는 **cache**에 data를 write한 후 바로 결과를 반환한다
  - Cache는 보통 **memory**를 사용하기 때문에 속도가 상당히 빠르다
    - 따로 작동하고 있는 **worker server** 들은
      - **cache server**에 있는 data를 가져와서
      - 작업을 수행하고,
      - 결과를 DB에 write한다
    - 이렇게 함으로써 DB는 순차적으로 **transaction**을 처리할 수 있게 된다

<br>

<br>

### Terms

- `Cache hit`
  - 참조하고자 하는 data가 cache에 존재하고 있을 경우
- `Cache miss`
  - 참조하고자 하는 data가 cache에 존재하지 않을 때
