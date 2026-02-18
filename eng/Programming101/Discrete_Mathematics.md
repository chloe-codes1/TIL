# Discrete Mathematics

> Mathematics for Computers

<br>

*Discrete Mathematics* provides a common forum for significant research in many areas of **discrete mathematics** and **combinatorics**.

<br>

<br>

## Overview of Discrete Mathematics

> Computer mathematics explored through true and false

<br>

### Why should we learn it?

- Discrete mathematics is mathematics that deals with discontinuous numbers

- Computers internally handle only 0s and 1s, so it is essential coursework for cultivating mathematical thinking suitable for dealing with such discontinuous data flows

- The content covered in discrete mathematics serves as the base for data structures, algorithms, etc., and develops overall Computational Thinking

  <br>

*Discrete mathematics is the foundational discipline of computer science!*

<br>

<br>

## Propositions and Operators

<br>

### Proposition

> Truth or Falsehood

- A sentence whose truth (True) or falsehood (False) can be determined
- A proposition, like computer memory that holds only 0 or 1, always has exactly one of two values: true or false
- Multiple propositions can also be combined
  - **Compound Proposition (`Compound Proposition`)**

<br>

### Logical Operator

> An operator is a tool for performing operations on propositions, and there are 6 basic operators in discrete mathematics

<br>

<img src="../kor/images/image-20200423194638742.png" alt="image-20200423194638742" style="zoom:30%;" />

<br>

<br>

1. `Not`

   - Reverses the truth value (true <-> false) of the following proposition

2. `And`

   - Conjunction

   - Used to combine two propositions
   - True only when both are true
     - False if even one is false

3. `Or`

   - Disjunction

   - True if at least one is true

4. `Exclusive or`

   - Exclusive disjunction
     - Mutually exclusive
   - True only when exactly one is true

5. `Implication`

   - **Conditional Proposition (`Conditional Proposition`)**
     - Under a certain condition, a certain result occurs
       - Used to express the flow based on conditions and results
     - A proposition that has a **cause** proposition and a **result** proposition
   - p -> q
     - The conditional proposition returns False only when p is True and q is False

6. `Biconditional`

   - Biconditional proposition
   - The biconditional proposition returns True only when both values match each other

<br>

<br>

## Converse, Inverse, Contrapositive

<br>

### Truth Table

- A table showing the truth values of the relational expressions between propositions
- No matter how complex a **compound proposition** is, it can be resolved through a truth table!

<br>

![img](http://img.sparknotes.com/figures/8/84ba14d565517459113594f30789b66a/tt4.gif)

<br>

<br>

### Converse, Inverse, Contrapositive

<br>

<img src="../kor/images/image-20200424040719609.png" alt="image-20200424040719609" style="zoom:40%;" />

<br>

- Used in **Conditional Propositions** (`Conditional Proposition`)
- Transforms a single proposition into different expressions
- Helps with proofs
- Propositions that are difficult to prove can be proven using the **contrapositive**
  - Because if the contrapositive of a proposition is true, the original proposition is also true!

<br><br>

## Equivalence

> When two propositions have the same truth values

<br>

### Meaning of Equivalence

- Equivalence means '*logically identical*'
- Used to discover simpler propositions with the same meaning
- There are various types of equivalence laws

<br>

### Proving with Equivalence Laws

> Even complex-looking compound propositions (compositional propositions) can be simplified using equivalence laws!

<br>

<img src="https://www.geeksforgeeks.org/wp-content/ql-cache/quicklatex.com-67ea85d519042c10897afc964c777539_l3.svg" alt="  \begin{tabular}{ ||c||c|| }      \hline     Equivalence &amp; Name of Identity\\     \hline          \hline     p\wedge T \equiv p &amp;  Identity Laws\\     p\vee F \equiv p &amp;  \\     \hline          p\wedge F \equiv F &amp;  Domination Laws\\     p\vee T \equiv T &amp;  \\     \hline          p\wedge p \equiv p &amp;  Idempotent Laws\\     p\vee p \equiv p &amp;  \\     \hline          \neg(\neg p) \equiv p &amp;  Double Negation Law\\     \hline          p\wedge q \equiv q\wedge p &amp;  Commutative Laws\\     p\vee q \equiv q\vee p &amp;  \\     \hline          (p\wedge q) \wedge r\equiv p\wedge (q \wedge r) &amp;  Associative Laws\\     (p\vee q) \vee r\equiv p\vee (q \vee r) &amp;  \\     \hline      p\wedge (q \vee r)\equiv (p\wedge q)\vee (p\wedge r) &amp;  Ditributive Laws\\     p\vee (q \wedge r)\equiv (p\vee q)\wedge (p\vee r) &amp;  \\     \hline          \hline      \neg(p\wedge q) \equiv \neg p \vee \neg q &amp;  De Morgan's Laws\\     \neg(p\vee q) \equiv \neg p \wedge \neg q &amp;  \\     \hline      p\wedge (p \vee q)\equiv p &amp;  Absorption Laws\\     p\vee (p \wedge q)\equiv p &amp;  \\     \hline          p\wedge \neg p \equiv F &amp;  Negation Laws\\     p\vee \neg p \equiv T &amp;  \\     \hline \end{tabular} " style="zoom:150%;" />

<br>

- #### Identity Laws

  - Regardless of whether the comparison target is True/False, it retains the value of p

- #### Domination Laws

  - The result is dominantly determined by the comparison target

- #### De Morgan's Laws

  - When p and q, adding not produces ~p or ~q respectively
  - Conversely, adding not to p or q produces ~p and ~q respectively

- #### Absorption Laws

  - The outer value is so strong that regardless of what is inside the parentheses (), the result is absorbed by the outer value

- #### Negation Laws

  - When one of the two is not, an and operation returns True, and an or operation returns False

- #### Implication Law

  - `p -> q`  <-> `~p or q`

<br>
