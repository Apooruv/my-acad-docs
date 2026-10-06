# Big-M Method

The Big-M Method is a technique for solving LPPs that contain
artificial variables.

The main idea is to assign a very large penalty to artificial
variables so that the optimization process forces them out of the
basis.

---

# 1. Why Big-M?

Consider:

$$
\max Z=c^Tx
$$

with a constraint such as

$$
a_1x_1+a_2x_2\geq b.
$$

After conversion:

$$
a_1x_1+a_2x_2-s+a=b.
$$

The artificial variable $a$ must not remain in the final solution.

Big-M assigns a large penalty to $a$.

---

# 2. Big-M for Maximization

For a maximization problem, artificial variables receive a large
negative penalty:

$$
\boxed{-Ma_i}
$$

where

$$
M\gg1.
$$

Therefore:

$$
\max Z
=
c^Tx-M\sum a_i.
$$

The Simplex method naturally attempts to eliminate artificial
variables because keeping them reduces the objective value.

---

# 3. Big-M for Minimization

For a minimization problem, artificial variables receive a large
positive penalty:

$$
\boxed{+Ma_i}.
$$

The minimization process attempts to drive them to zero.

---

# 4. Complete Worked Problem

Solve:

$$
\max Z=3x_1+2x_2
$$

subject to

$$
x_1+x_2\leq4
$$

$$
x_1+2x_2\geq6
$$

$$
x_1,x_2\geq0.
$$

---

## Step 1 — Standard Form

First constraint:

$$
x_1+x_2+s_1=4.
$$

Second constraint:

$$
x_1+2x_2-s_2+a_1=6.
$$

---

## Step 2 — Modify Objective

Original:

$$
Z=3x_1+2x_2.
$$

Since this is a maximization problem:

$$
\boxed{
Z=3x_1+2x_2-Ma_1
}
$$

---

## Step 3 — Initial Basis

The identity-type columns are:

$$
s_1,\quad a_1.
$$

Therefore:

| Basis | $C_B$ |
|---|---:|
| $s_1$ | 0 |
| $a_1$ | $-M$ |

Initial solution:

$$
s_1=4
$$

$$
a_1=6.
$$

The artificial variable is currently positive and must be removed.

---

## Step 4 — Construct Initial Tableau

| $C_B$ | Basis | $x_1$ | $x_2$ | $s_1$ | $s_2$ | $a_1$ | RHS |
|---:|---|---:|---:|---:|---:|---:|---:|
| 0 | $s_1$ | 1 | 1 | 1 | 0 | 0 | 4 |
| $-M$ | $a_1$ | 1 | 2 | 0 | -1 | 1 | 6 |

Now calculate $Z_j$.

For $x_1$:

$$
Z_{x_1}
=
0(1)+(-M)(1)
=-M.
$$

For $x_2$:

$$
Z_{x_2}
=
0(1)+(-M)(2)
=-2M.
$$

For $s_1$:

$$
Z_{s_1}=0.
$$

For $s_2$:

$$
Z_{s_2}=(-M)(-1)=M.
$$

For $a_1$:

$$
Z_{a_1}=-M.
$$

Therefore:

| Variable | $C_j$ | $Z_j$ | $Z_j-C_j$ |
|---|---:|---:|---:|
| $x_1$ | 3 | $-M$ | $-M-3$ |
| $x_2$ | 2 | $-2M$ | $-2M-2$ |
| $s_1$ | 0 | 0 | 0 |
| $s_2$ | 0 | $M$ | $M$ |
| $a_1$ | $-M$ | $-M$ | 0 |

The most negative expression is:

$$
-2M-2.
$$

Therefore:

$$
\boxed{x_2\text{ enters}}.
$$

---

## Step 5 — Ratio Test

Use the $x_2$ column.

Row 1:

$$
\frac{4}{1}=4.
$$

Row 2:

$$
\frac{6}{2}=3.
$$

Minimum positive ratio:

$$
3.
$$

Therefore:

$$
\boxed{a_1\text{ leaves}}.
$$

This is desirable because an artificial variable has left the basis.

---

## Step 6 — Pivot

Pivot element:

$$
2.
$$

Divide row 2 by 2:

$$
\frac12x_1+x_2-\frac12s_2+\frac12a_1=3.
$$

Eliminate $x_2$ from row 1:

$$
R_1\leftarrow R_1-R_2.
$$

This gives:

$$
\frac12x_1+\frac12s_1+\frac12s_2-\frac12a_1=1.
$$

The new basis is:

$$
s_1,x_2.
$$

The artificial variable has left the basis.

Continue Simplex iterations until optimality.

---

# 5. Interpretation of the Final Solution

At the final tableau:

### If every artificial variable is zero

The original LPP is feasible.

### If an artificial variable is positive

The original LPP is infeasible.

Thus:

$$
\boxed{
a_i>0\text{ at optimum}
\Rightarrow
\text{original LPP is infeasible}
}
$$

---

# 6. Big-M Exam Procedure

1. Convert LPP into equality form.
2. Add artificial variables where required.
3. Assign $-M$ to artificial variables in maximization.
4. Assign $+M$ in minimization.
5. Construct the initial tableau.
6. Calculate $Z_j$.
7. Calculate $Z_j-C_j$.
8. Apply the ordinary Simplex procedure.
9. Ensure artificial variables leave the basis.
10. Check that every artificial variable is zero at the end.
11. State the final solution.

---

# Common Mistakes

### Mistake 1

Adding an artificial variable to every constraint.

Wrong.

Artificial variables are introduced only where necessary.

---

### Mistake 2

Using $+M$ for artificial variables in maximization.

For the convention used here:

$$
\boxed{\text{Maximization}\Rightarrow-M}
$$

---

### Mistake 3

Forgetting to check artificial variables at the end.

The final solution is not valid for the original LPP if an artificial
variable remains positive.

---

# Practice Problems

## Problem 1

Solve using Big-M:

$$
\max Z=3x_1+5x_2
$$

subject to

$$
x_1+x_2\leq4
$$

$$
x_1+2x_2\geq6
$$

$$
x_1,x_2\geq0.
$$

---

## Problem 2

Solve:

$$
\max Z=4x_1+3x_2
$$

subject to

$$
x_1+x_2=5
$$

$$
2x_1+x_2\leq8
$$

$$
x_1,x_2\geq0.
$$

---

## Problem 3

Determine whether the following problem is feasible:

$$
\max Z=x_1+x_2
$$

subject to

$$
x_1+x_2\leq2
$$

$$
x_1+x_2\geq5
$$

$$
x_1,x_2\geq0.
$$

Use the Big-M interpretation to justify your answer.