---
title: Divide and Conquer
---
---

# Overview

In `Divide-and-Conquer`, we solve a give problem recursively. If we reach the **base case** (problem is small enough) then solve it directly, no more recusing. Otherwise, we on the **recursive case** we will perform these 3 steps.

1. `Divide` the problem into subproblems (smaller instances of the same problem)
2. `Conquer` the subproblem. Solve them recursively
3. `Combine` the subproblem solutions to form a solution to original problem.

---

Then, How can we analyze the recursive inside Divide-and-Conquer. We need to use mathematic tool call `recurrence`.

## Recurrence

It's an equation that defines a sequence of numbers or values in terms of one or more of its previous terms. 

$$T(n) = T(n/3) + T(2n/3) + Θ(n)$$

### How to solve recurrences

#### Substitution method
Guess the form of a bound and then use mathematic induction to prove that the guess is correct and solve for constants.

1. Guess the form of the solution using symbolic constant
2. Use mathematical induction to show that the solution works, and find the constants.

**Example**
Let find asymptotic upper bound (Big O) on the recurrence
$$T(n) = 2(T(\lfloor n/2\rfloor)+Θ(n)$$
1. Let's guess that the **asymptotic upper bound** is $T(n)=O(n\space lg\space n)$
2. Adopt Inductive hypothesis that$$T(n) \le cn\space lg\space n\space$$ for all $n \ge n_0$ 
3. Assume by induction that this bound hold all numbers at least 
	- Big as big as $n_0$ , less then $n$
	- If $n \ge 2n_0$  then it hold $\lfloor n/2\rfloor$

>If $n \ge 2n_0$ , then $\lfloor n/2\rfloor$, will always give you a result that  $\ge n_0$.

1. Let **substitute** into our hypothesis and then **substitute** into **recurrence**.
$$T(\lfloor n/2\rfloor) \le c\lfloor n/2\rfloor\space lg\space \lfloor n/2\rfloor\space$$
$$T(n) \le 2(c\lfloor n/2\rfloor\space lg\space \lfloor n/2\rfloor) +Θ(n)$$
$$T(n) \le cn\space lg\space n$$

We have demonstrated that the assumption we made for the inductive step is valid. 
#### Recursion-Tree method
Model the tree whose nodes represent the costs incurred at various levels of the recursion.
#### Master method

It will provide bounds for recurrences of the form.
$$T(n) = aT(n/b) + f(n)$$
where $a>0$ , $b>1$

$f(n)$ is time that we divide and combine and algorithm create $a$ subproblems
where $1/b$ times the size of original problems.


# Merge Sort

![[merge-sort-dvq.png | 400]]

# Integer Multiplication

# Counting Inversion