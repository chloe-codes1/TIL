# Computational Thinking

<br>

### Two Difficult Aspects of Programming

1. Programming language syntax and library usage
2. Logic (**`Hard Logic`**)

<br>

### Soft Logic vs Hard Logic

- In everyday life
  - `Soft Logic` is useful because it is fast
  - Although logically imprecise expressions are used, there is an assumption that everyone already knows what they mean
- Programming uses `Hard Logic`
  - All expressions in programming languages originate from logic
  - Hard Logic is needed to understand the numerous algorithms used

<br>

<br>

## 1. Logic and Proof

<br>

### Proposition

- A statement or sentence whose truth or falsity can be determined

- Expressed as p, q, r ...

  - If p -> q is true, then ~q -> ~p is also true (`Contrapositive`)

- ex)
  - Seoul is the capital of South Korea

  - 1 + 1 = 3

  - If two sides have equal length, then it is an isosceles triangle.

    -> If it is not an isosceles triangle, then no matter which two sides you choose, the lengths of the two sides are different

<br>

### Truth Value

- Expresses true or false
- T, F or 1, 0

<br>

#### Tautology

: A proposition whose truth value is always true

<br>

#### Contradiction

: A proposition whose truth value is always false

<br>

#### Contingent Proposition

- A proposition that is neither a tautology nor a contradiction
- A proposition that varies depending on the situation

<br>

#### Conditional Proposition

- When p and q are propositions, a proposition where p is the condition (or cause) and q is the conclusion (or result)
- `p -> q`  (if p then q)
- False only when p is True and q is False

<br>

#### Biconditional Proposition

- When p and q are propositions, a proposition where both p and q are conditions and conclusions
- `p <-> q`  (if p then q, and if q then p)
- True when p and q have the same truth value

<br>

### Propositional Operations (Connectives)

- #### Negation  `NOT`

  - When p is a proposition, the truth value of the proposition is reversed
  - Denoted as ~p
    - Read as not p or the negation of p

- #### Conjunction  `AND`

  - When p and q are propositions, a proposition that is true only when both p and q are true
  - `p ^ q`
    - p and q

- #### Disjunction  `OR`

  - When p and q are propositions, a proposition that is false only when both p and q are false
  - `p v q`
    - p or q

- #### Exclusive Disjunction  `XOR`

  - When p and q are propositions, a proposition that is true when only one of p or q is true
  - `p ⊕ q`
    - p xor q

<br>

### Operator Precedence

- `~`  >   `v` , `^`   >   `->` , `<->`

<br>

### Proof

- A proof must be expressible as a propositional formula
- Usually the exact propositional formula is not written out, but fundamentally it can be converted into one
- Many misunderstandings about proofs arise from confusing `p -> q` with `p <-> q`

<br>

### Mathematical Induction and Levels of Proof

- Basic form of mathematical induction
  - If `P(1)` is true and `P(n) -> P(n+1)` is true, then `P(n)` is true for all natural numbers n
- Strong form of mathematical induction
  - If `P(1)` is true and `P(1) ^ P(2) ^ ... ^ P(n) ->  P(n+1)` is true (all cases are true), then `P(n)` is true for all natural numbers n

<br>

<br>

### Vacuous Truth (pseudo-proposition) Logic

> *If you're the police chief, then I'm the president!*

<br>

#### F -> () is always true

- If you assume a false proposition is true, then any proposition becomes true
  - ex) If you win the lottery, I'll buy you a car
    - If you don't win the lottery, not buying a car is not a lie, and buying one even without winning is also not a lie
    - By the same principle, if we say 2 is odd, then 5 being even or odd is not false

<br>

#### Only T -> F is definitively false

<br>

<br>

## 2. Numbers and Representation

- Computers represent numbers by collecting bits that can express 0/1
- Using k bits, it is possible to represent from 0 to `2^k -1` (from 1 to `2^k`)
  - In fact, it is not necessarily that range!
  - It depends on the agreed-upon method, but in any case it is possible to represent up to `2^k` different values
    - This is exactly the same process as using k digits in decimal to represent from 0 to `10^k -1`

<br>

### How many bits are needed to represent a value n?

- 2^k -1 >= n must hold

  - That is, `2^k >= n+1`

  - Equivalently, k >= log(n+1)

    ->  Approximately logn bits are needed

  - x = logn and 2^x = n refer to the same thing!

<br>

`+`

#### What is logn

