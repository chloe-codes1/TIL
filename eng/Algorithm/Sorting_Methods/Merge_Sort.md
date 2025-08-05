# Merge Sort

> A method of merging multiple sorted data sets into one sorted set

<br>

*Most efficient method for linked lists!*

<br>

### Utilizing Divide and Conquer Algorithm

- Divide data into minimum unit problems, then sort in order to get final results
  - `top-down` approach

<br>

### Time Complexity

- O(n log n)

<br>

### Merge Sort Process

1. Divide Phase
   - Continue dividing the entire data set until it becomes minimum-sized subsets
2. Merge Phase
   - Sort and merge two subsets into one set

<br>

### Divide Process Algorithm

```python
def merge_sort(m):
    if len(m) <= 1: # Return immediately if size is 0 or 1
        return m
    
    # 1. Divide part
    mid = len(m)//2
    left = m[:mid]
    right = m[mid:]
    
    # Recursively call merge_sort until list size becomes 1
    left = merge_sort(left)
    right = merge_sort(right)
    
    # 2. Conquer part: Merge divided lists
    return merge(left, right)
```

<br>

### Merge Process Algorithm

```python
def merge(left, right):
    result = [] # Merge two divided lists to create result
    
    while len(left) > 0 and len(right) >0: # When elements remain in both lists
        # Compare first elements of two sub lists and add smaller ones to result first
        if left[0] <= right[0]:
            result.append(left.pop(0))
        else:
            result.append(right.pop(0))
    if len(left) > 0: # When elements remain in left list
        result.extend(left)
    if len(right) > 0: # When elements remain in right list
        result.extend(right)
    return result
``` 
