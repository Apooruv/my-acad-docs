# Duality in Linear Programming

Every Linear Programming Problem (LPP), called the **Primal**, has
another associated LPP called the **Dual**.

The two problems are mathematically related.

The original problem is called the:

$$
\boxed{\text{Primal}}
$$

and its associated problem is called the:

$$
\boxed{\text{Dual}}.
$$

---

# 1. Basic Idea

Suppose the primal problem is:

$$
\max Z=c^Tx
$$

subject to:

$$
Ax\leq b
$$

$$
x\geq0.
$$

Its dual is:

$$
\boxed{
\min W=b^Ty
}
$$

subject to:

$$
A^Ty\geq c
$$

$$
y\geq0.
$$

Therefore:

$$
\boxed{
\begin{aligned}
\text{Primal: } &\max c^Tx\\
&Ax\leq b,\quad x\geq0
\end{aligned}
}
$$

corresponds to:

$$
\boxed{
\begin{aligned}
\text{Dual: } &\min b^Ty\\
&A^Ty\geq c,\quad y\geq0.
\end{aligned}
}
$$

---

# 2. Matrix Interpretation

Primal:

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

Dual:

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

Notice the changes:

$$
A\rightarrow A^T
$$

$$
c\leftrightarrow b
$$

$$
\max\rightarrow\min
$$

and:

$$
\leq\rightarrow\geq.
$$

---

# 3. Primal-Dual Relationship

Suppose the primal has:

- $n$ decision variables;
- $m$ constraints.

Then the dual has:

- $m$ decision variables;
- $n$ constraints.

Therefore:

$$
\boxed{
\text{Number of primal constraints}
=
\text{Number of dual variables}
}
$$

and:

$$
\boxed{
\text{Number of primal variables}
=
\text{Number of dual constraints}.
}
$$

---

# 4. Economic Interpretation

Consider a maximization problem:

$$
\max Z=c^Tx
$$

where $x$ represents quantities of products.

The constraints represent limited resources.

The dual variables $y_i$ can be interpreted as:

$$
\boxed{\text{implicit values or shadow prices of resources}}
$$

For example, if:

$$
y_1=5,
$$

the corresponding resource has a marginal value of approximately
5 units of objective value per additional unit of that resource,
within the valid sensitivity range.

---

# 5. Example

Consider:

$$
\max Z=40x_1+30x_2
$$

subject to:

$$
2x_1+x_2\leq90
$$

$$
x_1+3x_2\leq120
$$

$$
3x_1+2x_2\leq150
$$

$$
x_1,x_2\geq0.
$$

The primal has:

- 2 variables;
- 3 constraints.

Therefore the dual will have:

- 3 variables;
- 2 constraints.

Let the dual variables be:

$$
y_1,y_2,y_3.
$$

---

# 6. Constructing the Dual

The primal objective coefficients become the RHS of the dual:

$$
40,\quad30.
$$

Therefore the dual constraints have RHS:

$$
40,\quad30.
$$

The primal RHS values:

$$
90,\quad120,\quad150
$$

become the coefficients of the dual objective.

Therefore:

$$
\min W=90y_1+120y_2+150y_3.
$$

---

## Dual Constraint 1

Take the coefficients of $x_1$ from the primal:

$$
2,\quad1,\quad3.
$$

Therefore:

$$
2y_1+y_2+3y_3\geq40.
$$

---

## Dual Constraint 2

Take the coefficients of $x_2$:

$$
1,\quad3,\quad2.
$$

Therefore:

$$
y_1+3y_2+2y_3\geq30.
$$

Thus:

$$
\boxed{
\begin{aligned}
\min W={}&90y_1+120y_2+150y_3\\
\text{s.t. }&
2y_1+y_2+3y_3\geq40\\
&
y_1+3y_2+2y_3\geq30\\
&
y_1,y_2,y_3\geq0.
\end{aligned}
}
$$

---

# 7. The Transpose Rule

The easiest way to construct the dual is:

$$
\boxed{
A_{\text{dual}}=A_{\text{primal}}^T
}
$$

while:

$$
\boxed{
b_{\text{dual}}=c_{\text{primal}}
}
$$

and:

$$
\boxed{
c_{\text{dual}}=b_{\text{primal}}.
}
$$

---

# 8. Dual of a General Maximization Problem

For:

$$
\max c^Tx
$$

subject to:

$$
Ax\leq b
$$

$$
x\geq0,
$$

the dual is:

$$
\boxed{
\min b^Ty
}
$$

subject to:

$$
A^Ty\geq c
$$

$$
y\geq0.
$$

---

# 9. Dual of a General Minimization Problem

For:

$$
\min c^Tx
$$

subject to:

$$
Ax\geq b
$$

$$
x\geq0,
$$

the dual is:

$$
\boxed{
\max b^Ty
}
$$

subject to:

$$
A^Ty\leq c
$$

$$
y\geq0.
$$

---

# 10. The Four Basic Rules

For the common forms:

| Primal | Dual |
|---|---|
| Max | Min |
| Min | Max |
| $A$ | $A^T$ |
| $b$ | $c$ |
| $c$ | $b$ |

For the standard max form:

$$
Ax\leq b,\quad x\geq0
$$

becomes:

$$
A^Ty\geq c,\quad y\geq0.
$$

---

# 11. Sign Restrictions

The sign restriction of a dual variable depends on the
corresponding primal constraint.

For a maximization primal:

| Primal constraint | Dual variable |
|---|---|
| $\leq$ | $y_i\geq0$ |
| $\geq$ | $y_i\leq0$ |
| $=$ | $y_i$ unrestricted |

Similarly, the sign restriction of a primal variable depends on
the corresponding dual constraint.

For a minimization dual:

| Dual constraint | Primal variable |
|---|---|
| $\geq$ | $x_j\geq0$ |
| $\leq$ | $x_j\leq0$ |
| $=$ | $x_j$ unrestricted |

---

# 12. Important Observation

The primal and dual are symmetric.

If we construct the dual of the dual, we recover the original
primal.

Therefore:

$$
\boxed{
(\text{Dual})_{\text{Dual}}=\text{Primal}
}
$$

This is called the **duality of duality**.

---

# 13. Exam Shortcut

When given:

$$
\max Z=c_1x_1+\cdots+c_nx_n
$$

with $m$ constraints:

### Step 1

Create $m$ dual variables.

### Step 2

Make the primal RHS the dual objective coefficients.

### Step 3

Make the primal objective coefficients the dual RHS.

### Step 4

Transpose the coefficient matrix.

### Step 5

Reverse max/min.

### Step 6

Determine signs from the constraint types.

---

# 14. Practice

Construct the dual:

$$
\max Z=5x_1+4x_2
$$

subject to:

$$
x_1+2x_2\leq8
$$

$$
3x_1+x_2\leq9
$$

$$
x_1,x_2\geq0.
$$

### Answer

Let dual variables be $y_1,y_2$.

$$
\boxed{
\min W=8y_1+9y_2
}
$$

subject to:

$$
y_1+3y_2\geq5
$$

$$
2y_1+y_2\geq4
$$

$$
y_1,y_2\geq0.
$$