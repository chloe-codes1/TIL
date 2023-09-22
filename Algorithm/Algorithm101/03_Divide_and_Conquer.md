# Divide and Conquer

<br>

- 분할 (Divide)
  - 해결할 문제를 여러 개의 작은 부분으로 나눈다.
- 정복 (Conquer)
  - 나눈 작은 문제를 각각 해결한다
- 통합 (Combine)
  - (필요하다면) 해결된 답을 모은다

<br>

#### Top-down Approach (하향식 접근법)

: 분할 정복은 하향식 접근법이다

<br>

<br>

### 거듭제곱

<br>

- 반복 (Iterative) 알고리즘: `O(n)`
  - C의 거듭제곱 = 1에 거듭제곱할 값만큼 C를 곱하는 방식으로 연산 수행
- 분할 정복 기반 알고리즘: `O(logn)
  - 거듭제곱을 반 씩 나누어서 곱해 나가는 방법으로 풀이
  - 지수가 1이 되면 밑 수를 그대로 반환
    - 시간 복잡도를 `O(log n)` 으로 줄일 수 있음!

<br>

<br>

## 병합 정렬 (Merge Sort)

- 여러 개의 정렬된 자료의 집합을 병합하여 한 개의 정렬된 집합으로 만드는 방식
- 분할 정복 알고리즘 활용
  - 자료를 최소 단위의 문제까지 나눈 후에 차례로 정렬하여 최종 결과를 얻어냄
  - **top-down** 방식
- 시간 복잡도
  - O(nlogn)

<br>

ex)

```python
def merge(left, right):
    result = [] # 두 개의 분할된 list를 병합하여 result를 만듦

    while len(left) > 0 and len(right) > 0: # 양쪽 list에 원소가 남아있는 경우

        # 두 sub list의 첫 원소들을 비교하여 작은 것부터 result에 추가함
        if left[0] <= right[0]:
            result.append(left.pop(0))
        else:
            result.append(right.pop(0))

    if len(left) > 0: # 왼쪽 list에 원소가 남아있는 경우
        result.extend(left)
    if len(right) > 0: # 오른쪽 list에 원소가 남아있는 경우
        result.extend(right)
    return result


def merge_sort(m):
    if len(m) <= 1: # 배열 크기가 0 이거나 1인 경우 바로 return
        return m

    # 1. Divide 부분
    mid = len(m) // 2
    left = m[:mid]
    right = m[mid:]

    # list의 크기가 1이 될 때까지 merge_sort() 재귀 호출
    left = merge_sort(left)
    right = merge_sort(right)

    # 2. Conquer 부분 : 분할된 리스트들 병함
    return merge(left, right)
```

<br>

<br>

## 퀵 정렬 (Quick Sort)

- 주어진 배열을 두 개로 분할하고, 각각을 정렬한다
- 병합 정렬과 다른 점
  1. 병합 정렬은 그냥 두 부분으로 나누는 반면에, 퀵 정렬은 분할할 때, 기준 아이템(pivot item) 중심으로, 이보다 작은 것은 왼편, 큰 것은 오른편에 위치시킨다
  2. 각 부분 정렬이 끝난 후, 병합정렬을 "병합"이란 후처리 작업이 필요하나, 퀵 정렬은 필요로 하지 않는다.
- 시간 복잡도
  - nlogn

<br>

### Hoare-Partition 알고리즘

#### 아이디어

- P(pivot) 값들 보다 큰 값은 오른쪽, 작은 값들은 왼쪽 집합에 위치하도록 한다
- Pivot을 두 집합의 가운데에 위치시킨다

<br>

#### 피봇 선택

- 왼쪽 끝 / 오른쪽 끝 / 임의의 세 개 값 중에 중간 값

<br>

ex)

```python
def quick_sort (arr, left, right):
    # pivot 위치 결정 (pivot을 기준으로 큰 값은 오른쪽, 작은 값은 왼쪽으로 구분)
    # 왼쪽 부분집합 정렬
    # 오른쪽 부분집합 정렬
    if left > right:
        return
    # 피봇 구하기
    pivot = lomuto_partition(arr, left, right)
    pivot = hoare_partition(arr, left, right)
    # 왼쪽 부분집합 정렬 실행
    quick_sort(arr, left, pivot-1)
    # 오르쪽 부분집합 정렬 실행
    quick_sort(arr,pivot+1, right)

def lomuto_partition(arr, left, right):
    # 맨 오른쪽 요소를 pivot으로 설정하고,
    # i = left -1
    # j = left
    pivot = arr[right]
    i = left -1

    for j in range(left, right):
        # arr[i] 가 pivot보다 작으면,
        if arr[j] < pivot:
            # i를 1 증가
            # arr[j], arr[i] 위치 교환
            i += 1
            arr[i], arr[j] = arr[j], arr[i]

    # i가 가리키는 위치가 pivot보다 작은 값의 마지막 인덱스
    # i + 1 의 위치에 pivot을 두고 i+1 반환
    arr[i+1], arr[right] = arr[right], arr[i+1]
    
    return i+1

def hoare_partition(arr, left, right):
    # i, j 설정하고, 큰값 & 작은 값 찾아서 위치 바꿔주기
    i = left
    j = right
    pivot = arr[left]

    # i가 j보다 작을 때 까지 게속해서 반복
    while i <= j:
        # pivot 보다 큰 값이 나올 때 까지 i 증가
        while i<=j and arr[i] <= pivot:
            i += 1
        # pivot 보다 작은 값이 나올 때 까지 j 감소
        while i <=j and arr[j] >= pivot:
            j -= 1
        
        # i가 j보다 작으면, 위치 교환
        if i < j:
            arr[i], arr[j] = arr[j], arr[i]
    
    arr[left], arr[j] = arr[j], arr[left]
    return j # pivot 위치인 j 반환

arr = [4,6,3,6,8,0,3,8,10]
quick_sort(arr, 0, len(arr)-1)
print(arr)
```

<br>

<br>

## 이진 검색 (Binary Search)

- 자료의 가운데에 있는 항목의 key 값과 비교하여 다음 검색의 위치를 결정하고 검색을 계속 진행하는 방법
  - 목적 키를 찾을 때까지 이진 검색을 순환적으로 반복 수행함으로써 검색 범위를 반으로 줄여가면서 보다 빠르게 검색을 수행함
- 이진 검색을 하기 위해서는 자료가 **정렬된** 상태여야 한다.

<br>

### 검색 과정

1. 자료의 중앙에 있는 원소를 고른다
2. 중앙 원소의 값과 찾고자 하는 목표 값을 비교
3. 목표 값이 중앙 원소의 값보다
   - 작으면 자료의 왼쪽 반에 대해서 새로 검색을 수행
   - 크다면 자료의 오른쪽 반에 대해서 새로 검색을 수행

4. 찾고자 하는 값을 찾을 때까지 1~3 반복
