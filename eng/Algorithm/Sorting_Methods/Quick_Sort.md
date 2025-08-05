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
