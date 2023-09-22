# 병합 정렬 (Merge Sort)

> 여러 개의 정렬된 자료의 집합을 병합하여 한 개의 정렬된 집합으로 만드는 방식

<br>

*연결 list의 경우 가장 효율적인 방식!*

<br>

### 분할 정복 알고리즘 활용

- 자료를 최소 단위의 문제까지 나눈 후에 차례대로 정렬하여 최종 결과를 얻어냄
  - `top-down` 방식

<br>

### 시간 복잡도

- O(n log n)

<br>

### 병합 정렬의 과정

1. 분할 단계
   - 전체 자료 집합에 대하여, 최소 크기의 부분집합이 될 때까지 분할 작업을 계속함
2. 병합 단계
   - 2개의 부분집합을 정렬하면서 하나의 집합으로 병합

<br>

### 분할 과정의 알고리즘

```python
def merge_sort(m):
    if len(m) <= 1: #size가 0이거나 1인 경우 바로 return
        return m
    
    # 1. Divide 부분
    mid = len(m)//2
    left = m[:mid]
    right = m[mid:]
    
    #list의 크기가 1이 될 때까지 merge_sort 재귀 호출
    left = merge_sort(left)
    right = merge_sort(right)
    
    # 2. Conquer 부분: 분할된 list들 병합
    ruturn merge(left, right)
```

<br>

### 병합 과정의 알고리즘

```python
def merge(left, right):
    result = [] #두 개의 분할된 list를 병합하여 result를 만듦
    
    while len(left) > 0 and len(right) >0: #양쪽 list에 원소가 남아있는 경우
        #두 sub list의 첫 원소들을 비교하여 작은 것부터 result에 추가함
        if left[0] <= right[0]:
            result.append(left.pop(0))
        else:
            result.append(right.pop(0))
    if len(left) > 0: #왼쪽 list에 원소가 남아있는 경우
        result.extend(left)
    if len(right) > 0: #오른쪽 list에 원소가 남아있는 경우
        result.extend(right)
    return result
```
