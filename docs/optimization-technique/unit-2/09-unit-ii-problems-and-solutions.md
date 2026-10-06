# 09 — Unit II Problems and Solutions

# Unit II — Practice Problems

This problem set covers all topics completed in Unit II:

1. Duality
2. Duality Theorem
3. Primal–Dual Construction
4. Complementary Slackness
5. Sensitivity Analysis
6. Dual Simplex Method
7. Matrix Calculus
8. Conditions for Solution of an Unconstrained Problem

The LPP lab uses the \(C_j-Z_j\) convention, so the maximization optimality condition used here is:

\[
\boxed{C_j-Z_j\leq0}
\]

---

# Part A — Duality

## Problem 1 — Construct the Dual

Consider the primal problem:

\[
\max Z=40x_1+30x_2
\]

subject to:

\[
2x_1+x_2\leq90
\]

\[
x_1+3x_2\leq120
\]

\[
3x_1+2x_2\leq150
\]

\[
x_1,x_2\geq0
\]

Construct the dual.

---

## Solution

The primal has:

- 2 variables
- 3 constraints

Therefore the dual has:

- 3 variables
- 2 constraints

Introduce:

\[
y_1,y_2,y_3\geq0
\]

Since the primal is a maximization problem with \(\leq\) constraints, the dual is a minimization problem with \(\geq\) constraints.

The dual objective is obtained from the RHS:

\[
\boxed{
\min W=90y_1+120y_2+150y_3
}
\]

The first dual constraint comes from the coefficients of \(x_1\):

\[
2y_1+y_2+3y_3\geq40
\]

The second dual constraint comes from the coefficients of \(x_2\):

\[
y_1+3y_2+2y_3\geq30
\]

Therefore:

\[
\boxed{
\begin{aligned}
\min W={}&90y_1+120y_2+150y_3\\
\text{s.t. }&
2y_1+y_2+3y_3\geq40\\
&
y_1+3y_2+2y_3\geq30\\
&
y_1,y_2,y_3\geq0
\end{aligned}
}
\]

---

# Problem 2 — Dual of a Mixed LPP

Construct the dual of:

\[
\max Z=3x_1+2x_2
\]

subject to:

\[
2x_1+x_2\leq10
\]

\[
x_1+3x_2\geq12
\]

\[
x_1+x_2=8
\]

\[
x_1,x_2\geq0
\]

---

## Solution

Introduce dual variables:

\[
y_1,y_2,y_3
\]

The primal is a maximization problem.

Therefore:

| Primal constraint | Dual variable |
|---|---|
| \(\leq\) | \(y_i\geq0\) |
| \(\geq\) | \(y_i\leq0\) |
| \(=\) | \(y_i\) unrestricted |

Therefore:

\[
y_1\geq0
\]

\[
y_2\leq0
\]

\[
y_3\text{ unrestricted}
\]

The dual objective is:

\[
\boxed{
\min W=10y_1+12y_2+8y_3
}
\]

For \(x_1\):

\[
2y_1+y_2+y_3\geq3
\]

For \(x_2\):

\[
y_1+3y_2+y_3\geq2
\]

Therefore:

\[
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
y_3\text{ unrestricted}
\end{aligned}
}
\]

---

# Part B — Duality Theorem

## Problem 3 — Verify Weak Duality

Consider:

\[
\max Z=3x_1+2x_2
\]

with a feasible primal solution:

\[
x=
\begin{bmatrix}
2\\
1
\end{bmatrix}
\]

and a feasible dual solution:

\[
y=
\begin{bmatrix}
1\\
2
\end{bmatrix}
\]

Suppose:

\[
Z=8
\]

and:

\[
W=10
\]

Verify the weak duality theorem.

---

## Solution

The Weak Duality Theorem states:

\[
\boxed{Z\leq W}
\]

for every feasible primal-dual pair.

Here:

\[
Z=8
\]

and:

\[
W=10
\]

Therefore:

\[
8\leq10
\]

Hence:

\[
\boxed{Z\leq W}
\]

Weak duality is satisfied.

---

# Problem 4 — Optimality Certificate

Suppose a feasible primal solution gives:

\[
Z=2100
\]

and a feasible dual solution gives:

\[
W=2100
\]

Can we conclude that both solutions are optimal?

---

## Solution

By weak duality:

\[
Z\leq W
\]

for every feasible pair.

