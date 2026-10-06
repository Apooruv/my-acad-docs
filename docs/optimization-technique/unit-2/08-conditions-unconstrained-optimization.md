# 08 — Conditions for Solution of an Unconstrained Problem

## 1. Unconstrained Optimization

An unconstrained optimization problem has the form:

\[
\boxed{
\min_{x\in\mathbb{R}^n}f(x)
}
\]

There are no constraints such as:

\[
g(x)\leq0
\]

or:

\[
h(x)=0
\]

The only variable is:

\[
x\in\mathbb{R}^n
\]

---

# 2. Local Minimum

A point \(x^*\) is a local minimum if there exists a neighborhood around \(x^*\) such that:

\[
f(x^*)\leq f(x)
\]

for every \(x\) sufficiently close to \(x^*\).

In simple terms:

> The function is not smaller than \(f(x^*)\) near \(x^*\).

---

# 3. Strict Local Minimum

A point \(x^*\) is a strict local minimum if:

\[
\boxed{
f(x^*)<f(x)
}
\]

for every:

\[
x\neq x^*
\]

sufficiently close to \(x^*\).

---

# 4. Local Maximum

A point \(x^*\) is a local maximum if:

\[
\boxed{
f(x^*)\geq f(x)
}
\]

for all \(x\) sufficiently close to \(x^*\).

---

# 5. Stationary Point

A point \(x^*\) is called a stationary point if:

\[
\boxed{
\nabla f(x^*)=0
}
\]

That means:

\[
\frac{\partial f}{\partial x_1}=0
\]

\[
\frac{\partial f}{\partial x_2}=0
\]

\[
\vdots
\]

\[
\frac{\partial f}{\partial x_n}=0
\]

---

# 6. First-Order Necessary Condition

Suppose \(f\) is differentiable and \(x^*\) is an interior local minimum or maximum.

Then:

\[
\boxed{
\nabla f(x^*)=0
}
\]

This is the **first-order necessary condition**.

---

# 7. Why Must the Gradient Be Zero?

Suppose:

\[
\nabla f(x^*)\neq0
\]

Then we can move in the direction:

\[
d=-\nabla f(x^*)
\]

The directional derivative is:

\[
D_df(x^*)
=
\nabla f(x^*)^Td
\]

Substituting:

\[
D_df(x^*)
=
-\nabla f(x^*)^T\nabla f(x^*)
\]

Therefore:

\[
D_df(x^*)
=
-\|\nabla f(x^*)\|^2<0
\]

So the function decreases in that direction.

Hence \(x^*\) cannot be a local minimum.

Therefore a differentiable interior optimum must satisfy:

\[
\boxed{\nabla f(x^*)=0}
\]

---

# 8. Important Warning

The condition:

\[
\nabla f(x^*)=0
\]

is **necessary**, but not sufficient.

A stationary point can be:

- Local minimum
- Local maximum
- Saddle point

Therefore, we need second-order information.

---

# 9. Second-Order Necessary Condition

Suppose \(f\) is twice differentiable and \(x^*\) is a local minimum.

Then:

\[
\boxed{
\nabla f(x^*)=0
}
\]

and:

\[
\boxed{
\nabla^2f(x^*)\succeq0
}
\]

That means the Hessian must be positive semidefinite.

Similarly, for a local maximum:

\[
\boxed{
\nabla^2f(x^*)\preceq0
}
\]

---

# 10. Second-Order Sufficient Condition

Suppose:

\[
\nabla f(x^*)=0
\]

and:

\[
\boxed{
\nabla^2f(x^*)\succ0
}
\]

Then:

\[
\boxed{x^*\text{ is a strict local minimum}}
\]

Similarly, if:

\[
\nabla f(x^*)=0
\]

and:

\[
\boxed{
\nabla^2f(x^*)\prec0
}
\]

then:

\[
\boxed{x^*\text{ is a strict local maximum}}
\]

---

# 11. Complete Second-Order Test

At a stationary point \(x^*\):

### Case 1 — Positive definite Hessian

\[
H(x^*)\succ0
\]

Then:

\[
\boxed{\text{Strict local minimum}}
\]

---

### Case 2 — Negative definite Hessian

\[
H(x^*)\prec0
\]

Then:

\[
\boxed{\text{Strict local maximum}}
\]

---

### Case 3 — Indefinite Hessian

\[
H(x^*)\text{ is indefinite}
\]

Then:

\[
\boxed{\text{Saddle point}}
\]

---

### Case 4 — Positive semidefinite Hessian

\[
H(x^*)\succeq0
\]

The second-order test is inconclusive in general.

Additional analysis is required.

---

### Case 5 — Negative semidefinite Hessian

\[
H(x^*)\preceq0
\]

Again, the second-order test is generally inconclusive.

---

# 12. Summary Table

| Gradient | Hessian | Result |
|---|---|---|
| \(0\) | \(H\succ0\) | Strict local minimum |
| \(0\) | \(H\prec0\) | Strict local maximum |
| \(0\) | Indefinite | Saddle point |
| \(0\) | \(H\succeq0\) | Inconclusive in general |
| \(0\) | \(H\preceq0\) | Inconclusive in general |
| \(\neq0\) | Any | Not an interior local optimum |

---

# 13. Two-Variable Second-Order Test

For:

\[
f(x_1,x_2)
\]

the Hessian is:

\[
H=
\begin{bmatrix}
f_{x_1x_1} & f_{x_1x_2}\\
f_{x_2x_1} & f_{x_2x_2}
\end{bmatrix}
\]

Define:

\[
D=
\det(H)
\]

or:

\[
D=
f_{x_1x_1}f_{x_2x_2}
-
(f_{x_1x_2})^2
\]

