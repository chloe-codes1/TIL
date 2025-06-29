# itertools.cycle - 무한 반복자

<br>
<br>

### cycle(iterable)

: `itertools.cycle`을 활용하여 무한히 반복되는 iterator를 만들 수 있으며, `next`를 호출하여 계속 요청할 수 있다

<br>

ex)

```python
from itertools import cycle

dinner_menus = cycle(["biscuits and gravy", "corn dog", "grits"])

for _ in range(10):
    print(next(dinner_menus))
```

<br>

결과

```
biscuits and gravy
corn dog
grits
biscuits and gravy
corn dog
grits
biscuits and gravy
corn dog
grits
biscuits and gravy
```
