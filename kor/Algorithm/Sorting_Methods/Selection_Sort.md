# 선택 정렬 (Selection Sort)

<br>

### Iterative Selection Sort

```python
def SelectionSort(arr):
    N = len(arr)
    for i in range(N-1):
        MIN = i
        for j in range(i+1, N):
            if arr[j] < arr[MIN]:
                MIN = j
        arr[MIN], arr[i] = arr[i], arr[MIN]
```

<br>

### Recursive Selection Sort

```python
def SelectionSort(arr, s):
    N = len(arr)
    if s == N-1:
        return
    MIN = s
    for i in range(s, N):
        if arr[MIN] > arr[i]:
            MIN = i
    arr[s], arr[MIN] = arr[MIN], arr[s]
    SelectionSort(arr, s+1)
```
