# Optimization Problems

Optimization is the process of finding the best possible solution to a problem
according to a given objective while satisfying specified restrictions.

In mathematical optimization, we generally want to:

- maximize a quantity such as profit, output, performance, etc.
- minimize a quantity such as cost, time, distance, error, etc.

---

## 1. General Optimization Problem

A general optimization problem can be written as

$$
\operatorname{optimize} \quad f(x)
$$

subject to

$$
g_i(x) \leq 0,\qquad i=1,2,\ldots,m
$$

$$
h_j(x)=0,\qquad j=1,2,\ldots,p
$$

where

$$
x=(x_1,x_2,\ldots,x_n)^T
$$

is the vector of decision variables.

The function

$$
f(x)
$$

is called the **objective function**.

The functions

$$
g_i(x),h_j(x)
$$

represent the constraints.

---

## 2. Important Terminology

### Decision Variables

The unknown quantities whose values must be determined.

Example:

If a factory produces two products, let

$$
x_1 = \text{number of units of product 1}
$$

$$
x_2 = \text{number of units of product 2}
$$

Then $x_1,x_2$ are decision variables.

---

### Objective Function

The mathematical expression representing what we want to maximize or minimize.

Example:

$$
\max Z = 40x_1+30x_2
$$

Here,

$$
Z=40x_1+30x_2
$$

is the objective function.

---

### Constraints

Restrictions imposed on the decision variables.

Example:

$$
2x_1+x_2\leq100
$$

may represent a limited amount of raw material.

---

### Feasible Solution

A solution satisfying **all constraints** is called a feasible solution.

---

### Feasible Region

The set of all feasible solutions.

---

### Optimal Solution

A feasible solution giving the best value of the objective function is called
an optimal solution.

For a maximization problem:

$$
Z(x^*)\geq Z(x)
$$

for every feasible $x$.

For a minimization problem:

$$
Z(x^*)\leq Z(x)
$$

for every feasible $x$.

---

## 3. Classification of Optimization Problems

Optimization problems can be classified in several ways.

### 3.1 Based on the Objective Function

#### Maximization

$$
\max f(x)
$$

Example:

$$
\max Z=5x_1+3x_2
$$

#### Minimization

$$
\min f(x)
$$

Example:

$$
\min Z=4x_1+7x_2
$$

---

### 3.2 Based on Constraints

#### Unconstrained Optimization

No explicit constraints are present.

$$
\min f(x)
$$

---

#### Constrained Optimization

One or more constraints are present.

$$
\min f(x)
$$

subject to

$$
g_i(x)\leq0
$$

---

### 3.3 Based on Mathematical Structure

#### Linear Optimization

Both the objective function and constraints are linear.

Example:

$$
\max Z=3x_1+5x_2
$$

subject to

$$
2x_1+x_2\leq10
$$

$$
x_1+3x_2\leq15
$$

---

#### Nonlinear Optimization

At least one objective or constraint is nonlinear.

Example:

$$
\min Z=x_1^2+x_2^2
$$

subject to

$$
x_1+x_2\geq1
$$

---

### 3.4 Based on the Variables

#### Continuous Optimization

Variables can take any value in an interval.

Example:

$$
x=2.37
$$

is allowed.

---

#### Integer Optimization

Variables must be integers.

$$
x_i\in\mathbb Z
$$

---

#### Binary Optimization

Variables can take only two values.

$$
x_i\in\{0,1\}
$$

---

## 4. Linear Programming Problem

A Linear Programming Problem (LPP) is an optimization problem in which:

1. the objective function is linear;
2. every constraint is linear;
3. decision variables satisfy specified sign restrictions.

A general LPP can be written as

$$
\max/\min\quad
Z=c_1x_1+c_2x_2+\cdots+c_nx_n
$$

subject to

$$
a_{11}x_1+a_{12}x_2+\cdots+a_{1n}x_n
\leq/\geq/=b_1
$$

$$
a_{21}x_1+a_{22}x_2+\cdots+a_{2n}x_n
\leq/\geq/=b_2
$$

$$
\vdots
$$

$$
a_{m1}x_1+a_{m2}x_2+\cdots+a_{mn}x_n
\leq/\geq/=b_m
$$

with appropriate restrictions on $x_i$.

---

## 5. Assumptions of Linear Programming

### 5.1 Proportionality

The contribution of a variable is proportional to its value.

If one unit of a product gives profit $c$,
then $x$ units give profit

$$
cx.
$$

---

### 5.2 Additivity

The total contribution is the sum of individual contributions.

For example,

$$
Z=5x_1+8x_2
$$

contains no interaction term such as

$$
x_1x_2.
$$

---

### 5.3 Divisibility

Variables are generally allowed to take fractional values unless
integer restrictions are explicitly imposed.

---

### 5.4 Certainty

The coefficients of the LPP are assumed to be known and fixed.

For example,

$$
Z=5x_1+8x_2
$$

assumes the coefficients $5$ and $8$ are known.

---

## 6. Important Special Cases

### Feasible LPP

At least one feasible solution exists.

---

### Infeasible LPP

No solution satisfies all constraints.

---

### Unbounded LPP

The objective function can improve indefinitely without violating
the constraints.

For a maximization problem:

$$
Z\rightarrow+\infty
$$

may occur.

---

### Multiple Optimal Solutions

More than one feasible solution gives the same optimal objective value.

---

### Degenerate Solution

