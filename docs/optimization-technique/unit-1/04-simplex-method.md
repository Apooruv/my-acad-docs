# Simplex Method

The Simplex Method is an iterative algebraic method for solving
Linear Programming Problems (LPPs).

It is particularly useful when an LPP contains more than two
decision variables, where the graphical method becomes impractical.

The method moves from one Basic Feasible Solution (BFS) to another,
improving the objective function at every iteration until the
optimality condition is satisfied.

---

## 1. Basic Idea

Consider an LPP in standard equality form:

$$
\max Z=c^Tx
$$

subject to

$$
Ax=b
$$

$$
x\geq0.
$$

The Simplex Method:

1. obtains an initial BFS;
2. evaluates whether it is optimal;
3. selects an entering variable;
4. selects a leaving variable;
5. performs a pivot operation;
6. obtains a new BFS;
7. repeats until the optimum is reached.

---

# 2. Basic Solution

Suppose there are $m$ equations and $n$ variables.

Select $m$ linearly independent columns of $A$.

These variables are called **basic variables**.

The remaining $n-m$ variables are called **non-basic variables**.

Set all non-basic variables equal to zero.

The resulting solution is a **basic solution**.

If all basic variables are non-negative, it is a:

$$
\boxed{\text{Basic Feasible Solution (BFS)}}
$$

---

# 3. Example of a Basic Solution

Consider

$$
x_1+x_2+s_1=4
$$

$$
2x_1+x_2+s_2=5
$$

with

$$
x_1,x_2,s_1,s_2\geq0.
$$

Suppose $x_1,x_2$ are selected as non-basic variables.

Set

$$
x_1=x_2=0.
$$

Then

$$
s_1=4
$$

and

$$
s_2=5.
$$

Therefore,

$$
(x_1,x_2,s_1,s_2)=(0,0,4,5)
$$

is a BFS.

---

# 4. Slack Variables and Initial BFS

For a maximization problem with constraints of the form

$$
Ax\leq b
$$

and

$$
b\geq0,
$$

introducing slack variables gives

$$
Ax+Is=b.
$$

The identity matrix $I$ provides an immediate initial basis.

Therefore, the initial BFS is obtained by setting the original
decision variables to zero.

---

# 5. Simplex Tableau

The standard Simplex tableau contains:

| Basis | $C_B$ | $x_1$ | $x_2$ | $s_1$ | $s_2$ | RHS |
|---|---:|---:|---:|---:|---:|---:|
| $s_1$ | 0 | ... | ... | ... | ... | ... |
| $s_2$ | 0 | ... | ... | ... | ... | ... |
| $Z_j$ | | ... | ... | ... | ... | ... |
| $Z_j-C_j$ | | ... | ... | ... | ... | ... |

where:

- $C_j$ = objective coefficient of variable $j$;
- $C_B$ = objective coefficient of the current basic variable;
- RHS = current value of the basic variable;
- $Z_j$ = contribution associated with the current basis.

---

# 6. Computing $Z_j$

For each column:

$$
\boxed{
Z_j=\sum_i C_{B_i}a_{ij}
}
$$

For the RHS:

$$
\boxed{
Z=\sum_i C_{B_i}b_i
}
$$

Then calculate:

$$
\boxed{
Z_j-C_j
}
$$

---

# 7. Optimality Condition

For the convention

$$
Z_j-C_j
$$

in a maximization problem:

$$
\boxed{
Z_j-C_j\geq0
\quad\text{for all }j
}
$$

indicates optimality.

If at least one value satisfies

$$
Z_j-C_j<0,
$$

the solution can be improved.

Therefore, a negative value identifies a candidate entering variable.

---

# 8. Entering Variable

For a maximization problem using $Z_j-C_j$:

> Select the column with the most negative $Z_j-C_j$.

That variable enters the basis.

For example:

| Variable | $Z_j-C_j$ |
|---|---:|
| $x_1$ | $-4$ |
| $x_2$ | $-7$ |
| $s_1$ | $0$ |
| $s_2$ | $0$ |

The most negative value is:

$$
-7.
$$

Therefore:

$$
\boxed{x_2\text{ enters}}
$$

