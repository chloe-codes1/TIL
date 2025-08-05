# Dijkstra Algorithm

<br>

<br>

## Shortest Path

<br>

### Shortest Path Definition

: Among paths between two vertices in a graph with weighted edges, the path with minimum sum of edge weights

<br>

### Shortest Path from One Starting Vertex to End Vertex (one to all)

- #### Dijkstra Algorithm

  - Does not allow negative weights

- #### Bellman-Ford Algorithm

  - Allows negative weights

<br>

### Shortest Paths for All Vertices

- #### Floyd-Warshall Algorithm

<br>

<br>

## Dijkstra Algorithm

> Method of finding shortest paths by selecting vertices with minimum distance from the starting vertex

<br>

- Vertex x exists in the shortest path from starting vertex (s) to end vertex (t)
- At this time, the shortest path consists of the shortest path from s to x and the shortest path from x to t
- Algorithm using **greedy technique**, similar to `Prim Algorithm` of MST
- Given an adjacency matrix graph and starting vertex, Dijkstra algorithm can find the **shortest distance** from the starting vertex to **all vertices**

<br>

#### `Time Complexity`

: O(logN)

<br>

### Implementation

> Dijkstra + adjacency list

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

Result
[0, 3, 5, 9, 11, 12]
"""

# Prepare dist, selected arrays
# Select starting point
# Until all vertices are selected
# Vertex not yet selected with minimum dist value: u
# Determine shortest distance of vertex u
# Edge relaxation for vertices adjacent to vertex u

V, E = map(int, input().split())
adj = {i:[] for i in range(V)}

for i in range(E):
    s, e, c = map(int, input().split())
    adj[s].append([e,c]) # Because it's directed graph

INF = float('inf')
dist = [INF]*V
selected = [False]*V

dist[0] = 0
cnt = 0
while cnt <V:
    # Find vertex with minimum dist
    MIN = INF
    for i in range(V):
        if not selected[i] and dist[i] < MIN:
            MIN = dist[i]
            u = i
    # Decision
    selected[u] = True
    cnt += 1

    # Edge relaxation
    for w, cost in adj[u]: # destination vertex, weight
        if dist[w] > dist[u] + cost:
            dist[w] = dist[u] + cost
    
print(dist) # [0, 3, 5, 9, 11, 12]
``` 
