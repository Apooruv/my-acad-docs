# Matrix Form of Linear Programming Problems

The matrix representation of an LPP provides a compact mathematical
form that is particularly useful for the Revised Simplex Method.

---

## 1. General Matrix Form

Consider an LPP:

$$
\max Z=c_1x_1+c_2x_2+\cdots+c_nx_n
$$

subject to

$$
a_{11}x_1+a_{12}x_2+\cdots+a_{1n}x_n=b_1
$$

$$
a_{21}x_1+a_{22}x_2+\cdots+a_{2n}x_n=b_2
$$

$$
\vdots
$$

$$
a_{m1}x_1+a_{m2}x_2+\cdots+a_{mn}x_n=b_m
$$

with

$$
x_j\geq0.
$$

Define

$$
x=
\begin{bmatrix}
x_1\\
x_2\\
\vdots\\
x_n
\end{bmatrix}
$$

$$
c=
\begin{bmatrix}
c_1\\
c_2\\
\vdots\\
c_n
\end{bmatrix}
$$

$$
b=
\begin{bmatrix}
b_1\\
b_2\\
\vdots\\
b_m
\end{bmatrix}
$$

and

$$
A=
\begin{bmatrix}
a_{11}&a_{12}&\cdots&a_{1n}\\
a_{21}&a_{22}&\cdots&a_{2n}\\
\vdots&\vdots&\ddots&\vdots\\
a_{m1}&a_{m2}&\cdots&a_{mn}
\end{bmatrix}.
$$

Then:

$$
\boxed{
\max Z=c^Tx
}
$$

subject to

$$
\boxed{
Ax=b
}
$$

and

$$
\boxed{
x\geq0.
}
$$

---

# 2. Meaning of the Matrices

| Symbol | Meaning | Dimension |
|---|---|---|
| $A$ | Constraint coefficient matrix | $m\times n$ |
| $x$ | Decision-variable vector | $n\times1$ |
| $b$ | RHS/resource vector | $m\times1$ |
| $c$ | Objective coefficient vector | $n\times1$ |
| $c^T$ | Objective row vector | $1\times n$ |

Therefore:

$$
Ax
$$

has dimension

$$
(m\times n)(n\times1)=m\times1,
$$

which matches the dimension of $b$.

---

# 3. Example

Consider:

$$
\max Z=40x_1+30x_2
$$

subject to

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

Introduce slack variables:

$$
2x_1+x_2+s_1=90
$$

$$
x_1+3x_2+s_2=120
$$

$$
3x_1+2x_2+s_3=150.
$$

Define:

$$
x=
\begin{bmatrix}
x_1\\
x_2\\
s_1\\
s_2\\
s_3
\end{bmatrix}
$$

and

$$
A=
\begin{bmatrix}
2&1&1&0&0\\
1&3&0&1&0\\
3&2&0&0&1
\end{bmatrix}.
$$

The RHS vector is:

$$
b=
\begin{bmatrix}
90\\
120\\
150
\end{bmatrix}.
$$

The objective vector is:

$$
c=
\begin{bmatrix}
40\\
30\\
0\\
0\\
0
\end{bmatrix}.
$$

Therefore:

$$
\boxed{
\max Z=c^Tx
}
$$

subject to

$$
\boxed{
Ax=b,\qquad x\geq0.
}
$$

---

# 4. Columns of $A$

Write the columns of $A$ as:

$$
A=
\begin{bmatrix}
a_1&a_2&\cdots&a_n
\end{bmatrix}.
$$

Thus:

$$
Ax=
a_1x_1+a_2x_2+\cdots+a_nx_n.
$$

Each column corresponds to one variable.

For the example:

$$
a_1=
\begin{bmatrix}
2\\1\\3
\end{bmatrix}
$$

$$
a_2=
\begin{bmatrix}
1\\3\\2
\end{bmatrix}
$$

$$
a_3=
\begin{bmatrix}
1\\0\\0
\end{bmatrix}
$$

etc.

---

# 5. Basis Matrix

Suppose $m$ variables are selected as basic variables.

Take the corresponding $m$ columns of $A$.

The resulting matrix is called the **basis matrix**:

$$
\boxed{
B=
\begin{bmatrix}
a_{B_1}&a_{B_2}&\cdots&a_{B_m}
\end{bmatrix}.
}
$$

For a valid basis:

$$
\det(B)\neq0.
$$

Therefore $B$ must be nonsingular.

---

# 6. Basic Variables

Partition the variables into:

$$
x_B
$$

and

$$
x_N.
$$

Then:

$$
Ax=b
$$

can be written as

$$
Bx_B+Nx_N=b.
$$

For a basic solution, set:

$$
x_N=0.
$$

Therefore:

$$
Bx_B=b.
$$

Hence:

$$
\boxed{
x_B=B^{-1}b.
}
$$

This equation is one of the most important equations in the
Revised Simplex Method.

---

# 7. Basic Feasible Solution

A basis produces a basic solution:

$$
x_B=B^{-1}b.
$$

If:

$$
x_B\geq0,
$$

then the basis gives a Basic Feasible Solution.

Therefore:

$$
\boxed{
B^{-1}b\geq0
}
$$

