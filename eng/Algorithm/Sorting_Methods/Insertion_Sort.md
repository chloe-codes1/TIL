# Insertion Sort

<br>

### Sorting Process

- Assume the data to be sorted consists of two subsets S and U
  1. `Subset S` : Sorted elements in the front part
  2. `Subset U` : Remaining elements not yet sorted
- Take elements one by one from the unsorted subset U and compare them starting from the last element of the already sorted subset S to find the position to insert.
- By repeating insertion sort, the elements of subset S increase one by one and the elements of subset U decrease one by one.
- When subset U becomes empty, insertion sort is complete

<br>

### Time Complexity

- O (n ^ 2)
  - Because we need to compare elements of each subset every time!

<br>

### Iterative Selection Sort

```python
arr = [69, 10, 30, 2, 16, 8, 31, 22]
N = len(arr)

for i in range(1,N):  # 1 ~ N-1
    tmp = arr[i]
    print(arr[:i], arr[i:])
    j = i -1
    while j >= 0 and arr[j] > tmp:
        arr[j+1] = arr[j]
        j -= 1
    arr[j+1] = tmp

print(arr)
``` 
