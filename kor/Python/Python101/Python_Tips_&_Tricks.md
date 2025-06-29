# Python Tips & Tricks

> Some tips and tricks you can use to bring up your Python programming

<br>

<br>

### `float('inf')`

: acts as an unbounded upper value for comparison

- `inf`  is infinity

  - a value that is greater than any other value

- `-inf`

  - is smaller than any other value

  <br>

ex)

```python
min_value = float('inf')
max_value = float('-inf')

nums = [1,2,3,4,5]

for num in nums:
    if num > max_value:
        max_value = num
    if num < min_value:
        min_value = num

print(min_value, max_value) #1 5
```

<br><br>

### `sys.maxsize`

: An integer giving the maximum value a variable of type Py_ssize_t can take.

-> It’s usually 2**31 - 1 on a 32-bit platform and 2**63 - 1 on a 64-bit platform.

<br>

```python
import sys
max_num = sys.maxsize
```

<br>

<br>

### `[::-1]`

: Reversing an iterable

<br>

ex)

```python
name = '이효리'
numbers = [1,2,3,4,5]

print('내이름은 이효리 거꾸로 하면', name[::-1]) # 내이름은 이효리 거꾸로 하면 리효이
print('make it reversed!!', numbers[::-1]) # make it reversed!! [5, 4, 3, 2, 1]
```
