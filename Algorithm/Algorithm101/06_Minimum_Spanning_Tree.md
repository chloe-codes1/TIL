# MST (Minimum Spanning Tree)

<br>

## 최소 신장 트리 (MST)

#### MST Algorithms 의 종류

1. Prim Algorithm - `정점`을 선택
2. KRUSKAL Algorithm - `간선`을 선택램

<br>

#### 그래프에서 최소 비용 문제

1. 모든 정점을 연결하는 간선들의 가중치의 합이 최소가 되는 Tree
2. 두 정점 사이의 최소 비용의 경로 찾기

<br>

#### 신장 트리 (Spanning Tree)

: n개의 정점으로 이루어진 무방향 그래프에서 n개의 정점과 n-1개의 간선으로 이루어진 트리

<br>

#### 최소 신장 트리 (Mininum Spanning Tree)

: 무방향 가중치 그래프에서 신장트리를 구성하는 간선들의 가중치의 합이 최소인 신장트리

<br>

<br>

### MST 표현

> Graph 표현

- 그래프
- 간선들의 배열
- 인접 리스트
- 부모 자식 관계와 가중치에 대한 배열
  - `Tree`로 나타낼 수 있다

<br>

<br>

## Prim Algorithm

- 하나의 `정점`에서 연결된 간선들 중에 **하나씩 선택**하면서 MST를 만들어 가는 방식
  1. 임의의 정점을 하나 선택해서 시작
  2. 선택한 정점과 인접하는 정점들 중의 **최소 비용의 간선**이 존재하는 정점을 선택
  3. 모든 저점이 선택될 때 까지 1,2 과정 반복
- 서로소(상호 배타)인 2개의 집합(2 disjoint-sets) 정보를 유지
  - **트리 정점들 (tree vertices)**
    - MST를 만들기 위해 선택된 정점들
  - **비트리 정점들 (nontree vertices)**
    - 선택 되지 않은 정점들

<br>

ex)

> MST

```python
"""
MST  + 인접행렬

7 11
0 5 60
0 1 32
0 2 31
0 6 51
1 2 21
2 4 46
2 6 25
3 4 34
3 5 18
4 5 40
4 6 51

시작정점 끝정점 가중치

결과
[0, 21, 31, 34, 46, 18, 25]
175
"""

V, E = map(int, input().split())
adj = [[0] * V for _ in range(V)]

for i in range(E):
    s, e, c = map(int, input().split())
    adj[s][e] = c
    adj[e][s] = c # 무방향 그래프라서

# for row in adj:
#     print(row)

# key, p(parent), mst 준비
INF = float('inf')
key = [INF] *V # key는 무한대로 초기화
p = [-1] * V   # p(parent)는 -1로 초기화
mst = [False] * V

# 시작점 선택 : 0번 선택
key[0] = 0
cnt = 0
result = 0
while cnt < V:
    # 아직 mst가 아니고, key가 최소인 정점 선택 : u
    MIN = INF
    u = -1
    for i in range(V):
        if not mst[i] and key[i] <MIN:
            MIN = key[i]
            u = i
    # u를 mst로 선택
    mst[u] = True
    result += MIN
    cnt+=1
    # key 값을 갱신
    # u에 인접하고, 아직 mst가 아닌 정점 w에서 key[w] > u - w 가중치  이면 갱신!
    for w in range(V):
        if adj[u][w] > 0 and not mst[w] and key[w] > adj[u][w]:
            key[w] = adj[u][w]
            p[w] = u

print(key) # [0, 21, 31, 34, 46, 18, 25]
print(p) # [-1, 2, 0, 4, 2, 3, 2]
print(result) # 175
```

<br>

ex)

> Mst - prim algorithm

