# Divide and Conquer

<br>

- Divide
  - Divide the problem to solve into several small parts.
- Conquer
  - Solve each small divided problem
- Combine
  - (If necessary) collect the solved answers

<br>

#### Top-down Approach

: Divide and conquer is a top-down approach

<br>

<br>

### Exponentiation

<br>

- Iterative algorithm: `O(n)`
  - C to the power = multiply C by the value to be raised to the power starting from 1
- Divide and conquer based algorithm: `O(logn)`
  - Solve by dividing the exponent in half and multiplying
  - When the exponent becomes 1, return the base directly
    - Time complexity can be reduced to `O(log n)`!

<br>

<br>

## Merge Sort

- A method of merging multiple sorted data sets into one sorted set
- Utilizing divide and conquer algorithms
  - Divide data into minimum unit problems, then sort in order to get final results
  - **top-down** approach
- Time complexity
  - O(nlogn)

<br>

Example)

```python
def merge(left, right):
    result = [] # Merge two divided lists to create result

    while len(left) > 0 and len(right) > 0: # When elements remain in both lists

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


def merge_sort(m):
    if len(m) <= 1: # Return immediately if array size is 0 or 1
        return m

    # 1. Divide part
    mid = len(m) // 2
    left = m[:mid]
    right = m[mid:]

    # Recursively call merge_sort() until list size becomes 1
    left = merge_sort(left)
    right = merge_sort(right)

    # 2. Conquer part: Merge divided lists
    return merge(left, right)
```

<br>

<br>

## Quick Sort

- Divide the given array into two and sort each
- Differences from merge sort
  1. While merge sort just divides into two parts, quick sort positions items smaller than the pivot item on the left and larger items on the right when dividing
  2. After each part is sorted, merge sort requires "merging" post-processing work, but quick sort does not require it.
- Time complexity
  - nlogn

<br>

### Hoare-Partition Algorithm

#### Idea

- Position values larger than P(pivot) in the right set and smaller values in the left set
- Position the pivot in the middle of the two sets

<br>

#### Pivot Selection

- Left end / Right end / Middle value among three arbitrary values

<br>

Example)

```python
def quick_sort (arr, left, right):
    # Determine pivot position (separate large values to right, small values to left based on pivot)
    # Sort left subset
    # Sort right subset
    if left > right:
        return
    # Get pivot
    pivot = lomuto_partition(arr, left, right)
    pivot = hoare_partition(arr, left, right)
    # Execute left subset sorting
    quick_sort(arr, left, pivot-1)
    # Execute right subset sorting
    quick_sort(arr,pivot+1, right)

def lomuto_partition(arr, left, right):
    # Set rightmost element as pivot,
    # i = left -1
    # j = left
    pivot = arr[right]
    i = left -1

    for j in range(left, right):
        # If arr[i] is smaller than pivot,
        if arr[j] < pivot:
            # Increase i by 1
            # Swap positions of arr[j], arr[i]
            i += 1
            arr[i], arr[j] = arr[j], arr[i]

    # Position i points to is the last index of values smaller than pivot
    # Place pivot at position i + 1 and return i+1
    arr[i+1], arr[right] = arr[right], arr[i+1]
    
    return i+1

def hoare_partition(arr, left, right):
    # Set i, j and find large & small values to swap positions
    i = left
    j = right
    pivot = arr[left]

    # Continue repeating until i is smaller than j
    while i <= j:
        # Increase i until value larger than pivot appears
        while i<=j and arr[i] <= pivot:
            i += 1
        # Decrease j until value smaller than pivot appears
        while i <=j and arr[j] >= pivot:
            j -= 1
        
        # If i is smaller than j, swap positions
        if i < j:
            arr[i], arr[j] = arr[j], arr[i]
    
    arr[left], arr[j] = arr[j], arr[left]
    return j # Return j which is pivot position

arr = [4,6,3,6,8,0,3,8,10]
quick_sort(arr, 0, len(arr)-1)
print(arr)
```

<br>

<br>

## Binary Search

- A method of determining the next search position by comparing with the key value of the item in the middle of the data and continuing the search
  - By recursively repeating binary search until the target key is found, the search range is halved to perform faster searches
- For binary search, the data must be in a **sorted** state.

<br>

### Search Process

1. Select the element in the center of the data
2. Compare the value of the central element with the target value to find
3. If the target value is compared to the central element value
   - If smaller, perform new search on the left half of the data
   - If larger, perform new search on the right half of the data 