We have:

\[
Z=2100
\]

and:

\[
W=2100
\]

Therefore:

\[
Z=W
\]

By the Strong Duality Theorem:

\[
\boxed{Z^*=W^*=2100}
\]

Hence:

\[
\boxed{\text{Both solutions are optimal}}
\]

This is an important optimality certificate:

\[
\boxed{
\text{Primal feasible}
+
\text{Dual feasible}
+
Z=W
\Rightarrow
\text{Optimal}
}
\]

---

# Part C — Complementary Slackness

## Problem 5 — Find the Dual Solution

Consider:

\[
\max Z=40x_1+30x_2
\]

subject to:

\[
2x_1+x_2\leq90
\]

\[
x_1+3x_2\leq120
\]

\[
3x_1+2x_2\leq150
\]

Suppose the optimal primal solution is:

\[
x_1=30,\qquad x_2=30
\]

Use complementary slackness to find the optimal dual solution.

---

## Solution

The dual is:

\[
\min W=90y_1+120y_2+150y_3
\]

subject to:

\[
2y_1+y_2+3y_3\geq40
\]

\[
y_1+3y_2+2y_3\geq30
\]

\[
y_1,y_2,y_3\geq0
\]

Evaluate the primal constraints.

### Constraint 1

\[
2(30)+30=90
\]

It is tight.

### Constraint 2

\[
30+3(30)=120
\]

It is tight.

### Constraint 3

\[
3(30)+2(30)=150
\]

It is also tight.

Since all primal constraints are tight, complementary slackness does not force any \(y_i\) to zero.

Now both \(x_1\) and \(x_2\) are positive.

Therefore their corresponding dual constraints must be tight:

\[
2y_1+y_2+3y_3=40
\]

\[
y_1+3y_2+2y_3=30
\]

There are infinitely many solutions to these two equations, so primal optimality alone does not uniquely determine the dual variables.

However, the dual optimum for this problem is:

\[
\boxed{y_1=18,\quad y_2=4,\quad y_3=0}
\]

Check:

\[
2(18)+4+3(0)=40
\]

and:

\[
18+3(4)+2(0)=30
\]

Both are satisfied.

Dual objective:

\[
W=90(18)+120(4)+150(0)
\]

\[
W=1620+480
\]

\[
\boxed{W=2100}
\]

Since:

\[
Z=W=2100
\]

both solutions are optimal.

---

# Part D — Sensitivity Analysis

## Problem 6 — Shadow Price

For the previous problem, suppose:

\[
y=(18,4,0)
\]

What is the shadow price of the first resource?

What happens to the objective value if the first RHS increases by 5 units, assuming the current basis remains valid?

---

## Solution

The first dual variable is:

\[
y_1=18
\]

Therefore the shadow price is:

\[
\boxed{18}
\]

For:

\[
\Delta b=
\begin{bmatrix}
5\\
0\\
0
\end{bmatrix}
\]

the objective change is:

\[
\Delta Z=y^T\Delta b
\]

Therefore:

\[
\Delta Z=18(5)
\]

\[
\boxed{\Delta Z=90}
\]

The new objective value is:

\[
Z'=2100+90
\]

