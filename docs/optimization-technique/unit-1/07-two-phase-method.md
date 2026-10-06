# Two-Phase Method

The Two-Phase Method is another technique for handling artificial
variables.

Instead of assigning a large numerical penalty $M$, it separates
the solution process into two phases.

---

# 1. Basic Idea

The method has two stages:

### Phase I

Find a feasible solution to the original constraints by minimizing
the sum of artificial variables.

### Phase II

Once a feasible basis has been obtained, remove the artificial
variables and optimize the original objective function.

---

# 2. Phase I Objective

Suppose artificial variables are

$$
a_1,a_2,\ldots,a_k.
$$

For Phase I, define:

$$
\boxed{
\min W=a_1+a_2+\cdots+a_k
}
$$

The goal is to drive all artificial variables to zero.

---

# 3. Phase I Decision

At the end of Phase I:

### Case 1

$$
W^*=0.
$$

A feasible solution to the original LPP exists.

Proceed to Phase II.

### Case 2

$$
W^*>0.
$$

The original LPP is infeasible.

Stop.

---

# 4. Phase II

If

$$
W^*=0,
$$

remove all artificial variables and restore the original objective:

$$
\max Z=c^Tx
$$

or

$$
\min Z=c^Tx.
$$

Then continue with the ordinary Simplex Method.

---

# 5. Worked Example

Consider:

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

## Step 1 — Convert Constraints

First constraint:

$$
x_1+x_2+s_1=4.
$$

Second constraint:

$$
x_1+2x_2-s_2+a_1=6.
$$

Initial basis:

$$
s_1,a_1.
$$

---

# Phase I

## Step 2 — Define Phase I Objective

There is one artificial variable:

$$
\boxed{\min W=a_1}
$$

Equivalently, we can maximize

$$
-W=-a_1.
$$

The latter allows use of the maximization tableau convention.

---

## Step 3 — Construct Initial Tableau

The basis is:

$$
s_1,a_1.
$$

Phase I objective coefficients:

$$
C_B=0,-1.
$$

The initial artificial variable has positive value.

The Simplex iterations are now performed to minimize the sum of
artificial variables.

The objective is to drive:

$$
a_1\rightarrow0.
$$

---

## Step 4 — Phase I Result

If the final Phase I objective is:

$$
W^*=0,
$$

the original problem is feasible.

For this problem, a feasible point is:

$$
(x_1,x_2)=(2,2).
$$

Check:

$$
2+2=4
$$

and

$$
2+2(2)=6.
$$

Therefore the constraints are simultaneously satisfied.

Hence:

$$
W^*=0.
$$

---

# Phase II

## Step 5 — Restore Original Objective

Original objective:

$$
\max Z=3x_1+2x_2.
$$

Remove the artificial variable.

Continue using the ordinary Simplex Method.

At the optimal solution:

$$
x_1=2,\qquad x_2=2.
$$

Therefore:

$$
Z=3(2)+2(2)
$$

$$
=6+4
$$

$$
\boxed{Z_{\max}=10}.
$$

---

# 6. Big-M vs Two-Phase

| Feature | Big-M | Two-Phase |
|---|---|---|
| Artificial variables | Yes | Yes |
| Large $M$ | Yes | No |
| Number of conceptual stages | One | Two |
| Phase I | No | Find feasibility |
| Phase II | No | Optimize original objective |
| Numerical stability | Can be awkward | Generally cleaner |

---

# 7. Two-Phase Algorithm

## Phase I

1. Convert the LPP to equality form.
2. Introduce artificial variables.
3. Form

$$
\min W=\sum a_i.
$$

4. Solve the Phase I problem using Simplex.
5. Check the optimal value.

If

$$
W^*>0,
$$

stop: infeasible.

If

$$
W^*=0,
$$

continue.

---

## Phase II

1. Remove artificial variables.
2. Restore the original objective.
3. Use the Phase I basis as the starting basis.
4. Continue Simplex.
5. Stop when the optimality condition is satisfied.

---

# 8. Important Exam Question

### Why is Phase I necessary?

Because the original objective function does not guarantee that
artificial variables will be removed.

Phase I explicitly attempts to eliminate them.

---

# 9. Key Result

The most important condition is:

$$
\boxed{
W^*=0
\Rightarrow
\text{feasible original LPP}
}
$$

and

$$
\boxed{
W^*>0
\Rightarrow
\text{infeasible original LPP}
}
$$

---

# Practice Problems

## Problem 1

Solve using the Two-Phase Method:

$$
\max Z=3x_1+2x_2
$$

subject to

$$
x_1+x_2\geq4
$$

$$
x_1+2x_2\leq6
$$

$$
x_1,x_2\geq0.
$$

---

## Problem 2

Solve:

$$
\max Z=2x_1+3x_2
$$

subject to

$$
x_1+x_2=4
$$

$$
2x_1+x_2\geq5
$$

$$
x_1,x_2\geq0.
$$

---

## Problem 3

Determine whether the following LPP is feasible using Phase I:

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

# Final Comparison

The three important ideas are:

$$
\boxed{
\begin{array}{c}
\text{Simplex}\\
\downarrow\\
\text{Requires an initial BFS}\\
\downarrow\\
\text{Artificial variables if BFS unavailable}\\
\downarrow\\
\begin{cases}
\text{Big-M}\\
\text{Two-Phase}
\end{cases}
\end{array}
}
$$

Big-M removes artificial variables by assigning them a large penalty.

Two-Phase removes artificial variables by first solving a separate
feasibility problem.