---

# 9. Leaving Variable

Once the entering column has been selected, determine the
leaving variable using the minimum positive ratio:

$$
\boxed{
\frac{\text{RHS}}{\text{positive entry in entering column}}
}
$$

Ignore:

- zero entries;
- negative entries.

Select the smallest positive ratio.

---

# 10. Why Only Positive Entries?

Suppose the entering variable is increased by $\theta$.

For a row

$$
x_B+a\theta=b,
$$

we have

$$
x_B=b-a\theta.
$$

If

$$
a>0,
$$

increasing $\theta$ eventually makes $x_B=0$.

If

$$
a\leq0,
$$

that variable does not impose an upper bound on $\theta$.

Therefore, only positive entries participate in the ratio test.

---

# 11. Pivot Element

The intersection of:

- entering-variable column;
- leaving-variable row

is the **pivot element**.

The pivot operation transforms the tableau so that:

- the entering variable becomes basic;
- the leaving variable becomes non-basic.

---

# 12. Complete Simplex Algorithm

### Step 1

Convert the LPP into the required standard form.

### Step 2

Construct the initial simplex tableau.

### Step 3

Identify the current basic variables.

### Step 4

Calculate $Z_j$.

### Step 5

Calculate $Z_j-C_j$.

### Step 6

Check optimality.

For maximization:

$$
Z_j-C_j\geq0
$$

for all $j$.

If yes, stop.

### Step 7

Select the most negative $Z_j-C_j$.

This determines the entering variable.

### Step 8

Perform the ratio test.

### Step 9

Select the leaving variable.

### Step 10

Identify the pivot element.

### Step 11

Perform row operations.

### Step 12

Construct the new tableau.

### Step 13

Repeat until optimality is reached.

---

# 13. Worked Problem — Complete Simplex Solution

Solve:

$$
\max Z=3x_1+5x_2
$$

subject to

$$
x_1\leq4
$$

$$
2x_2\leq12
$$

$$
3x_1+2x_2\leq18
$$

$$
x_1,x_2\geq0.
$$

---

## Step 1 — Convert to standard form

Introduce slack variables:

$$
x_1+s_1=4
$$

$$
2x_2+s_2=12
$$

$$
3x_1+2x_2+s_3=18.
$$

Objective:

$$
\max Z=3x_1+5x_2.
$$

---

## Step 2 — Initial Tableau

The initial basis is:

$$
s_1,s_2,s_3.
$$

Their objective coefficients are:

$$
C_B=0,0,0.
$$

| $C_B$ | Basis | $x_1$ | $x_2$ | $s_1$ | $s_2$ | $s_3$ | RHS |
|---:|---|---:|---:|---:|---:|---:|---:|
| 0 | $s_1$ | 1 | 0 | 1 | 0 | 0 | 4 |
| 0 | $s_2$ | 0 | 2 | 0 | 1 | 0 | 12 |
| 0 | $s_3$ | 3 | 2 | 0 | 0 | 1 | 18 |

Since all $C_B=0$:

$$
Z_j=0
$$

for every column.

Therefore:

| Variable | $C_j$ | $Z_j$ | $Z_j-C_j$ |
|---|---:|---:|---:|
| $x_1$ | 3 | 0 | -3 |
| $x_2$ | 5 | 0 | -5 |
| $s_1$ | 0 | 0 | 0 |
| $s_2$ | 0 | 0 | 0 |
| $s_3$ | 0 | 0 | 0 |

---

## Step 3 — Entering Variable

Most negative:

$$
-5.
$$

Therefore:

$$
\boxed{x_2\text{ enters}}
$$

---

## Step 4 — Ratio Test

Use the $x_2$ column.

Row 1:

$$
a_{12}=0
$$

Ignore.

Row 2:

$$
\frac{12}{2}=6
$$

Row 3:

$$
\frac{18}{2}=9
$$

Minimum positive ratio:

$$
6.
$$

Therefore:

$$
\boxed{s_2\text{ leaves}}
$$

Pivot element:

$$
\boxed{2}
$$

---

## Step 5 — Normalize Pivot Row

Current pivot row:

$$
2x_2+s_2=12.
$$

Divide by 2:

$$
x_2+\frac12s_2=6.
$$

---

## Step 6 — Eliminate $x_2$ From Other Rows

Row 1 already contains zero $x_2$.

Row 3:

$$
3x_1+2x_2+s_3=18.
$$

Subtract twice the new pivot row:

$$
3x_1+2x_2+s_3
-
2\left(x_2+\frac12s_2\right)
=18-12.
$$

Therefore:

$$
3x_1-s_2+s_3=6.
$$

The new system is:

$$
x_1+s_1=4
$$

$$
x_2+\frac12s_2=6
$$

$$
3x_1-s_2+s_3=6.
$$

---

## Step 7 — New Basis

The new basis is:

$$
s_1,x_2,s_3.
$$

Their objective coefficients are:

$$
0,5,0.
$$

Compute $Z_j$.

For $x_1$:

$$
Z_{x_1}=0(1)+5(0)+0(3)=0.
$$

For $x_2$:

$$
Z_{x_2}=0(0)+5(1)+0(0)=5.
$$

For $s_1$:

$$
Z_{s_1}=0.
$$

For $s_2$:

$$
Z_{s_2}=0(0)+5\left(\frac12\right)+0(-1)
=\frac52.
$$

For $s_3$:

$$
Z_{s_3}=0.
$$

Therefore:

| Variable | $C_j$ | $Z_j$ | $Z_j-C_j$ |
|---|---:|---:|---:|
| $x_1$ | 3 | 0 | -3 |
| $x_2$ | 5 | 5 | 0 |
| $s_1$ | 0 | 0 | 0 |
| $s_2$ | 0 | 2.5 | 2.5 |
| $s_3$ | 0 | 0 | 0 |

The most negative value is:

$$
-3.
$$

Therefore:

$$
\boxed{x_1\text{ enters}}
$$

---

## Step 8 — Ratio Test

Use the $x_1$ column.

Row 1:

$$
\frac{4}{1}=4.
$$

Row 2:

$$
a_{21}=0
$$

Ignore.

Row 3:

$$
\frac{6}{3}=2.
$$

Minimum positive ratio:

$$
2.
$$

Therefore:

$$
\boxed{s_3\text{ leaves}}
$$

Pivot:

$$
3.
$$

---

## Step 9 — Normalize Pivot Row

Current row:

$$
3x_1-s_2+s_3=6.
$$

Divide by 3:

$$
x_1-\frac13s_2+\frac13s_3=2.
$$

---

## Step 10 — Eliminate $x_1$

Row 1:

$$
x_1+s_1=4.
$$

Subtract the new pivot row:

$$
s_1+\frac13s_2-\frac13s_3=2.
$$

The second row remains:

$$
x_2+\frac12s_2=6.
$$

Therefore:

$$
x_1-\frac13s_2+\frac13s_3=2
$$

$$
x_2+\frac12s_2=6
$$

$$
s_1+\frac13s_2-\frac13s_3=2.
$$

---

## Step 11 — New Basic Variables

The basis is:

$$
s_1,x_2,x_1.
$$

Their objective coefficients are:

$$
0,5,3.
$$

Calculate $Z_j$.

For $x_1$:

$$
Z_{x_1}=3.
$$

For $x_2$:

$$
Z_{x_2}=5.
$$

For $s_1$:

$$
Z_{s_1}=0.
$$

For $s_2$:

$$
Z_{s_2}
=
5\left(\frac12\right)
+
3\left(-\frac13\right)
$$

$$
=\frac52-1
=\frac32.
$$

For $s_3$:

$$
Z_{s_3}
=
3\left(\frac13\right)
=1.
$$

Therefore:

| Variable | $C_j$ | $Z_j$ | $Z_j-C_j$ |
|---|---:|---:|---:|
| $x_1$ | 3 | 3 | 0 |
| $x_2$ | 5 | 5 | 0 |
| $s_1$ | 0 | 0 | 0 |
| $s_2$ | 0 | 1.5 | 1.5 |
| $s_3$ | 0 | 1 | 1 |

All values satisfy:

