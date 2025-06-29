# Dijkstra Algorithm

<br>

<br>

## 최단 경로

<br>

### 최단 경로 정의

: 간선의 가중치가 있는 그래프에서 두 정점 사이의 경로들 중에 간선의 가중치의 합이 최소인 경로

<br>

### 하나의 시작 정점에서 끝 정점까지의 최단 경로 (one to all)

- #### 다익스트라 (dijkstra) 알고리즘

  - 음의 가중치를 허용하지 않음

- #### 벨만-포드 (Bellman-Ford) 알고리즘

  - 음의 가중치 허용

<br>

### 모든 정점들에 대한 최단 경로

- #### 플로이드-워샬 (Floyd-Warshall) 알고리즘

<br>

<br>

## Dijkstra Algorithm

> 시작 정점에서 거리가 최소인 정점을 선택해 나가면서 최단 경로를 구하는 방식

<br>

- 시작 정점 (s)에서 끝 정점 (t) 까지의 최단 경로에 정점 x가 존재한다
- 이때, 최단 경로는 s에서 x까지의 최단 경로와 x 에서 t 까지의 최단 경로로 구성된다
- **탐욕 (greedy) 기법**을 사용한 알고리즘으로 MST의 `Prim Algorithm`과 유사하다
- 인접 행렬 그래프와 시작 정점이 주어졌을 때, 다익스트라 알고리즘을 사용하면 시작 정점에서 **모든 정점**으로 가는 **최단 거리**를 구할 수 있다

<br>

#### `시간 복잡도`

: O(logN)

<br>

### 구현 해보기

> Dijkstra + 인접리스트

```python
"""
6 11
0 1 3
0 2 5
1 2 2
1 3 6
2 1 1
2 3 4
2 4 6
3 4 2
3 5 3
4 0 3
4 5 6

결과
[0, 3, 5, 9, 11, 12]
"""

# dist, selected 배열 준비
# 시작점 선택
# 모든 정점이 선택될 때 까지
# 아직 선택되지 않고 dist의 값이 최소인 정점 : u
# 정점 u의 최단거리 결정
# 정점 u에 인접한 정점에 대해서 간선 완화

V, E = map(int, input().split())
adj = {i:[] for i in range(V)}

for i in range(E):
    s, e, c = map(int, input().split())
    adj[s].append([e,c]) #방향 그래프라서

INF = float('inf')
dist = [INF]*V
selected = [False]*V

dist[0] = 0
cnt = 0
while cnt <V:
    # dist가 최소인 정점 찾기
    MIN = INF
    for i in range(V):
        if not selected[i] and dist[i] < MIN:
            MIN = dist[i]
            u = i
    # 결정
    selected[u] = True
    cnt += 1

    # 간선 완화
    for w, cost in adj[u]: # 도착정점, 가증치
        if dist[w] > dist[u] + cost:
            dist[w] = dist[u] + cost
    
print(dist) # [0, 3, 5, 9, 11, 12]
```
