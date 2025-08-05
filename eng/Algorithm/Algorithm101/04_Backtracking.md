# Backtracking

<br>

<br>

## Backtracking Concept

<br>

- Select one option when multiple choices exist
- When a choice is made, a new set of choices is generated
- Continue making choices until reaching a final state
  - If you keep making correct choices, you reach the goal state!

<br>

<br>

## Difference between Backtracking and DFS

- Reduce the number of attempts by not following a path if it seems unlikely to lead to a solution
  - `Prunning`
- While DFS tracks all paths, Backtracking cuts off unnecessary paths early
- When there are too many cases for DFS
  - DFS on problems with N! cases becomes unprocessable
- Applying Back Tracking algorithm generally reduces the number of cases, but in worst case scenarios, it still requires exponential time, making it unprocessable

<br>

- The path from root node to leaf node becomes a candidate solution, and we can find the answer among these candidates using DFS
  - However, this method is inefficient because it searches all descendant nodes of nodes that have no possibility of being solutions

<br>

<br>

## Backtracking Technique

- After checking the promisingess of a node, if it's determined to be unpromising, backtrack to the parent node and move to the next child node
- When visiting a node:
  - If the path including that node cannot be a solution, the node is unpromising
  - If there's a possibility for a solution, it's promising

<br>

### Prunning

: No longer consider paths that include unpromising nodes

<br>

<br>

### Backtracking Algorithm Procedure

1. Perform DFS (Depth-First Search) on the state space tree
2. Check if each node is promising
3. If the node is unpromising, return to its parent node and continue searching

<br>

### N-Queen Problem

> SWEA 2806

```python
def backtrack(idx): #idx = row
    global N, cnt
    # Check if it's the final state, if so, it's a solution
    if idx == N:
        # Found it all - solution!
        cnt +=1
        return 
    # Generate candidates to choose from in this state
    # Check if Node is promising : check column / upward diagonal / downward diagonal
    for i in range(N):
        # if column is promising and diagonals are promising
        if not col[i] and not dia_1[idx +i] and not dia_2[N+i-idx-1]:
            # Execute next state for all candidates
            col[i] = 1
            dia_1[idx+i] = 1
            dia_2[N+i-idx-1] = 1
            # Increase row
            backtrack(idx+1)
            # Remove what was used
            col[i] = 0
            dia_1[idx+i] = 0
            dia_2[N+i-idx-1] = 0

T = int(input())
for t in range(1, T+1):
    N = int(input())

    # Only 1 Queen can be placed in each row
    col = [0] * N # List to check column usage
    # Lists to check diagonal promising
    
    # Upward diagonal: sum of i and j is the same
    dia_1 = [0] * (2*N -1) # Number diagonals by (r+c)
    # Downward diagonal: difference between i-j is constant
    dia_2 = [0] * (2*N -1) # Number diagonals by (N + c -r -1)

    cnt = 0
    backtrack(0)
    print('#{} {}'.format(t,cnt))
```

<br>

### Subset

> Finding subsets

ex)

```python
# Print all subsets of {1,2,3,4,5,6,7,8,9,10} powerset where sum of elements is 10.

def backtrack(arr, idx, N, selected, sum_num):
    if sum_num > 10:
        return
    if idx == N: 
        # Print if total sum is 10
        if sum_num == 10:
            for i in range(N):
                if selected[i]:
                    print(arr[i], end=' ')
            print()
        return

    #When current index is selected
    selected[idx] =1
    backtrack(arr, idx+1, N, selected, sum_num + arr[idx])

    #When current index is not selected
    selected[idx] = 0
    backtrack(arr, idx+1, N, selected, sum_num )


arr = [1,2,3,4,5,6,7,8,9,10]

backtrack(arr, 0, 10, [0]*10, 0)
```

<br>

<br>

## Solving Problems by Building Space State Tree

<br>

### Finding Permutations using Backtracking

> The approach is similar to finding subsets

<br>

ex)

```python
def backtrack(result, selected, idx, N):
    if idx == N:
        print(result)
        return
    # Proceed to next step for available choice candidates
    for i in range(N):
        if not selected[i]:
            selected[i] = 1
            result[idx] = i
            backtrack(result, selected, idx+1, N)
            selected[i] = 0

N = 5
backtrack([0]*N, [0]*N, 0, N)
``` 
