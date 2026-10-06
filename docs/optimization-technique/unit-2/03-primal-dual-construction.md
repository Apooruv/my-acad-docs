# Primal-Dual Construction

This note focuses on constructing the dual when constraints and
variable restrictions are not all in the standard form.

---

# 1. Standard Pair

The most important pair is:

### Primal

$$
\max c^Tx
$$

subject to:

$$
Ax\leq b
$$

$$
x\geq0.
$$

### Dual

$$
\min b^Ty
$$

subject to:

$$
A^Ty\geq c
$$

$$
y\geq0.
$$

---

# 2. Constraint-Variable Correspondence

Every primal constraint produces one dual variable.

Therefore:

$$
\boxed{
\text{Primal constraint}
\leftrightarrow
\text{Dual variable}
}
$$

Every primal variable produces one dual constraint.

Therefore:

$$
\boxed{
\text{Primal variable}
\leftrightarrow
\text{Dual constraint}
}
$$

---

# 3. Sign Rules

For a maximization primal:

| Primal constraint | Dual variable |
|---|---|
| $\leq$ | $y_i\geq0$ |
| $\geq$ | $y_i\leq0$ |
| $=$ | $y_i$ unrestricted |

For primal variables:

| Primal variable | Corresponding dual constraint |
|---|---|
| $x_j\geq0$ | $\geq$ |
| $x_j\leq0$ | $\leq$ |
| $x_j$ unrestricted | $=$ |

---

# 4. Example with Mixed Constraints

Consider:

$$
\max Z=3x_1+2x_2
$$

subject to:

$$
2x_1+x_2\leq10
$$

$$
x_1+3x_2\geq12
$$

$$
x_1+x_2=8
$$

$$
x_1,x_2\geq0.
$$

Introduce dual variables:

$$
y_1,y_2,y_3.
$$

From the constraint types:

$$
y_1\geq0
$$

because the first constraint is $\leq$.

$$
y_2\leq0
$$

because the second constraint is $\geq$.

$$
y_3
$$

is unrestricted because the third constraint is equality.

---

# 5. Dual Objective

The primal RHS values are:

$$
10,\quad12,\quad8.
$$

Therefore:

$$
\boxed{
\min W=10y_1+12y_2+8y_3.
}
$$

---

# 6. Dual Constraints

For $x_1$, collect its coefficients:

$$
2,\quad1,\quad1.
$$

Since:

$$
x_1\geq0,
$$

the dual constraint is $\geq$:

$$
\boxed{
2y_1+y_2+y_3\geq3.
}
$$

For $x_2$:

$$
1,\quad3,\quad1.
$$

Therefore:

$$
\boxed{
y_1+3y_2+y_3\geq2.
}
$$

Thus the dual is:

$$
\boxed{
\begin{aligned}
\min W={}&10y_1+12y_2+8y_3\\
\text{s.t. }&
2y_1+y_2+y_3\geq3\\
&
y_1+3y_2+y_3\geq2\\
&
y_1\geq0\\
&
y_2\leq0\\
&
y_3\text{ unrestricted}.
\end{aligned}
}
$$

---

# 7. Free Variables

Suppose the primal contains:

$$
x_j\text{ unrestricted}.
$$

Then the corresponding dual constraint must be:

$$
\boxed{=}.
$$

Conversely, if a dual variable is unrestricted, the corresponding
primal constraint is an equality.

---

# 8. Quick Construction Table

| Primal | Dual |
|---|---|
| Max | Min |
| Min | Max |
| Primal RHS | Dual objective |
| Primal objective | Dual RHS |
| $A$ | $A^T$ |
| $\leq$ constraint in max | $y\geq0$ |
| $\geq$ constraint in max | $y\leq0$ |
| $=$ constraint | $y$ unrestricted |
| $x\geq0$ | dual constraint $\geq$ |
| $x\leq0$ | dual constraint $\leq$ |
| $x$ unrestricted | dual constraint $=$ |

---

# 9. Best Exam Method

Never try to memorize every possible dual form separately.

Instead:

1. Write one dual variable for every primal constraint.
2. Determine its sign from the primal constraint.
3. Write the dual objective using the primal RHS.
4. Transpose the coefficient matrix.
5. Determine each dual constraint from the corresponding primal
   variable's sign.
6. Use the primal objective coefficients as the dual RHS.
7. Reverse max/min.

---

# 10. Practice

Construct the dual:

$$
\max Z=6x_1+5x_2
$$

subject to:

$$
2x_1+x_2\leq20
$$

$$
x_1+2x_2\geq15
$$

$$
x_1-x_2=4
$$

$$
x_1\geq0,\quad x_2\text{ unrestricted}.
$$

First identify:

$$
y_1\geq0
$$

$$
y_2\leq0
$$

$$
y_3\text{ unrestricted}.
$$

Then use the rules above to construct the dual.