# Linear Programming

Linear Programming (LP) is a mathematical technique for finding the
maximum or minimum value of a linear objective function subject to
linear constraints.

---

## 1. General Form of an LPP

A general LPP is

$$
\operatorname{optimize}\quad
Z=\sum_{j=1}^{n}c_jx_j
$$

subject to

$$
\sum_{j=1}^{n}a_{ij}x_j
\leq/\geq/=b_i,
\qquad i=1,2,\ldots,m
$$

and variable restrictions.

For a non-negative LPP:

$$
x_j\geq0,
\qquad j=1,2,\ldots,n.
$$

---

## 2. Matrix Form

An LPP can be represented as

$$
\boxed{
\operatorname{optimize}\quad Z=c^Tx
}
$$

subject to

$$
Ax\leq/\geq/=b
$$

and

$$
x\geq0.
$$

Here:

$$
x=
\begin{bmatrix}
x_1\\
x_2\\
\vdots\\
x_n
\end{bmatrix}
$$

is the decision-variable vector.

$$
c=
\begin{bmatrix}
c_1\\
c_2\\
\vdots\\
c_n
\end{bmatrix}
$$

is the objective coefficient vector.

$$
A=[a_{ij}]
$$

is the coefficient matrix.

$$
b=
\begin{bmatrix}
b_1\\
b_2\\
\vdots\\
b_m
\end{bmatrix}
$$

is the RHS/resource vector.

---

# 3. Types of Constraints

An LPP may contain:

### Less-than-or-equal constraint

$$
a_1x_1+a_2x_2\leq b
$$

### Greater-than-or-equal constraint

$$
a_1x_1+a_2x_2\geq b
$$

### Equality constraint

$$
a_1x_1+a_2x_2=b
$$

The distinction becomes important when converting the LPP into
Simplex standard form.

---

# 4. Graphical Interpretation

For two variables, each linear constraint represents a line
in the $x_1-x_2$ plane.

For example,

$$
x_1+x_2\leq6
$$

has boundary

$$
x_1+x_2=6.
$$

The inequality selects one side of the line.

The intersection of all selected regions is the feasible region.

---

# 5. Feasible Region

A feasible region is the set

$$
F=
\{x: Ax\leq b,\ x\geq0\}
$$

for a maximization problem in the corresponding form.

Every point inside $F$ satisfies all constraints.

---

# 6. Corner-Point Principle

For a linear programming problem with a non-empty bounded feasible
region, an optimal solution occurs at an extreme point
(corner point) of the feasible region.

Therefore, for a two-variable LPP, we can solve the problem by:

1. finding the feasible region;
2. finding its corner points;
3. evaluating the objective function at each corner point;
4. selecting the best value.

This is the basis of the graphical method.

---

# Worked Problem 1 — Graphical Method

Solve:

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

## Step 1 — Identify boundary equations

Constraint 1:

$$
x_1+x_2=4
$$

Constraint 2:

$$
x_1=2
$$

Constraint 3:

$$
x_2=3
$$

and

$$
x_1=0,\qquad x_2=0.
$$

---

## Step 2 — Find feasible corner points

The feasible region has the corner points:

$$
(0,0)
$$

$$
(2,0)
$$

$$
(2,2)
$$

$$
(1,3)
$$

$$
(0,3).
$$

---

## Step 3 — Evaluate the objective

The objective is

$$
Z=3x_1+2x_2.
$$

### At $(0,0)$

$$
Z=0.
$$

### At $(2,0)$

$$
Z=3(2)+2(0)=6.
$$

### At $(2,2)$

$$
Z=3(2)+2(2)=10.
$$

### At $(1,3)$

$$
Z=3(1)+2(3)=9.
$$

### At $(0,3)$

$$
Z=3(0)+2(3)=6.
$$

---

## Step 4 — Select maximum

The largest value is

$$
10.
$$

Therefore,

$$
\boxed{x_1=2,\qquad x_2=2}
$$

and

$$
\boxed{Z_{\max}=10}.
$$

---

# 7. Special Cases in Graphical LP

## 7.1 Unique Optimal Solution

Only one corner point gives the optimum.

---

## 7.2 Multiple Optimal Solutions

An entire edge may give the same objective value.

This happens when the objective function is parallel to
a binding boundary.

---

## 7.3 Unbounded Solution

The feasible region extends indefinitely in a direction in which
the objective can continue improving.