\[
\boxed{Z'=2190}
\]

provided the current basis remains feasible.

---

# Problem 7 — RHS Sensitivity

Using:

\[
B^{-1}=
\begin{bmatrix}
3/5&-1/5&0\\
-1/5&2/5&0\\
-7/5&-1/5&1
\end{bmatrix}
\]

and:

\[
x_B=
\begin{bmatrix}
30\\
30\\
0
\end{bmatrix}
\]

suppose the first RHS changes by:

\[
\Delta b_1=\Delta
\]

Find the range of \(\Delta\) for which the current basis remains feasible.

---

## Solution

We have:

\[
\Delta b=
\begin{bmatrix}
\Delta\\
0\\
0
\end{bmatrix}
\]

Therefore:

\[
x_B'
=
x_B+B^{-1}\Delta b
\]

Hence:

\[
\begin{bmatrix}
x_1'\\
x_2'\\
s_3'
\end{bmatrix}
=
\begin{bmatrix}
30\\
30\\
0
\end{bmatrix}
+
\begin{bmatrix}
3/5\\
-1/5\\
-7/5
\end{bmatrix}
\Delta
\]

Thus:

\[
x_1'=30+\frac35\Delta
\]

\[
x_2'=30-\frac15\Delta
\]

\[
s_3'=-\frac75\Delta
\]

For feasibility:

\[
x_1'\geq0
\]

gives:

\[
\Delta\geq-50
\]

\[
x_2'\geq0
\]

gives:

\[
\Delta\leq150
\]

and:

\[
s_3'\geq0
\]

gives:

\[
\Delta\leq0
\]

Combining:

\[
\boxed{-50\leq\Delta\leq0}
\]

Therefore the first RHS can vary from:

\[
90-50=40
\]

to:

\[
90+0=90
\]

Hence:

\[
\boxed{40\leq b_1\leq90}
\]

---

# Part E — Dual Simplex

## Problem 8 — One Dual Simplex Iteration

Consider the tableau:

| Basis | \(x_1\) | \(x_2\) | \(s_1\) | \(s_2\) | RHS |
|---|---:|---:|---:|---:|---:|
| \(s_1\) | 1 | -1 | 1 | 0 | -2 |
| \(s_2\) | -1 | 2 | 0 | 1 | 4 |
| \(C_j-Z_j\) | -1 | -2 | 0 | 0 | |

Perform one Dual Simplex iteration.

---

## Solution

First check dual feasibility:

\[
C_j-Z_j=(-1,-2,0,0)
\]

All values satisfy:

\[
C_j-Z_j\leq0
\]

Therefore dual feasibility holds.

But:

\[
RHS=(-2,4)
\]

contains a negative value.

---

### Step 1 — Leaving Variable

Most negative RHS:

\[
-2
\]

Therefore:

\[
\boxed{s_1\text{ leaves}}
\]

---

### Step 2 — Candidate Entering Variables

Selected row:

\[
[1,-1,1,0]
\]

Only negative coefficient:

\[
a_{12}=-1
\]

Therefore \(x_2\) is the only candidate.

---

### Step 3 — Ratio

\[
\theta=
\frac{C_2-Z_2}{a_{12}}
\]

\[
\theta=
\frac{-2}{-1}=2
\]

Therefore:

\[
\boxed{x_2\text{ enters}}
\]

Pivot:

\[
\boxed{-1}
\]

---

### Step 4 — Pivot

Original first row:

\[
x_1-x_2+s_1=-2
\]

Divide by \(-1\):

\[
-x_1+x_2-s_1=2
\]

The new basis is:

\[
\boxed{x_2,s_2}
\]

The second row becomes:

\[
x_1+2s_1+s_2=0
\]

Therefore:

| Basis | \(x_1\) | \(x_2\) | \(s_1\) | \(s_2\) | RHS |
|---|---:|---:|---:|---:|---:|
| \(x_2\) | -1 | 1 | -1 | 0 | 2 |
| \(s_2\) | 1 | 0 | 2 | 1 | 0 |

All RHS values are now non-negative.

Therefore the primal feasibility condition has been restored.

---

# Problem 9 — Dual Simplex Infeasibility

Suppose a Dual Simplex iteration selects a row:

\[
[2,3,1,0\mid-5]
\]

Can the algorithm continue?

---

## Solution

The RHS is:

\[
-5<0
\]

Therefore this row must be repaired.

For Dual Simplex, an entering variable requires:

\[
a_{ij}<0
\]

But the row contains:

\[
2,\quad3,\quad1,\quad0
\]

There is no negative coefficient.

Therefore no entering variable exists.

Hence:

\[
\boxed{\text{The problem is infeasible}}
\]

---

# Part F — Matrix Calculus

## Problem 10 — Find the Gradient

Find the gradient of:

\[
f(x_1,x_2)
=
x_1^2+3x_1x_2+2x_2^2
\]

---

## Solution

Differentiate with respect to \(x_1\):

\[
\frac{\partial f}{\partial x_1}
=
2x_1+3x_2
\]

Differentiate with respect to \(x_2\):

\[
\frac{\partial f}{\partial x_2}
=
3x_1+4x_2
\]

Therefore:

\[
\boxed{
\nabla f=
\begin{bmatrix}
2x_1+3x_2\\
3x_1+4x_2
\end{bmatrix}
}
\]

---

# Problem 11 — Find the Hessian

For:

\[
f(x_1,x_2)
=
x_1^2+3x_1x_2+2x_2^2
\]

find the Hessian.

---

## Solution

The gradient is:

\[
\nabla f=
\begin{bmatrix}
2x_1+3x_2\\
3x_1+4x_2
\end{bmatrix}
\]

Differentiate again:

\[
H=
\begin{bmatrix}
2&3\\
3&4
\end{bmatrix}
\]

Therefore:

\[
\boxed{
\nabla^2f=
\begin{bmatrix}
2&3\\
3&4
\end{bmatrix}
}
\]

---

# Problem 12 — Gradient of a Quadratic Function

Find the gradient and Hessian of:

\[
f(x)=\frac12x^TAx+b^Tx+c
\]

where \(A=A^T\).

---

## Solution

For a symmetric matrix:

\[
\boxed{
\nabla f(x)=Ax+b
}
\]

The Hessian is:

\[
\boxed{
\nabla^2f(x)=A
}
\]

Therefore:

\[
\boxed{
\nabla f=Ax+b
}
\]

and:

\[
\boxed{
H=A
}
\]

---

# Problem 13 — Directional Derivative

Let:

\[
f(x_1,x_2)=x_1^2+x_2^2
\]

Find the directional derivative at:

\[
x=(1,2)
\]

in the direction:

\[
d=
\begin{bmatrix}
3\\
4
\end{bmatrix}
\]

---

## Solution

First calculate the gradient:

\[
\nabla f=
\begin{bmatrix}
2x_1\\
2x_2
\end{bmatrix}
\]

At:

\[
x=(1,2)
\]

we get:

\[
\nabla f(1,2)=
\begin{bmatrix}
2\\
4
\end{bmatrix}
\]

The directional derivative is:

\[
D_df(x)=\nabla f(x)^Td
\]

Therefore:

\[
D_df=
\begin{bmatrix}
2&4
\end{bmatrix}
\begin{bmatrix}
3\\
4
\end{bmatrix}
\]

\[
=6+16
\]

\[
\boxed{D_df=22}
\]

---

# Problem 14 — Direction of Steepest Descent

For:

\[
f(x_1,x_2)=x_1^2+x_2^2
\]

find the direction of steepest descent at:

\[
x=(3,4)
\]

---

## Solution

Gradient:

\[
\nabla f=
\begin{bmatrix}
2x_1\\
2x_2
\end{bmatrix}
\]

At:

\[
(3,4)
\]

we have:

\[
\nabla f=
\begin{bmatrix}
6\\
8
\end{bmatrix}
\]

The magnitude is:

\[
\|\nabla f\|
=
\sqrt{6^2+8^2}
\]

\[
=10
\]

The unit direction of steepest descent is:

\[
d=
-\frac{\nabla f}{\|\nabla f\|}
\]

Therefore:

\[
d=
-\frac1{10}
\begin{bmatrix}
6\\
8
\end{bmatrix}
\]

Hence:

\[
\boxed{
d=
\begin{bmatrix}
-0.6\\
-0.8
\end{bmatrix}
}
\]

---

# Part G — Unconstrained Optimization

## Problem 15 — Find the Minimum

Find the stationary point and classify it:

\[
f(x_1,x_2)=x_1^2+x_2^2
\]

---

## Solution

### Step 1 — Gradient

\[
\nabla f=
\begin{bmatrix}
2x_1\\
2x_2
\end{bmatrix}
\]

Set:

\[
\nabla f=0
\]

Therefore:

\[
x_1=0
\]

\[
x_2=0
\]

So:

\[
x^*=(0,0)
\]

---

### Step 2 — Hessian

\[
H=
\begin{bmatrix}
2&0\\
0&2
\end{bmatrix}
\]

The eigenvalues are:

\[
2,2
\]

Both are positive.

Therefore:

\[
H\succ0
\]

Hence:

\[
\boxed{(0,0)\text{ is a strict local minimum}}
\]

Since the function is convex:

\[
\boxed{(0,0)\text{ is also the global minimum}}
\]

and:

\[
\boxed{f_{\min}=0}
\]

---

# Problem 16 — Find the Maximum

Find and classify the stationary point:

\[
f(x_1,x_2)=-(x_1^2+x_2^2)
\]

---

## Solution

Gradient:

\[
\nabla f=
\begin{bmatrix}
-2x_1\\
-2x_2
\end{bmatrix}
\]

Setting it equal to zero:

\[
x_1=x_2=0
\]

Therefore:

\[
x^*=(0,0)
\]

Hessian:

\[
H=
\begin{bmatrix}
-2&0\\
0&-2
\end{bmatrix}
\]

Both eigenvalues are negative.

Therefore:

\[
H\prec0
\]

Hence:

\[
\boxed{(0,0)\text{ is a strict local maximum}}
\]

---

# Problem 17 — Identify the Saddle Point

Classify the stationary point of:

\[
f(x_1,x_2)=x_1^2-x_2^2
\]

---

## Solution

Gradient:

\[
\nabla f=
\begin{bmatrix}
2x_1\\
-2x_2
\end{bmatrix}
\]

Set:

\[
\nabla f=0
\]

Therefore:

\[
x_1=x_2=0
\]

Hessian:

\[
H=
\begin{bmatrix}
2&0\\
0&-2
\end{bmatrix}
\]

The eigenvalues are:

\[
2,-2
\]

One is positive and one is negative.

Therefore \(H\) is indefinite.

Hence:

\[
\boxed{(0,0)\text{ is a saddle point}}
\]

---

# Problem 18 — Two-Variable Second-Order Test

Classify the stationary point of:

\[
f(x_1,x_2)
=
x_1^2+4x_1x_2+5x_2^2
\]

---

## Solution

### Step 1 — Gradient

\[
\frac{\partial f}{\partial x_1}
=
2x_1+4x_2
\]

\[
\frac{\partial f}{\partial x_2}
=
4x_1+10x_2
\]

Set both equal to zero:

\[
2x_1+4x_2=0
\]

\[
4x_1+10x_2=0
\]

The solution is:

\[
x_1=0,\qquad x_2=0
\]

---

### Step 2 — Hessian

\[
H=
\begin{bmatrix}
2&4\\
4&10
\end{bmatrix}
\]

Calculate determinant:

\[
D=
(2)(10)-(4)(4)
\]

\[
D=20-16
\]

\[
D=4>0
\]

Also:

\[
f_{x_1x_1}=2>0
\]

Therefore:

\[
\boxed{\text{Strict local minimum}}
\]

---

# Problem 19 — Indefinite Hessian

Classify:

\[
f(x_1,x_2)=x_1^2-4x_1x_2+x_2^2
\]

---

## Solution

Gradient:

\[
\nabla f=
\begin{bmatrix}
2x_1-4x_2\\
-4x_1+2x_2
\end{bmatrix}
\]

Stationary point:

\[
x_1=x_2=0
\]

Hessian:

\[
H=
\begin{bmatrix}
2&-4\\
-4&2
\end{bmatrix}
\]

Determinant:

\[
D=(2)(2)-(-4)^2
\]

\[
D=4-16
\]

\[
D=-12<0
\]

Therefore:

\[
\boxed{\text{Saddle point}}
\]

---

# Part H — Mixed Exam Problem

## Problem 20

Consider:

\[
f(x_1,x_2)
=
x_1^2+2x_1x_2+2x_2^2-4x_1-6x_2
\]

Find:

1. The gradient.
2. The stationary point.
3. The Hessian.
4. The type of stationary point.
5. The minimum value.

---

## Solution

### Step 1 — Gradient

\[
\frac{\partial f}{\partial x_1}
=
2x_1+2x_2-4
\]

\[
\frac{\partial f}{\partial x_2}
=
2x_1+4x_2-6
\]

Therefore:

\[
\nabla f=
\begin{bmatrix}
2x_1+2x_2-4\\
2x_1+4x_2-6
\end{bmatrix}
\]

---

### Step 2 — Stationary Point

Set:

\[
2x_1+2x_2-4=0
\]

Therefore:

\[
x_1+x_2=2
\]

Second equation:

\[
2x_1+4x_2-6=0
\]

or:

\[
x_1+2x_2=3
\]

Subtract:

\[
x_2=1
\]

Therefore:

\[
x_1=1
\]

So:

\[
\boxed{x^*=(1,1)}
\]

---

### Step 3 — Hessian

\[
H=
\begin{bmatrix}
2&2\\
2&4
\end{bmatrix}
\]

---

### Step 4 — Classification

Calculate determinant:

\[
D=(2)(4)-(2)(2)
\]

\[
D=8-4=4>0
\]

and:

\[
f_{x_1x_1}=2>0
\]

Therefore:

\[
\boxed{x^*=(1,1)\text{ is a strict local minimum}}
\]

Since the Hessian is positive definite everywhere, the function is strictly convex.

Therefore this is also the unique global minimum.

---

### Step 5 — Minimum Value

Substitute:

\[
x_1=1,\qquad x_2=1
\]

into:

\[
f=x_1^2+2x_1x_2+2x_2^2-4x_1-6x_2
\]

\[
f(1,1)
=
1+2+2-4-6
\]

\[
=5-10
\]

\[
\boxed{f_{\min}=-5}
\]

---

# Final Unit II Formula Sheet

## Duality

\[
\boxed{
\max c^Tx,\ Ax\leq b,\ x\geq0
}
\]

has dual:

\[
\boxed{
\min b^Ty,\ A^Ty\geq c,\ y\geq0
}
\]

---

## Weak Duality

\[
\boxed{
c^Tx\leq b^Ty
}
\]

for every feasible primal-dual pair.

---

## Strong Duality

\[
\boxed{
Z^*=W^*
}
\]

when optimal solutions exist.

---

## Complementary Slackness

\[
\boxed{
y_i[b_i-(Ax)_i]=0
}
\]

\[
\boxed{
x_j[(A^Ty)_j-c_j]=0
}
\]

---

## Sensitivity

\[
\boxed{
x_B'=x_B+B^{-1}\Delta b
}
\]

\[
\boxed{
\Delta Z=y^T\Delta b
}
\]

\[
\boxed{
y^T=C_BB^{-1}
}
\]

---

## Dual Simplex

For maximization:

\[
\boxed{
C_j-Z_j\leq0
}
\]

Select:

\[
\boxed{\text{Most negative RHS}}
\]

Then:

\[
\boxed{a_{ij}<0}
\]

and:

\[
\boxed{
\frac{C_j-Z_j}{a_{ij}}
}
\]

Choose the smallest non-negative ratio.

---

## Gradient

\[
\boxed{
\nabla f(x)=
\begin{bmatrix}
\frac{\partial f}{\partial x_1}\\
\vdots\\
\frac{\partial f}{\partial x_n}
\end{bmatrix}
}
\]

---

## Hessian

\[
\boxed{
H(x)=\nabla^2f(x)
}
\]

---

## First-Order Condition

\[
\boxed{
\nabla f(x^*)=0
}
\]

---

## Second-Order Conditions

Minimum:

\[
\boxed{
H(x^*)\succ0
}
\]

Maximum:

\[
\boxed{
H(x^*)\prec0
}
\]

Saddle:

\[
\boxed{
H(x^*)\text{ indefinite}
}
\]

---

# Unit II Exam Strategy

For numerical problems:

### LPP / Duality

```text
1. Write primal.
2. Construct dual.
3. Solve/check feasibility.
4. Apply weak/strong duality.
5. Use complementary slackness if required.
```

### Sensitivity

```text
1. Identify the change.
2. RHS change → use B^-1 Δb.
3. Objective change → update reduced costs.
4. Check feasibility/optimality.
5. Calculate new objective value.
```

### Dual Simplex

```text
1. Check Cj - Zj <= 0.
2. Find most negative RHS.
3. Select negative coefficients in that row.
4. Calculate ratio.
5. Pivot.
6. Repeat until RHS >= 0.
```

### Unconstrained Optimization

```text
1. Calculate gradient.
2. Set gradient = 0.
3. Find stationary points.
4. Calculate Hessian.
5. Check definiteness.
6. Classify minimum / maximum / saddle.
7. Calculate objective value.
```

---

# Unit II Checklist

- [ ] Can construct a dual from a primal.
- [ ] Can handle mixed constraint signs.
- [ ] Can apply Weak Duality.
- [ ] Can use Strong Duality as an optimality certificate.
- [ ] Can apply Complementary Slackness.
- [ ] Can calculate shadow prices.
- [ ] Can perform RHS sensitivity.
- [ ] Can calculate allowable RHS changes.
- [ ] Can perform a Dual Simplex iteration.
- [ ] Can identify infeasibility in Dual Simplex.
- [ ] Can calculate gradients.
- [ ] Can calculate Hessians.
- [ ] Can classify matrices as positive/negative definite.
- [ ] Can find stationary points.
- [ ] Can classify local minima, maxima and saddle points.
- [ ] Can solve two-variable second-order tests.
```
