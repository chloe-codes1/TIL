# Day 1 -Introduction

<br/>

## 1-1 Why Study Algorithms?

- important for all other branches of computer science
- plays a key role in modern technological innovation
- provides novel "lens" on processes outside of CS & technology
- challenging!

<br/>

## 1-2 Integer Multiplication

> How this course works

   : Define a computational problem & give solution

#### The Grade-School Algorithm

ex)

```python
  5678
x 1234
_______

```

Up-shot

: number of operations grows n<sup>2</sup>

​     -> As an algorithm designer, we should keep ask ourselves

​     "*CAN WE DO BETTER?*"

<br/>

## 1-3 Karatsuba Multiplication

ex)

```
x = 5678
y = 1234

-> a = 56, b = 78, c = 12, d =24

Step1: compute a*c = 671
Step2: compute b*d = 2652(
Step3: compute (a+b)(c+d) = 6164
Step4: compute (3) -(2) -(1)
```

#### <br/>

### A Recursive Algorithm

> invokes themselves with a sub routine

  -> needs a base case

<br/>

### Karatsuba Multiplication

```
Recall: x*y = 
```