---

## 7.4 Infeasible Problem

The constraints have no common feasible region.

---

## 7.5 Redundant Constraint

A constraint that does not change the feasible region is redundant.

---

# Worked Problem 2 — Minimization

Solve graphically:

$$
\min Z=2x_1+3x_2
$$

subject to

$$
x_1+x_2\geq4
$$

$$
x_1+2x_2\geq6
$$

$$
x_1,x_2\geq0.
$$

---

## Step 1 — Boundary equations

$$
x_1+x_2=4
$$

and

$$
x_1+2x_2=6.
$$

---

## Step 2 — Find their intersection

Subtract the first equation from the second:

$$
x_2=2.
$$

Therefore,

$$
x_1=2.
$$

Intersection:

$$
(2,2).
$$

---

## Step 3 — Find axis intersections

For

$$
x_1+x_2=4,
$$

we have:

$$
(4,0),\qquad(0,4).
$$

For

$$
x_1+2x_2=6,
$$

we have:

$$
(6,0),\qquad(0,3).
$$

After applying the inequality directions, the relevant boundary
points include

$$
(0,4),\qquad(2,2),\qquad(6,0).
$$

---

## Step 4 — Evaluate objective

At $(0,4)$:

$$
Z=2(0)+3(4)=12.
$$

At $(2,2)$:

$$
Z=2(2)+3(2)=10.
$$

At $(6,0)$:

$$
Z=2(6)+3(0)=12.
$$

Therefore,

$$
\boxed{x_1=2,\qquad x_2=2}
$$

and

$$
\boxed{Z_{\min}=10}.
$$

---

# 8. Slack, Surplus and Artificial Variables

These variables are introduced while converting constraints
to equality form for Simplex.

### Slack Variable

For

$$
a_1x_1+a_2x_2\leq b
$$

add $s\geq0$:

$$
a_1x_1+a_2x_2+s=b.
$$

---

### Surplus Variable

For

$$
a_1x_1+a_2x_2\geq b
$$

subtract $s\geq0$:

$$
a_1x_1+a_2x_2-s=b.
$$

---

### Artificial Variable

For constraints where a convenient initial basic variable
cannot be obtained using only slack/surplus variables,
an artificial variable may be introduced.

Artificial variables are handled using methods such as:

- Big-M Method
- Two-Phase Method

These are covered later in Unit I.

---

# 9. Basic Feasible Solution

After converting an LPP into standard equality form,

$$
Ax=b,\qquad x\geq0,
$$

a basic solution is obtained by:

1. selecting a basis;
2. setting non-basic variables to zero;
3. solving for the basic variables.

If all basic variables are non-negative, the solution is a
**Basic Feasible Solution (BFS)**.

---

# 10. Why Simplex Method?

The graphical method is practical only when there are
two variables (and sometimes three).

For larger problems, we need an algebraic method.

The Simplex Method systematically moves from one BFS to another
while improving the objective function.

The process continues until the optimality condition is satisfied.

---

# Exam Checklist

For a graphical LPP:

- [ ] Write objective function
- [ ] Write every constraint
- [ ] Include non-negativity
- [ ] Convert boundaries to equations
- [ ] Plot/find intersections
- [ ] Determine feasible region
- [ ] Identify corner points
- [ ] Evaluate objective at each corner
- [ ] Select maximum/minimum
- [ ] State the final solution clearly

---

# Practice Problems

## Problem 1

Solve graphically:

$$
\max Z=5x_1+4x_2
$$

subject to

$$
x_1+x_2\leq5
$$

$$
2x_1+x_2\leq8
$$

$$
x_1,x_2\geq0.
$$

---

## Problem 2

Solve graphically:

$$
\min Z=3x_1+2x_2
$$

subject to

$$
x_1+x_2\geq4
$$

$$
2x_1+x_2\geq5
$$

$$
x_1,x_2\geq0.
$$

---

## Problem 3

Determine whether the following LPP is feasible:

$$
x_1+x_2\leq2
$$

$$
x_1+x_2\geq5
$$

$$
x_1,x_2\geq0.
$$

---

## Problem 4

Identify the type of solution:

$$
\max Z=x_1+x_2
$$

subject to

$$
x_1+x_2\leq10
$$

$$
x_1,x_2\geq0.
$$

Investigate whether multiple optimal solutions exist.