A basic feasible solution is degenerate when one or more basic variables
are zero.

This becomes particularly important when studying the Simplex Method.

---

## 7. Converting a Real-World Problem into an LPP

The general modelling procedure is:

### Step 1 — Identify decision variables

Ask:

> What quantities do I need to determine?

---

### Step 2 — Define the objective

Ask:

> What am I trying to maximize or minimize?

---

### Step 3 — Identify constraints

Ask:

> What resources, requirements, or restrictions limit the variables?

---

### Step 4 — Add sign restrictions

For quantities that cannot be negative:

$$
x_i\geq0
$$

---

### Step 5 — Write the complete LPP

---

# Worked Problem 1 — Product Mix

A company manufactures products $P_1$ and $P_2$.

Each unit of $P_1$ gives a profit of ₹40 and each unit of $P_2$
gives a profit of ₹30.

The available resources impose the following restrictions:

$$
2x_1+x_2\leq100
$$

$$
x_1+x_2\leq80
$$

$$
x_1,x_2\geq0
$$

Formulate the LPP.

---

## Step 1 — Decision Variables

Let

$$
x_1=\text{units of }P_1
$$

$$
x_2=\text{units of }P_2
$$

---

## Step 2 — Objective Function

Profit from $P_1$:

$$
40x_1
$$

Profit from $P_2$:

$$
30x_2
$$

Therefore,

$$
\boxed{\max Z=40x_1+30x_2}
$$

---

## Step 3 — Constraints

The first resource gives

$$
\boxed{2x_1+x_2\leq100}
$$

The second resource gives

$$
\boxed{x_1+x_2\leq80}
$$

---

## Step 4 — Non-negativity

Production quantities cannot be negative:

$$
\boxed{x_1,x_2\geq0}
$$

---

## Final LPP

$$
\boxed{
\begin{aligned}
\max\quad & Z=40x_1+30x_2\\
\text{s.t.}\quad
&2x_1+x_2\leq100\\
&x_1+x_2\leq80\\
&x_1,x_2\geq0
\end{aligned}
}
$$

---

# Worked Problem 2 — Minimization

A diet must contain at least 20 units of nutrient A and
at least 30 units of nutrient B.

Food 1 costs ₹5 per unit and Food 2 costs ₹4 per unit.

One unit of Food 1 provides:

- 4 units of A
- 2 units of B

One unit of Food 2 provides:

- 2 units of A
- 5 units of B

Formulate the LPP.

---

## Step 1 — Variables

Let

$$
x_1=\text{units of Food 1}
$$

$$
x_2=\text{units of Food 2}
$$

---

## Step 2 — Objective

We want to minimize cost:

$$
\boxed{\min Z=5x_1+4x_2}
$$

---

## Step 3 — Nutrient A Constraint

Food 1 contributes $4x_1$.

Food 2 contributes $2x_2$.

At least 20 units are required:

$$
\boxed{4x_1+2x_2\geq20}
$$

---

## Step 4 — Nutrient B Constraint

$$
2x_1+5x_2\geq30
$$

---

## Step 5 — Non-negativity

$$
x_1,x_2\geq0
$$

---

## Final LPP

$$
\boxed{
\begin{aligned}
\min\quad &Z=5x_1+4x_2\\
\text{s.t.}\quad
&4x_1+2x_2\geq20\\
&2x_1+5x_2\geq30\\
&x_1,x_2\geq0
\end{aligned}
}
$$

---

# Exam Checklist

Before considering an LPP formulation complete, verify:

- [ ] Decision variables defined
- [ ] Objective direction identified
- [ ] Objective coefficients correct
- [ ] Every resource/requirement represented
- [ ] Constraint direction correct
- [ ] Non-negativity restrictions included
- [ ] No nonlinear terms accidentally introduced

---

# Quick Revision

| Term | Meaning |
|---|---|
| Decision variable | Unknown quantity to determine |
| Objective function | Quantity to maximize/minimize |
| Constraint | Restriction on variables |
| Feasible solution | Satisfies all constraints |
| Feasible region | Set of all feasible solutions |
| Optimal solution | Best feasible solution |
| LPP | Optimization problem with linear objective and constraints |
| Unbounded | Objective can improve indefinitely |
| Infeasible | No feasible solution exists |
| Degenerate BFS | Basic variable is zero |

---

# Practice Problems

## Problem 1

A factory produces $x_1$ units of product A and $x_2$ units of product B.

Profit per unit is ₹50 and ₹40 respectively.

Resources:

$$
3x_1+2x_2\leq120
$$

$$
x_1+2x_2\leq80
$$

Formulate the LPP.

---

## Problem 2

Minimize

$$
Z=6x_1+8x_2
$$

subject to

$$
2x_1+x_2\geq10
$$

$$
x_1+3x_2\geq12
$$

$$
x_1,x_2\geq0.
$$

Identify:

1. objective function
2. decision variables
3. constraints
4. objective direction

---

## Problem 3

Identify whether each problem is linear or nonlinear.

### (a)

$$
Z=3x_1+4x_2
$$

### (b)

$$
Z=x_1^2+2x_2
$$

### (c)

$$
Z=5x_1+3x_2
$$

subject to

$$
x_1x_2\leq10
$$

### (d)

$$
Z=4x_1+7x_2
$$

subject to

$$
2x_1+3x_2\leq20.
$$

### Answers

- (a) Linear
- (b) Nonlinear
- (c) Nonlinear
- (d) Linear