# Brute-Force

<br>

<br>

## Brute-force

- Brute-force is a simple and straightforward approach to problem solving
  - *Just-do-it*
  - The meaning of `force` refers to computer force rather than human intelligence
- The brute-force method is applicable to most problems
- It allows relatively quick problem solving (algorithm design)
- Useful when the size of data (elements, instances) included in the problem is small
- Used as a measure to judge algorithm efficiency for academic or educational purposes

<br>

<br>

## Brute-force Search (Sequential Search)

: To find a key value in a list of data, start comparing from the first data and proceed

<br>

- Results
  - Successful search
  - Failed search

<br>

- Since all possible cases are generated and tested, the execution speed is slow, but the probability of not finding an answer is small
  - Complete search involves writing a program that gets answers simply and quickly by making the input size small
- Based on this, efficient algorithms can be found using `greedy techniques` or `dynamic programming`
- When solving problems in coding tests, it's advisable to first approach with complete search to derive answers, then use other algorithms for performance improvement and verify the answers

<br>

<br>

### Baby-gin Game

#### Description

- When 6 cards are randomly drawn from number cards between 0-9, a case where 3 cards have consecutive numbers is called a run, and a case where 3 cards have the same number is called a triplet.
- When 6 cards consist only of runs and triplets, it's called baby-gin
- Write a program that takes a 6-digit number as input and determines whether it's baby-gin.

<br>

### Complete Search Approach for Baby-gin

1. Generate all possible cases
   - All number arrangements that can be made with 6 numbers (including duplicates)
2. Test the solution
   - Cut the first 3 digits and last 3 digits, test for run and triplet, and finally determine baby-gin

<br>

<br>

## Complete Search

- Many types of problems involve finding cases or elements that satisfy specific conditions
- Typically associated with **combinatorial problems** such as `permutations`, `combinations`, and `subsets`
- Complete search is a brute-force method for combinatorial problems

<br>

<br>

## Permutation

- Arranging some items selected from different things in a row
- The permutation of selecting r items from n different items is nPr
- The following formula holds:
  - nPr = n x (n-1) x (n-2) x ... x (n-r+1)
- nPn = n! is written as `Factorial`
  - n! = n x (n-1) x (n-2) x ... 2x1
- Permutations are related to finding the best method in a set of ordered elements
  - ex) TSP (Traveling Salesman Problem)
- For N elements, there are n! permutations
  - When n >12, time complexity explosion!!! (because it goes up exponentially...)

<br>

### 1. Permutation Generation Through Recursive Calls - Generation Through Exchange

```python
def perm(n,k):
    if k == n:
        #do something
 else:
        for i in range(k, n):
            swap(k,i)#swap!
            perm(n, k+1)
            swap(k,i) #restore to original state
```

<br>

<br>

## Subsets

- Selecting elements included in a set
- Many important algorithms involve finding the optimal subset from a group of elements
  - ex) knapsack problem
- Set containing N elements
  - The number of all power sets including itself and the empty set is 2^n
  - As the number of elements increases, the number of subsets increases exponentially

<br>

### 1. Simple Method to Generate All Subsets

- Finding the `power set` for a set containing 4 elements

<br>

### 2. Binary Counting

- Use N bit strings corresponding to the number of elements
- If the nth bit value is 1, it means the nth element is included

<br>

<br>

## Combination

> Selecting r items from n different elements without considering order

- Combination formula
  - nCr = `n-1 C r-1` +`n-1 C r`
  - nC0 = 1
