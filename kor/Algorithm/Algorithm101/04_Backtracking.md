# Backtracking

<br>

<br>

## Backtracking 개념

<br>

- 여러 가지 선택지들이 존재하는 상황에서 한가지를 선택
- 선택이 이루어지면 새로운 선택지들의 집합이 생성됨
- 이런 선택을 반복하면서 최종 상태에 도달
  - 올바른 선택을 계속하면 목표 상태(goal state)에 도달한다!

<br>

<br>

## Backtracking과 DFS의 차이

- 어떤 node에서 출발하는 경로가 해결책으로 이어질 것 같지 않으면 더 이상 그 경로를 따라가지 않음으로써 시도의 횟수를 줄임
  - `Prunning (가지치기)`
- DFS가 모든 경로를 추적하는데 비해 Backtacking은 불필요한 경로를 조기에 차단함
- DFS를 하기에는 경우의 수가 너무 많을 때
  - N! 가지의 경우의 수를 가진 문제에 대해 DFS를 하면 처리 불가능하다
- Back Tracking 알고리즘을 적용하면 일반적으로 경우의 수가 줄어들지만, 이 역시 최악의 경우에는 여전히 지수함수 시간 (Exponential Time)을 요하므로 처리 불가능

<br>

- Root node에서 Leaf node 까지의 경로는 해답 후보 (candidate solution)가 되는데, DFS를 하여 그 해답 후보 중에서 해답을 찾을 수 있음
  - but, 이 방법을 사용하면 해답이 될 가능성이 전혀 없는 node의 자식 node (descendant) 들도 모두 검색해야 하므로 비효율적

<br>

<br>

## Backtracking 기법

- 어떤 node의 유망성을 점검한 후에 유망(promising) 하지 않다고 결정되면 그 node의 부모로 되돌아가서 (`backtracking`)  다음 자식 node로 감
- 어떤 node를 방문하였을 때
  - 그 node를 포함한 경로가 해답이 될 수 없으면 그 node는 유망하지 않다고 함
  - 해답이 가능성이 있으명 유망하다고 함

<br>

### 가지치기 (prunning)

: 유망하지 않은 node가 포함된 경로는 더 이상 고려하지 않는다

<br>

<br>

### Backtracking을 이용한 알고리즘의 절차

1. 상태 공간 트리의 DFS (깊이 우선 검색)을 실시한다
2. 각 node가 유망한지를 점검한다
3. 만일 그 node가 유망하지 않으면, 그 node의 부모 node로 돌아가서 검색을 계속한다

<br>

### N-Queen 문제

> SWEA 2806

```python
def backtrack(idx): #idx = 행
    global N, cnt
    # 최종 상태인지 확인하고, 최종상태이면 해
    if idx == N:
        # 다 찾았음 - 해!
        cnt +=1
        return 
    # 해당 상태에서 선택할 수 있는 후보군 생성
    # Node가 유망한지 확인 : 열 / 상향 대각 / 하향 대각 확인
    for i in range(N):
        # if 열이 유망하고, 대각들이 유망
        if not col[i] and not dia_1[idx +i] and not dia_2[N+i-idx-1]:
            # 모든 후보군에 대해서 다음 상태 실행 
            col[i] = 1
            dia_1[idx+i] = 1
            dia_2[N+i-idx-1] = 1
            # 행을 증가시키기
            backtrack(idx+1)
            # 다시 사용한 것을 없애줌
            col[i] = 0
            dia_1[idx+i] = 0
            dia_2[N+i-idx-1] = 0

T = int(input())
for t in range(1, T+1):
    N = int(input())

    # 각 행에는 1개의 Queen만 올 수 있음
    col = [0] * N # 열의 사용 여부를 판단하는 리스트
    # 대각 유망성을 판단할 리스트
    
    # 상향 대각: i와 j의 합이 같음
    dia_1 = [0] * (2*N -1) # (r+c) 로 대각선 번호 매김
    # 하향 대각: i-j 차가 일정
    dia_2 = [0] * (2*N -1) # (N + c -r -1) 로 대각선 번호 매김

    cnt = 0
    backtrack(0)
    print('#{} {}'.format(t,cnt))
```

<br>

### Subset

> 부분집합 구하기

ex)

```python
# {1,2,3,4,5,6,7,8,9,10} 의 powerset 중 원소ㅡ이 값이 10인 부분집합을 모두 출력하시오.

def backtrack(arr, idx, N, selected, sum_num):
    if sum_num > 10:
        return
    if idx == N: 
        # 총합이 10이면 출력
        if sum_num == 10:
            for i in range(N):
                if selected[i]:
                    print(arr[i], end=' ')
            print()
        return

    #현재 index를 선택 했을 경우
    selected[idx] =1
    backtrack(arr, idx+1, N, selected, sum_num + arr[idx])

    #현재 index 를 선택하지 않았을 경우
    selected[idx] = 0
    backtrack(arr, idx+1, N, selected, sum_num )


arr = [1,2,3,4,5,6,7,8,9,10]

backtrack(arr, 0, 10, [0]*10, 0)
```

<br>

<br>

## Space State Tree를 구축하여 문제 해결하기

<br>

### Backtracking을 이용하여 순열 구하기

> 접근 방법은 부분집합 구하는 방법과 유사

<br>

ex)

```python
def backtrack(result, selected, idx, N):
    if idx == N:
        print(result)
        return
    # 사용 가능한 선택지 후보군에 대하여 다음 단계로 진행
    for i in range(N):
        if not selected[i]:
            selected[i] = 1
            result[idx] = i
            backtrack(result, selected, idx+1, N)
            selected[i] = 0

N = 5
backtrack([0]*N, [0]*N, 0, N)
```
