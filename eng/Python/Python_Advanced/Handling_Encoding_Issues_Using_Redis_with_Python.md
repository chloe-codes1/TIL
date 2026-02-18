# Handling Encoding Issues Using Redis with Python

> How to resolve encoding issues when using Redis in Python

<br>

<br>

### Problem

: When publishing strings to Redis in Python, a problem occurs where binary is returned

<br>

<br>

### Solution

: This can be resolved by using the **decode_responses** option provided by the [Redis Python interface](https://pypi.org/project/redis/) for the **Redis connection class**

<br>

ex)

![](../../kor/images/python-redis-issue.png)

- As shown in the example above, if you set the **decode_responses** option to **True**, the client will return decoded results using the configured encoding option
- In the example, **charset="utf-8"** is explicitly specified, but since the default encoding value is utf-8, it can be omitted

<br>

<br>

#### References

- <https://stackoverflow.com/questions/35726358/distinction-between-str-and-unicode-why-does-redis-return-binary-data-when-pass/35735233>
- <https://zedo.tistory.com/100>
- <https://zedo.tistory.com/100>