$$
Z_j-C_j\geq0.
$$

Therefore, the solution is optimal.

---

## Step 12 — Read the Solution

Non-basic variables:

$$
s_2=s_3=0.
$$

Therefore:

$$
x_1=2
$$

and

$$
x_2=6.
$$

Calculate objective:

$$
Z=3(2)+5(6)
$$

$$
=6+30
$$

$$
\boxed{Z_{\max}=36}.
$$

Final answer:

$$
\boxed{x_1=2,\quad x_2=6,\quad Z_{\max}=36}
$$

---

# 14. Important Simplex Cases

## Case 1 — Optimal Solution

For maximization using $Z_j-C_j$:

$$
Z_j-C_j\geq0
$$

for every column.

---

## Case 2 — Multiple Optimal Solutions

At an optimal tableau, if a non-basic variable has

$$
Z_j-C_j=0,
$$

another optimal solution may exist.

---

## Case 3 — Unbounded Solution

If an entering variable is selected but all entries in its column
are non-positive, the ratio test cannot be performed.

Therefore, the objective can improve indefinitely.

The problem is unbounded.

---

## Case 4 — Degeneracy

If the minimum ratio is zero, the resulting BFS is degenerate.

A basic variable becomes zero.

---

## Case 5 — Infeasibility

The ordinary Simplex Method assumes an appropriate initial BFS.

When such a BFS cannot be obtained directly, artificial variables
and methods such as Big-M or Two-Phase are used.

---

# 15. Maximization vs Minimization

Be careful about the convention used.

The above notes use:

$$
Z_j-C_j
$$

for a maximization problem.

Under this convention:

$$
\boxed{
Z_j-C_j\geq0
}
$$

means optimality.

Some textbooks instead use:

$$
C_j-Z_j.
$$

Then the signs and entering-variable rule are reversed.

Always determine which convention your course/tableau uses before
solving a problem.

---

# Exam Procedure

When given a Simplex problem, write these steps explicitly:

1. Convert to standard form.
2. Construct initial tableau.
3. Identify $C_B$.
4. Calculate $Z_j$.
5. Calculate $Z_j-C_j$.
6. Check optimality.
7. Select entering variable.
8. Perform ratio test.
9. Select leaving variable.
10. Identify pivot.
11. Perform row operations.
12. Construct new tableau.
13. Repeat.
14. State the optimal solution.

---

# Quick Formula Sheet

$$
Z_j=\sum_i C_{B_i}a_{ij}
$$

$$
Z=\sum_i C_{B_i}b_i
$$

For the $Z_j-C_j$ convention:

$$
\boxed{\text{Maximization optimum: }Z_j-C_j\geq0}
$$

Entering variable:

$$
\boxed{\text{Most negative }Z_j-C_j}
$$

Ratio test:

$$
\boxed{
\min\left\{
\frac{b_i}{a_{ij}}:a_{ij}>0
\right\}
}
$$

---

# Practice Problems

## Problem 1 — Basic

Solve using Simplex:

$$
\max Z=3x_1+2x_2
$$

subject to

$$
x_1+x_2\leq4
$$

$$
x_1\leq2
$$

$$
x_2\leq3
$$

$$
x_1,x_2\geq0.
$$

---

## Problem 2 — Two Iterations

Solve:

$$
\max Z=5x_1+4x_2
$$

subject to

$$
6x_1+4x_2\leq24
$$

$$
x_1+2x_2\leq6
$$

$$
x_1,x_2\geq0.
$$

Show every tableau.

---

## Problem 3 — Identify Unboundedness

Consider:

$$
\max Z=x_1+x_2
$$

subject to

$$
x_1-x_2\geq2
$$

$$
x_1,x_2\geq0.
$$

Determine whether the problem has a finite optimum.

---

## Problem 4 — Degeneracy

Construct an LPP whose Simplex solution contains a degenerate BFS
and demonstrate how degeneracy occurs during the ratio test.

---

## Problem 5 — Multiple Optima

Solve an LPP in which the final tableau contains a non-basic variable
with

$$
Z_j-C_j=0.
$$

Explain why this indicates the possibility of an alternate optimum.