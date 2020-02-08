# Day 19 - Algorithm (02/03)



### Ground Rules

- 연습은 min(), max(), sort() 없이 해보기
- 최대한 스스로 해보기
- import 사용할 일은 Test Case 파일 입력을 위한 import sys 밖에 없다





## Intermediate

> 이차원 배열이 전부!







> 폴더 전체를 copy 하기

```bash
$ cp -r master-algo/ algo
```

<br/>



> 눈에 안보이는 .git file 삭제해서 git remote  끊기

```bash
$ rm -rf .git
```

<br/>



> 파일 열어서 input 값 넣기

```python
import sys

sys.stdin = open('input.txt')
#.stdin 
# :standard input output
```



<br/>



`구간 합` 문제 중요함!!! (prefix_sum)



<br/>

<br/>



## What is Algorithm?

> Program that solves a problem





###  Computer Science & Programming

 : 현실의 complexity를 computer에 어떻게 옮겨갈 지에 대한 방법론

​		**complexity**   --->   **abstraction**



<br/>



#### Computer Science의 두 가지 중요 개념

1. `Abstraction`

​	: 어떻게 하면 현실의 문제를 요약해서 컴퓨터에 넘겨줄지



2. `Reduction`

​    : 무언가 문제를 구체화 하는 것



<br/>



### Algorithm

= Machine way of thinking

  ( 컴퓨터가 생각하는 방식으로 문제를 구체화 하는 것)



<br/>



### 2D List

: 현실 세계의 문제를 표현하기에 좋음



