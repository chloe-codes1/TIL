# Type Hints in Python

> 오늘 새로 알게되어서 정리!
>
> Reference: [python docs](https://docs.python.org/3.8/library/typing.html)

<br>

<br>

## Before getting started

- Python runtime은 function이나 variable의 type annotation을 강제시 하지 않는다
  - IDE나 type checker를 이용해야 확인 할 수 있다

- Type hint를 제공해서 method 사용 시 type을 알려줄 수 있다

<br>

<br>

## Function Annotations 

> [docs](https://www.python.org/dev/peps/pep-3107/)

- Function annotation은 **Parameter** 와 **return value** 에서 사용될 수 있는데 강제는 아니다!
- Function annotation을 활용하여 typechecking 을 제공할 수 있다
  - 단, Lambda는 annotation을 지원하지 않는다!

<br>

### Syntax

#### 1. Parameters

ex1) **parameter**

```python
def foo(a: expression, b: expression = 2):
  ...
```

<br>

ex2) **excess parameter** ( `*args`, `**kwargs` )

```python
def foo(*args: expression, **kwargs: expression):
    ...
```

<br>

#### 2. Return Values

ex)

```python
def sum() -> expression:
  ...
```

<br>

<br>

<br>

`+`

## Type aliases

: 추가로 alias를 활용할 수도 있다!

ex) 

```python
from typing import List
Vector = List[float]

def scale(scalar: float, vector: Vector) -> Vector:
    return [scalar * num for num in vector]

# typechecks; a list of floats qualifies as a Vector.
new_vector = scale(2.0, [1.0, -4.2, 5.4])
```