is the feasibility condition for the current basis.

---

# 8. Basic Solution Example

Using:

$$
A=
\begin{bmatrix}
2&1&1&0&0\\
1&3&0&1&0\\
3&2&0&0&1
\end{bmatrix}
$$

select the slack columns:

$$
B=
\begin{bmatrix}
1&0&0\\
0&1&0\\
0&0&1
\end{bmatrix}.
$$

Therefore:

$$
B=I
$$

and

$$
B^{-1}=I.
$$

Thus:

$$
x_B=B^{-1}b=b.
$$

Hence:

$$
x_B=
\begin{bmatrix}
90\\
120\\
150
\end{bmatrix}.
$$

The initial BFS is:

$$
x_1=x_2=0
$$

$$
s_1=90,\quad s_2=120,\quad s_3=150.
$$

---

# 9. Objective Value of a Basis

Let:

$$
C_B=
\begin{bmatrix}
c_{B_1}&c_{B_2}&\cdots&c_{B_m}
\end{bmatrix}.
$$

Then:

$$
\boxed{
Z=C_Bx_B.
}
$$

Since:

$$
x_B=B^{-1}b,
$$

we obtain:

$$
\boxed{
Z=C_BB^{-1}b.
}
$$

---

# 10. Simplex Multipliers

Define:

$$
\boxed{
y^T=C_BB^{-1}.
}
$$

The vector $y$ is sometimes called the vector of simplex
multipliers or dual prices.

Then:

$$
Z=y^Tb.
$$

For every column $a_j$:

$$
Z_j=y^Ta_j.
$$

Therefore:

$$
\boxed{
Z_j=C_BB^{-1}a_j.
}
$$

---

# 11. Reduced Cost

For a maximization problem, define:

$$
\boxed{
C_j-Z_j
}
$$

where

$$
Z_j=C_BB^{-1}a_j.
$$

Therefore:

$$
\boxed{
C_j-Z_j
=
C_j-C_BB^{-1}a_j.
}
$$

For a maximization problem:

$$
\boxed{
C_j-Z_j\leq0
}
$$

for every variable indicates optimality.

---

# 12. Why Matrix Form Matters

The ordinary Simplex Method repeatedly manipulates the entire tableau.

The Revised Simplex Method instead works primarily with:

$$
B^{-1}
$$

and vectors such as:

$$
B^{-1}b
$$

and

$$
B^{-1}a_j.
$$

This reduces unnecessary computation, especially for large problems.

---

# 13. Important Relationships

Memorize these:

### Basic solution

$$
\boxed{x_B=B^{-1}b}
$$

### Objective value

$$
\boxed{Z=C_Bx_B}
$$

### Simplex multiplier

$$
\boxed{y^T=C_BB^{-1}}
$$

### Column contribution

$$
\boxed{Z_j=y^Ta_j}
$$

### Reduced cost

$$
\boxed{C_j-Z_j=C_j-y^Ta_j}
$$

### Optimality for maximization

$$
\boxed{C_j-Z_j\leq0\quad\forall j}
$$

---

# 14. Exam Problem

Given:

$$
B=
\begin{bmatrix}
2&1\\
1&3
\end{bmatrix},
\qquad
b=
\begin{bmatrix}
8\\
9
\end{bmatrix},
$$

and

$$
C_B=
\begin{bmatrix}
5&4
\end{bmatrix},
$$

calculate:

1. $B^{-1}$
2. $x_B$
3. $Z$

---

## Solution

### Step 1 — Find $B^{-1}$

For

$$
B=
\begin{bmatrix}
2&1\\
1&3
\end{bmatrix},
$$

the determinant is:

$$
|B|=(2)(3)-(1)(1)=5.
$$

Therefore:

$$
B^{-1}
=
\frac15
\begin{bmatrix}
3&-1\\
-1&2
\end{bmatrix}.
$$

---

### Step 2 — Calculate $x_B$

$$
x_B=B^{-1}b
$$

$$
=
\frac15
\begin{bmatrix}
3&-1\\
-1&2
\end{bmatrix}
\begin{bmatrix}
8\\
9
\end{bmatrix}.
$$

First component:

$$
\frac{24-9}{5}=3.
$$

Second:

$$
\frac{-8+18}{5}=2.
$$

Therefore:

$$
\boxed{
x_B=
\begin{bmatrix}
3\\
2
\end{bmatrix}
}
$$

---

### Step 3 — Calculate $Z$

$$
Z=C_Bx_B
$$

$$
=
\begin{bmatrix}
5&4
\end{bmatrix}
\begin{bmatrix}
3\\
2
\end{bmatrix}
$$

$$
=15+8
$$

$$
\boxed{Z=23}.
$$

---

# Quick Revision

$$
Ax=b
$$

$$
Bx_B=b
$$

$$
x_B=B^{-1}b
$$

$$
Z=C_Bx_B
$$

$$
y^T=C_BB^{-1}
$$

$$
Z_j=y^Ta_j
$$

$$
C_j-Z_j=C_j-y^Ta_j
$$

For maximization:

$$
\boxed{C_j-Z_j\leq0}
$$

at optimum.