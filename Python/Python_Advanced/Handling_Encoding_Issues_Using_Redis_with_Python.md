# Handling Encoding Issues Using Redis with Python

> Pythond에서 Redis 사용시 encoding issue 해결 방법

<br>

<br>

### Problem

:Python 에서 Redis에 문자열을 publish 하면 binary를 return 하는 문제 발생

<br>

<br>

### Solution

: [Redis Python interface](https://pypi.org/project/redis/) 가 **Redis connection class**에 대해 제공하는 **decode_responses** option을 활용하여 해결할 수 있다

<br>

ex)

![](../images/python-redis-issue.png)

- 위의 예시와 같이 **decode_responses** option을 **True**로 설정하면, client는 설정한 encoding option을 이용하여 decode한 결과값을 return 해준다
- 예시에서는 명시적으로 **charset="utf-8"**로 표현했으나 encoding default 값이 utf-8이므로 생략해도 된다

<br>

<br>

#### References

- <https://stackoverflow.com/questions/35726358/distinction-between-str-and-unicode-why-does-redis-return-binary-data-when-pass/35735233>
- <https://zedo.tistory.com/100>
- <https://zedo.tistory.com/100>