At a stationary point:

### If:

\[
D>0
\]

and:

\[
f_{x_1x_1}>0
\]

then:

\[
\boxed{\text{Local minimum}}
\]

### If:

\[
D>0
\]

and:

\[
f_{x_1x_1}<0
\]

then:

\[
\boxed{\text{Local maximum}}
\]

### If:

\[
D<0
\]

then:

\[
\boxed{\text{Saddle point}}
\]

### If:

\[
D=0
\]

then:

\[
\boxed{\text{Test is inconclusive}}
\]

---

# 14. Example — Local Minimum

Consider:

\[
f(x_1,x_2)=x_1^2+x_2^2
\]

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
x_1=0,\qquad x_2=0
\]

So:

\[
x^*=
\begin{bmatrix}
0\\
0
\end{bmatrix}
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
2,\quad2
\]

Both are positive.

Therefore:

\[
H\succ0
\]

Hence:

\[
\boxed{x^*=(0,0)\text{ is a strict local minimum}}
\]

In fact, it is also the global minimum.

---

# 15. Example — Local Maximum

Consider:

\[
f(x_1,x_2)=-(x_1^2+x_2^2)
\]

Gradient:

\[
\nabla f=
\begin{bmatrix}
-2x_1\\
-2x_2
\end{bmatrix}
\]

Setting it to zero:

\[
x_1=x_2=0
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

# 16. Example — Saddle Point

Consider:

\[
f(x_1,x_2)=x_1^2-x_2^2
\]

Gradient:

\[
\nabla f=
\begin{bmatrix}
2x_1\\
-2x_2
\end{bmatrix}
\]

Stationary point:

\[
x^*=(0,0)
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
2,\quad-2
\]

One is positive and one is negative.

Therefore the Hessian is indefinite.

Hence:

\[
\boxed{(0,0)\text{ is a saddle point}}
\]

---

# 17. Global Minimum

A local minimum is not necessarily a global minimum.

A point \(x^*\) is a global minimum if:

\[
\boxed{
f(x^*)\leq f(x)
}
\]

for every feasible \(x\).

For a convex function:

\[
\boxed{
\nabla^2f(x)\succeq0
}
\]

throughout the domain.

If \(f\) is strictly convex:

\[
\boxed{
\nabla^2f(x)\succ0
}
\]

throughout the domain, then the minimizer is unique if it exists.

---

# 18. Convexity and Optimization

For a twice-differentiable function:

### Convex

If:

\[
\boxed{
\nabla^2f(x)\succeq0
}
\]

for all \(x\), then \(f\) is convex.

### Strictly Convex

If:

\[
\boxed{
\nabla^2f(x)\succ0
}
\]

for all \(x\), then \(f\) is strictly convex.

For a convex differentiable function:

\[
\boxed{
\nabla f(x^*)=0
}
\]

is sufficient for \(x^*\) to be a global minimizer.

For a strictly convex function, the global minimizer is unique.

---

# 19. First-Order vs Second-Order Conditions

| Condition | Meaning |
|---|---|
| \(\nabla f(x^*)=0\) | First-order necessary condition |
| \(H(x^*)\succeq0\) | Second-order necessary condition for minimum |
| \(H(x^*)\preceq0\) | Second-order necessary condition for maximum |
| \(H(x^*)\succ0\) | Strict local minimum |
| \(H(x^*)\prec0\) | Strict local maximum |
| \(H(x^*)\) indefinite | Saddle point |

---

# 20. Exam Procedure for Unconstrained Optimization

Given:

\[
\min f(x)
\]

### Step 1 — Find the gradient

Calculate:

\[
\nabla f(x)
\]

---

### Step 2 — Find stationary points

Solve:

\[
\boxed{\nabla f(x)=0}
\]

---

### Step 3 — Calculate the Hessian

Find:

\[
\boxed{
H(x)=\nabla^2f(x)
}
\]

---

### Step 4 — Evaluate the Hessian

Substitute each stationary point:

\[
H(x^*)
\]

---

### Step 5 — Classify

Use:

- Eigenvalues
- Positive/negative definiteness
- Determinant test for two variables

---

### Step 6 — State the Result

For example:

\[
\boxed{
\nabla f(x^*)=0,\quad H(x^*)\succ0
}
\]

Therefore:

\[
\boxed{x^*\text{ is a strict local minimum}}
\]

---

# 21. Important Formulas

### Gradient

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

### Hessian

\[
\boxed{
H(x)=\nabla^2f(x)
}
\]

### Directional derivative

\[
\boxed{
D_df(x)=\nabla f(x)^Td
}
\]

### Quadratic function

\[
\boxed{
f(x)=\frac12x^TAx+b^Tx+c
}
\]

### Gradient of quadratic function

\[
\boxed{
\nabla f(x)=Ax+b
}
\]

when \(A=A^T\).

### Hessian of quadratic function

\[
\boxed{
\nabla^2f(x)=A
}
\]

### First-order condition

\[
\boxed{
\nabla f(x^*)=0
}
\]

### Second-order minimum condition

\[
\boxed{
\nabla^2f(x^*)\succ0
}
\]

### Second-order maximum condition

\[
\boxed{
\nabla^2f(x^*)\prec0
}
\]

---

# 22. Quick Revision

```text
UNCONSTRAINED OPTIMIZATION

min f(x)
     |
     v
Calculate gradient
     |
     v
∇f(x) = 0
     |
     v
Find stationary points
     |
     v
Calculate Hessian H
     |
     +----------------------+
     |                      |
 H positive definite   H negative definite
     |                      |
     v                      v
Local minimum          Local maximum
     |
     |
 H indefinite
     |
     v
 Saddle point