1. The answer to "what power of 2 gives `n`"
2. The answer to "how many bits are needed to represent n"
3. The answer to "starting from 1 and continuously doubling, how many times until you reach n"
4. The answer to "when continuously dividing n by 2, **how many divisions** until you get approximately 1"

<br>

- When `x = logn`, comparing x and **n**, **x** is smaller, and as n grows, they diverge enormously
  - When you want to represent something that changes drastically in a smaller scale, use log!
- The value of a 100-digit decimal number is so large it's unreadable!
- **In computer science, the base of log is always 2**
- The address space of a `32-bit computer` is `2^32` = approximately 4 billion addresses
- ![image-20200427003641554](./../kor/images/image-20200427003641554.png)
  - When we reach the last (1+1+ ...)
    - n/ 2^k = 1
    - n = 2^k
    - k = logn
  - The total number of parentheses is logn
  - So when factoring the entire expression by n, we get `nlogn`

<br>

### Big-O Complexity

![Big O](https://www.daveperrett.com/images/articles/2010-12-07-comp-sci-101-big-o-notation/Time_Complexity.png)

<br>

<br>

### Exercises

1. What is the range of numbers that can be represented with `logn bits` in binary representation?

   - With n bits  ->  2^n values

   - With logn bits  ->  n values

2. If the game of 20 Questions proceeds ideally, how many possible answers can be guessed?

   - Each question can yield 2 possible answers
   - The total number of questions is 20
   - Therefore, the number of possible answers is **2^20**

3. When n is sufficiently large, which value is greater?
   1. `2n`  <  `n^2`
       - When the number is infinitely large, the constant in front of n can be ignored, and the growth rate of n^2 is much greater than n
   2. `2^(n/2)`  <  `sqrt(3^n)`
       - sqrt(3^n) =  3^(n/2)
       - That is, comparing 2^n and 3^n, 3^n is greater
   3. `2^(nlogn)`   >   `n!`
       - Assuming base 2,
       - n^n > n!
   4. `log2^(2n)` < `n*sqrt(n)`
       - 2n <  n*sqrt(n)

4. When x = loga(yz), express x using logarithms with base 2. However, each logarithm function's argument must be a single letter.

   ![](../kor/images/0424_02.jpg)

5. Find the inverse functions of the following functions
   1. f(x) = log(x-3) -5
      - f^-1(x) = 2^(x+5) +3
   2. f(x) = 3 log(x+3) +1
   3. f(x) = 2 x 3^x -1

<br>

<br>

## Sets and Combinatorics

<br>

### Sets

- To prove that **A is a subset of B** for two sets A and B is equivalent to showing that any element of A is contained in B
  - ex) To prove that all multiples of 4 are multiples of 2, it suffices to show that 4k = 2(2k)!
- To prove that two sets A and B are equal, it suffices to prove that A is a subset of B and B is a subset of A

<br>

### Combinations

- Combinatorics generally refers to problems that involve counting the number of cases
- The number of combinations is sometimes expressed using **C**, but the parenthetical notation such as (5 choose 2) = 10 is used more frequently

<br>

<br>

`+`

### Mathematical Induction

> One of the methods of mathematical proof, primarily used to show that a proposition holds for all natural numbers.

Mathematical induction consists of two steps.

First, show that the given proposition holds for 1 (or generally for k).

Next, show that if the proposition holds for any natural number n greater than or equal to 1 (or k), then it also holds for n+1.

Then, by mathematical induction, the given proposition holds for all natural numbers (or all natural numbers greater than or equal to k).

<br>

`+`

### Proof by Contradiction

- When trying to prove a proposition, assume the negation of that proposition is true
- Show that this assumption leads to a contradiction, thereby demonstrating the original proposition is true

<br>

<br>

## Exercises

<br>

![Image from iOS](../kor/images/0424_01.jpg)

<br>

![Image from iOS](../kor/images/0424_02.jpg)

<br>

![Image from iOS](../kor/images/0424_03.jpg)

<br>

<br>

## 4. Basic Formulas

master crm

<br><br>

## 5. Recursion

- Recursion is a function that calls itself
- (Can it ever terminate?)
  - A function has input, and if it calls itself with the same input, it obviously cannot terminate
  - It can terminate with different input!

- A function is something that codes a method to solve a problem

  - It does not solve just a single case of a problem!
    - If properly coded, it must solve all cases of the problem it addresses

- **Mathematical induction** can be used for proof

  1. The problem can be solved when n is 0
  2. If the problem can be solved for n-1, then it can also be solved for n
     - If the above two are true, then it is true that the problem can be solved for all possible n
