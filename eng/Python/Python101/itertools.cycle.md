# itertools.cycle - Infinite Iterator

<br>
<br>

### cycle(iterable)

: You can create an infinitely repeating iterator using `itertools.cycle`, and keep requesting values by calling `next`

<br>

ex)

```python
from itertools import cycle

dinner_menus = cycle(["biscuits and gravy", "corn dog", "grits"])

for _ in range(10):
    print(next(dinner_menus))
```

<br>

Result

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