```python
# Prim Algorithm
# : 하나의 정점에서 연결된 간선들 중에 하나씩 선택 하면서 MST를 만들어 가는 방식

# 우선순위 큐 활용하기 -> 이진힙 -> heapq
import heapq

"""
MST  + 인접행렬

7 11
0 5 60
0 1 32
0 2 31
0 6 51
1 2 21
2 4 46
2 6 25
3 4 34
3 5 18
4 5 40
4 6 51

시작정점 끝정점 가중치

결과
[0, 21, 31, 34, 46, 18, 25]
175
"""

V, E = map(int, input().split())
adj = {i: [] for i in range(V)}
for i in range(E):
    s, e, c = map(int, input().split())
    adj[s].append([e,c])
    adj[e].append([s,c]) #무방향이라서
# print(adj)

# key, mst, 우선순위 큐 준비
INF = float('inf')
key = [INF] * V
mst = [False] * V
pq = []
# 시작 정점 선택 : 0
key[0] = 0
# 큐에 시작 정점을 넣음 => (key, 정점 index) 묶어서 넣기
# 우선순위 큐 => 이진힙 => heapq 라이브러리 사용
heapq.heappush(pq, (0,0)) # heqppush(배열 정보, 어떤 원소 넣을 지) : heap의 구조를 유지하면서 하나의 원소를 넣어줌
                    # 우선순위큐 -> 원소의 첫번째 요소 -> key를 우선순위로
result = 0
while pq:
    # 최소값 찾기
    k, node = heapq.heappop(pq) #내가 갖고있는 heapq에서 최소값을 pop해줌
    if mst[node]: continue # 갱신 할 때 필요했던 정보는 skip하기
    # mst로 선택
    mst[node] = True
    result += k
    # key값 갱신 => key배열 / 큐
    for destination, weight in adj[node]:
        if not mst[destination] and key[destination] > weight:
            key[destination] = weight
            # 큐 갱신 => 새로운 (key, 정점) 삽입 => 필요없는 원소는 skip
            heapq.heappush(pq, (key[destination], destination))

print(result) # 175
```

<br>

<br>

## KRUSKAL Algorithm

: **간선**을 하나씩 선택해서 MST를 찾는 알고리즘

1. 최초, 모든 간선을 `가중치`에 따라 **오름차순**으로 정렬
2. 가중치가 가장 낮은 간선부터 선택하면서 트리를 증가시킴
   - 사이클이 존재하면 다음으로 가중치가 낮은 간선 선택
     - 사이클은 선택하지 않는다!
       - 사이클이 있다는 것은 최단거리로 가는 것이 아니라 돌아서 가는 것을 의미하기 때문
   - 사이클이 존재하는지 확인하는 법
     - 정점의 대표자가 같으면 사이클이 있다는 것!
3. `n-1`개의 간선이 선택될 때 까지 2를 반복

<br>

ex)

> kruskal

```python
"""
예제

7 11
0 5 60
0 1 32
0 2 31
0 6 51
1 2 21
2 4 46
2 6 25
3 4 34
3 5 18
4 5 40
4 6 51

"""

def make_set(x):
    p[x] = x

def find_set(x):
    if p[x] == x:
        return x
    else:
        p[x] = find_set(p[x])
        return p[x]

def union(x,y):
    px = find_set(x)
    py = find_set(y)
    if rank[px] > rank[py]:
        p[py] = px
    else:
        p[px] = py
        if rank[px] == rank[py]:
            rank[py] += 1

V, E = map(int, input().split())
edges = [ list(map(int, input().split()))for _ in range(E)]

# 간선을 간선 가중치를 기준으로 정렬
edges.sort(key=lambda x: x[2]) # () 암에 기준이 들어감

# make_set : 모든 정점에 대해 집합 생성
p = [0] * V
rank = [0] * V
for i in range(V):
    make_set(i)

cnt = 0
result = 0
mst = []
# 모든 간선에 대해서 반복 -> V-1개의 간선이 선택될 때 까지
for i in range(E):
    s, e, c = edges[i][0], edges[i][1], edges[i][2]
    # 사이클이면 skip : 채택하려는 두 정점이 ㅅ로 같은 집합이면 skip  => find_set 이용
    if find_set(s) == find_set(e):
        continue
    # 간선 선택
    result += c
    mst.append(edges[i])
    # => mst에 간선 정보 더하기 / 두 정점을 합친다  => Union
    union(s,e)
    cnt +=1
    if cnt == V-1:
        break

print(result) # 175
print(mst) #[[3, 5, 18], [1, 2, 21], [2, 6, 25], [0, 2, 31], [3, 4, 34], [2, 4, 46]]
```

<br>
