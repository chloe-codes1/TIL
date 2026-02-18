# Type Hints in Python

> Learned about this today, so I'm organizing it!
>
> Reference: [python docs](https://docs.python.org/3.8/library/typing.html)

<br>

<br>

## Before getting started

- The Python runtime does not enforce type annotations on functions or variables
  - You need to use an IDE or type checker to verify them

- You can provide type hints to indicate types when using methods

<br>

<br>

## Function Annotations

> [docs](https://www.python.org/dev/peps/pep-3107/)

- Function annotations can be used for **Parameters** and **return values**, but they are not mandatory!
- Function annotations can be used to provide type checking
  - However, Lambda does not support annotations!

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

: Additionally, you can also use aliases!

ex)

```python
from typing import List
Vector = List[float]

def scale(scalar: float, vector: Vector) -> Vector:
    return [scalar * num for num in vector]

# typechecks; a list of floats qualifies as a Vector.
new_vector = scale(2.0, [1.0, -4.2, 5.4])
```


