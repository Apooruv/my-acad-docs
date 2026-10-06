# Optimization Techniques — Unit I Practice Problems and Solutions

## Unit I

Topics covered:

1. Types of Optimization Problems
2. Linear Programming Problems
3. Standard Form Conversion
4. Simplex Method
5. Artificial Variables
6. Big M Method
7. Two-Phase Method
8. Matrix Form
9. Revised Simplex Method
10. Special Cases in LPP

---

# 1. Types of Optimization Problems

## Problem 1

Classify the following optimization problems.

### (a)

Maximize

`Z = 5x1 + 3x2`

subject to

`2x1 + x2 <= 10`

`x1 + 2x2 <= 8`

`x1, x2 >= 0`

### Solution

This is a:

- Linear optimization problem
- Linear Programming Problem (LPP)
- Maximization problem
- Constrained problem
- Continuous-variable problem
- Two-variable problem

---

## Problem 2

Determine whether the following is an LPP.

`Maximize Z = x1^2 + 2x2`

subject to

`x1 + x2 <= 10`

### Solution

It is **not an LPP** because the objective contains `x1^2`.

LPP requires both the objective function and constraints to be linear.

---

# 2. Standard Form Conversion

## Problem 3

Convert the following LPP into standard form.

Maximize

`Z = 3x1 + 5x2`

subject to

`2x1 + x2 <= 8`

`x1 + 3x2 <= 9`

`x1, x2 >= 0`

### Solution

Introduce slack variables `s1` and `s2`.

`2x1 + x2 + s1 = 8`

`x1 + 3x2 + s2 = 9`

Therefore,

Maximize

`Z = 3x1 + 5x2`

subject to

`2x1 + x2 + s1 = 8`

`x1 + 3x2 + s2 = 9`

`x1, x2, s1, s2 >= 0`

---

## Problem 4

Convert the following constraint into standard form.

`3x1 + 2x2 >= 12`

### Solution

For a `>=` constraint, subtract a surplus variable.

`3x1 + 2x2 - s1 = 12`

However, `s1` does not provide an initial basic variable.

Therefore an artificial variable is also required for Simplex-based methods:

`3x1 + 2x2 - s1 + a1 = 12`

---

## Problem 5

Convert the equality constraint

`2x1 + 4x2 = 20`

into a form suitable for Big M / Two-Phase methods.

### Solution

An equality constraint requires an artificial variable:

`2x1 + 4x2 + a1 = 20`

---

## Important Conversion Rules

| Constraint | Standard form |
|---|---|
| `<=` | Add slack: `+s` |
| `>=` | Subtract surplus: `-s`, add artificial variable |
| `=` | Add artificial variable |
| RHS < 0 | Multiply entire constraint by `-1` first |

---

# 3. Simplex Method

## Problem 6 — Basic Simplex Practice

Maximize

`Z = 3x1 + 2x2`

subject to

`x1 + x2 <= 4`

`2x1 + x2 <= 5`

`x1, x2 >= 0`

---

## Step 1: Convert to standard form

`x1 + x2 + s1 = 4`

`2x1 + x2 + s2 = 5`

Initial basis:

`s1, s2`

Initial solution:

`x1 = 0`

`x2 = 0`

`s1 = 4`

`s2 = 5`

`Z = 0`

---

## Step 2: Initial Tableau

| Basis | CB | x1 | x2 | s1 | s2 | RHS |
|---|---:|---:|---:|---:|---:|---:|
| s1 | 0 | 1 | 1 | 1 | 0 | 4 |
| s2 | 0 | 2 | 1 | 0 | 1 | 5 |
| Zj | | 0 | 0 | 0 | 0 | |
| Cj-Zj | | 3 | 2 | 0 | 0 | |

For maximization, select the largest positive `Cj-Zj`.

Therefore:

`x1` enters.

---

## Step 3: Ratio Test

For the `x1` column:

First row:

`4 / 1 = 4`

Second row:

`5 / 2 = 2.5`

Minimum positive ratio:

`2.5`

Therefore:

`s2` leaves.

Pivot:

`2`

---

## Step 4: After Pivot

Divide row 2 by 2:

`R2 -> R2 / 2`

Then eliminate `x1` from row 1.

The resulting rows are:

`R1 = [0, 0.5, 1, -0.5 | 1.5]`

`R2 = [1, 0.5, 0, 0.5 | 2.5]`

Basis:

`s1, x1`

---

## Step 5: Compute Cj-Zj

The new basic costs are:

`CB = [0, 3]`

Therefore:

`Zj(x1) = 3`

`Zj(x2) = 1.5`

`Zj(s1) = 0`

`Zj(s2) = 1.5`

Hence:

`Cj-Zj = [0, 0.5, 0, -1.5]`

Since `x2` has a positive value:

`x2` enters.

---

## Step 6: Ratio Test

For the `x2` column:

First row:

`1.5 / 0.5 = 3`

Second row:

`2.5 / 0.5 = 5`

Therefore:

`s1` leaves.

Pivot:

`0.5`

---

## Final Solution

After the second pivot:

`x1 = 2`

`x2 = 2`

Objective:

`Z = 3(2) + 2(2)`

`Z = 10`

Therefore:

**Optimal solution**

`x1 = 2`

`x2 = 2`

`Zmax = 10`

---

# 4. Lab Problem — Q1

## Problem 7

A furniture company manufactures tables and chairs.

Each table requires:

- 4 hours carpentry
- 2 hours finishing

Each chair requires:

- 3 hours carpentry
- 1 hour finishing

Available:

- 240 hours carpentry
- 100 hours finishing

Profit:

- Table = 70
- Chair = 50

Formulate and solve using Simplex.

---

## Mathematical Model

Maximize

`Z = 70x1 + 50x2`

subject to

`4x1 + 3x2 <= 240`

`2x1 + x2 <= 100`

`x1, x2 >= 0`

---

## Standard Form

`4x1 + 3x2 + s1 = 240`

`2x1 + x2 + s2 = 100`

---

## Simplex Sequence

Initial basis:

`s1, s2`

### Iteration 0

Entering:

`x1`

Leaving:

`s2`

Pivot:

`2`

### Iteration 1

Entering:

`x2`

Leaving:

`s1`

Pivot:

`1`

### Iteration 2

Optimality reached.

---

## Final Answer

`x1 = 30`

`x2 = 40`

`Zmax = 4100`

Verification:

`4(30) + 3(40) = 240`

`2(30) + 40 = 100`

Both constraints are satisfied and tight.

---

# 5. Lab Problem — Q2

## Problem 8

Maximize

`Z = 40x1 + 30x2`

subject to

`2x1 + x2 <= 90`

`x1 + 3x2 <= 120`

`3x1 + 2x2 <= 150`

`x1, x2 >= 0`

---

## Standard Form

`2x1 + x2 + s1 = 90`

`x1 + 3x2 + s2 = 120`

`3x1 + 2x2 + s3 = 150`

---

## Simplex Sequence

### Iteration 0

Entering:

`x1`

Leaving:

`s1`

Pivot:

`2`

### Iteration 1

Entering:

`x2`

Leaving:

`s2`

Pivot:

`2.5`

### Iteration 2

Optimality reached.

---

## Final Answer

`x1 = 30`

`x2 = 30`

`Zmax = 2100`

At the optimum:

`s3 = 0`

The solution is still unique because there is no non-basic variable with zero `Cj-Zj`.

---

# 6. Simplex Optimality Rule

For the convention used in the lab:

### Maximization

If

`Cj - Zj <= 0`

for every column, the current solution is optimal.

### Entering Variable

Choose the variable with the **largest positive `Cj-Zj`**.

### Leaving Variable

Use the minimum positive ratio:

`Ratio = RHS / positive coefficient`

The smallest valid ratio determines the leaving variable.

### Pivot

The intersection of:

- entering-variable column
- leaving-variable row

is the pivot element.

---

# 7. Artificial Variables

## Problem 9

Why are artificial variables required?

### Answer

Consider:

`2x1 + x2 >= 10`

Convert:

`2x1 + x2 - s1 = 10`

There is no obvious identity-column variable that can serve as the initial basic variable.

Therefore introduce:

`2x1 + x2 - s1 + a1 = 10`

The artificial variable `a1` provides an initial basis.

It must eventually be removed from the solution.

---

# 8. Big M Method

## Big M Concept

Artificial variables are given a large penalty.

For a **maximization** problem:

`Artificial variable coefficient = -M`

For a **minimization** problem:

`Artificial variable coefficient = +M`

where `M` is a very large positive number.

The purpose is to force artificial variables out of the final solution.

---

# 9. Big M Practice Problem

## Problem 10 — Diet Problem

Minimize

`Z = 3x1 + 2.5x2`

subject to

`2x1 + 4x2 >= 80`

`4x1 + 2x2 >= 100`

`x1, x2 >= 0`

---

## Step 1: Standard Form

First constraint:

`2x1 + 4x2 - s1 + a1 = 80`

Second constraint:

`4x1 + 2x2 - s2 + a2 = 100`

Because this is a minimization problem:

`Z = 3x1 + 2.5x2 + Ma1 + Ma2`

where `M` is large.

For the lab implementation:

`M = 100000`

---

## Step 2: Artificial Variables

Initial basis:

`a1, a2`

The artificial variables are heavily penalized.

The Simplex iterations drive:

`a1 -> 0`

`a2 -> 0`

---

## Final Answer

`x1 = 20`

`x2 = 10`

Objective:

`Z = 3(20) + 2.5(10)`

`Z = 60 + 25`

`Z = 85`

Therefore:

`Zmin = 85`

---

## Verification

First constraint:

`2(20) + 4(10) = 80`

Second constraint:

`4(20) + 2(10) = 100`

Both constraints are tight.

Artificial variables:

`a1 = 0`

`a2 = 0`

Therefore the solution is feasible.

---

# 10. Big M Practice Problem

## Problem 11 — Production Contract

Minimize

`Z = 50x1 + 40x2`

subject to

`3x1 + 2x2 = 60`

`2x1 + 4x2 >= 40`

`x1, x2 >= 0`

---

## Standard Form

Equality:

`3x1 + 2x2 + a1 = 60`

Greater-than-or-equal constraint:

`2x1 + 4x2 - s1 + a2 = 40`

Objective:

`Min Z = 50x1 + 40x2 + Ma1 + Ma2`

---

## Final Answer

`x1 = 20`

`x2 = 0`

`Zmin = 1000`

Verification:

`3(20) + 2(0) = 60`

`2(20) + 4(0) = 40`

Artificial variables are zero.

The final solution is feasible.

---

# 11. Two-Phase Method

## Basic Idea

Two-Phase Method separates the process into two stages.

### Phase I

Find a feasible solution.

Objective:

`Minimize W = sum of artificial variables`

For example:

`W = a1 + a2`

---

### Phase II

After obtaining:

`W = 0`

remove artificial variables and optimize the original objective.

---

## Important Rule

### If Phase I optimum is:

`W = 0`

A feasible solution exists.

Proceed to Phase II.

### If Phase I optimum is:

`W > 0`

The original LPP is infeasible.

Do not proceed to Phase II.

---

# 12. Two-Phase Practice Problem

## Problem 12 — Investment Allocation

Minimize

`Z = 4x1 + 2x2`

subject to

`x1 + x2 >= 3`

`2x1 - x2 <= 0`

`x1, x2 >= 0`

---

## Standard Form

First constraint:

`x1 + x2 - su1 + a1 = 3`

Second constraint:

`2x1 - x2 + s1 = 0`

---

# Phase I

Minimize:

`W = a1`

Initial artificial variable:

`a1`

The Simplex iterations remove `a1` from the basis.

Phase I result:

`W = 0`

Therefore a feasible solution exists.

---

# Phase II

Remove the artificial variable.

Restore the original objective:

`Min Z = 4x1 + 2x2`

The Phase II iterations produce:

`x1 = 0`

`x2 = 3`

---

## Final Answer

`Z = 4(0) + 2(3)`

`Z = 6`

Therefore:

`x1 = 0`

`x2 = 3`

`Zmin = 6`

---

## Verification

First constraint:

`0 + 3 = 3 >= 3`

Second constraint:

`2(0) - 3 = -3 <= 0`

Therefore the solution is feasible.

---

# 13. Two-Phase Practice Problem

## Problem 13 — Two Production Lines

Minimize

`Z = 2x1 + 3x2`

subject to

`x1 + x2 = 10`

`2x1 + x2 >= 12`

`x1, x2 >= 0`

---

## Standard Form

Equality:

`x1 + x2 + a1 = 10`

Greater-than-or-equal:

`2x1 + x2 - su1 + a2 = 12`

---

# Phase I

Minimize:

`W = a1 + a2`

Initial basis:

`a1, a2`

The Phase I iterations are:

### Iteration 0

Entering:

`x1`

Leaving:

`a2`

Pivot:

`2`

### Iteration 1

Entering:

`x2`

Leaving:

`a1`

Pivot:

`0.5`

### Iteration 2

Phase I optimum:

`W = 0`

Therefore the problem is feasible.

---

# Phase II

Remove:

`a1, a2`

Restore:

`Min Z = 2x1 + 3x2`

Initial Phase II basis:

`x2, x1`

The next pivot is:

Entering:

`su1`

Leaving:

`x2`

Pivot:

`1`

Then optimality is reached.

---

## Final Answer

`x1 = 10`

`x2 = 0`

`Zmin = 20`

---

## Verification

Equality constraint:

`10 + 0 = 10`

Second constraint:

`2(10) + 0 = 20 >= 12`

Objective:

`Z = 2(10) + 3(0)`

`Z = 20`

Therefore the solution is feasible and optimal.

---

# 14. Big M vs Two-Phase

| Feature | Big M | Two-Phase |
|---|---|---|
| Artificial variables | Yes | Yes |
| Phase I | No | Yes |
| Large `M` required | Yes | No |
| Artificial variables penalized | Directly in objective | Minimized separately |
| Numerical issues | Can occur because of large M | Usually cleaner |
| Feasibility check | Artificial variables must leave | Phase I objective must become 0 |

---

# 15. Matrix Form of LPP

A standard equality-form maximization problem can be written as:

`Max Z = c^T x`

subject to

`Ax = b`

`x >= 0`

where:

- `A` = constraint coefficient matrix
- `x` = variable vector
- `b` = RHS vector
- `c` = objective coefficient vector

---

# 16. Matrix Form Practice Problem

## Problem 14

Write the following LPP in matrix form.

Maximize

`Z = 4x1 + 3x2`

subject to

`2x1 + x2 <= 10`

`x1 + 2x2 <= 8`

`x1, x2 >= 0`

---

## Solution

Introduce slack variables:

`2x1 + x2 + s1 = 10`

`x1 + 2x2 + s2 = 8`

Define

`x = [x1, x2, s1, s2]^T`

Then:

`c = [4, 3, 0, 0]^T`

`A = [[2, 1, 1, 0],`

`     [1, 2, 0, 1]]`

`b = [10, 8]^T`

Therefore:

`Max Z = c^T x`

subject to

`Ax = b`

`x >= 0`

---

# 17. Basis Matrix

Suppose:

`Ax = b`

and the basic variables correspond to columns forming:

`B`

Then:

`Bx_B = b`

Therefore:

`x_B = B^-1 b`

This gives the current basic solution.

---

# 18. Revised Simplex Method

## Important Formulas

Given basis matrix `B`:

### Basic solution

`x_B = B^-1 b`

### Dual multipliers

`y^T = C_B B^-1`

### Zj

`Zj = y^T a_j`

### Reduced cost

`Cj - Zj = Cj - y^T a_j`

For maximization:

`Cj - Zj <= 0`

is the optimality condition.

---

# 19. Revised Simplex Practice Problem

## Problem 15

Use the following LPP:

Maximize

`Z = 40x1 + 30x2`

subject to

`2x1 + x2 <= 90`

`x1 + 3x2 <= 120`

`3x1 + 2x2 <= 150`

`x1, x2 >= 0`

---

## Standard Form

`2x1 + x2 + s1 = 90`

`x1 + 3x2 + s2 = 120`

`3x1 + 2x2 + s3 = 150`

Initial basis:

`B = [s1, s2, s3]`

Therefore:

`B = I`

and

`B^-1 = I`

---

## Initial Basic Solution

`x_B = B^-1b`

Therefore:

`x_B = [90, 120, 150]^T`

---

## First Entering Variable

Objective coefficients:

`Cj = [40, 30, 0, 0, 0]`

Initial:

`CB = [0,0,0]`

Therefore:

`y^T = C_B B^-1 = [0,0,0]`

Thus:

`Cj-Zj = [40,30,0,0,0]`

Largest positive value:

`40`

Therefore:

`x1` enters.

---

## Direction Vector

The `x1` column is:

`a1 = [2,1,3]^T`

Therefore:

`d = B^-1 a1`

Since `B^-1 = I`:

`d = [2,1,3]^T`

---

## Ratio Test

`90/2 = 45`

`120/1 = 120`

`150/3 = 50`

Minimum:

`45`

Therefore:

`s1` leaves.

---

## Next Iteration

After the basis updates:

`B = [x1, s2, s3]`

Continue calculating:

`B^-1`

`x_B = B^-1b`

`y^T = C_BB^-1`

`Cj-Zj`

until all reduced costs satisfy:

`Cj-Zj <= 0`

---

## Final Answer

The optimal solution is:

`x1 = 30`

`x2 = 30`

`Z = 2100`

---

# 20. Revised Simplex vs Ordinary Simplex

| Ordinary Simplex | Revised Simplex |
|---|---|
| Uses complete tableau | Uses basis matrix |
| More calculations stored | More compact |
| Tableau explicitly maintained | Uses `B^-1` |
| Easy to display manually | Efficient for larger problems |
| Same optimality principle | Same optimality principle |

---

# 21. Special Cases

## 21.1 Degeneracy

A basic variable has value:

`0`

at a basic feasible solution.

Example:

`x_B = [5, 0, 10]`

The second basic variable is zero.

This is a degenerate basic solution.

---

# 22. Multiple Optimal Solutions

For a maximization problem, if an optimal tableau contains a **non-basic variable** with:

`Cj-Zj = 0`

then an alternate optimal solution may exist.

Important:

A zero reduced cost must correspond to a **non-basic variable**.

---

# 23. Unbounded Solution

Suppose a variable has:

`Cj-Zj > 0`

and is therefore selected to enter.

If every coefficient in its column is:

`<= 0`

then no valid positive ratio exists.

Therefore the objective can increase indefinitely.

Hence:

**The LPP is unbounded.**

---

# 24. Infeasible Solution

In Big M:

If an artificial variable remains positive in the final solution, the original problem is infeasible.

In Two-Phase:

If

`W* > 0`

after Phase I, the original LPP is infeasible.

---

# 25. Practice — Identify the Special Case

## Problem 16

An optimal Simplex tableau has a non-basic variable `x3` with:

`C3-Z3 = 0`

What does this indicate?

### Answer

An **alternate optimal solution may exist**.

---

## Problem 17

During maximization, an entering variable has:

`Cj-Zj = 8`

but all coefficients in its column are non-positive.

What is the result?

### Answer

The problem is **unbounded**.

---

## Problem 18

After Phase I:

`W = 5`

What is the conclusion?

### Answer

The original LPP is **infeasible**.

---

## Problem 19

A basic variable has value zero at the final solution.

What is this called?

### Answer

**Degeneracy.**

---

# 26. Exam-Oriented Mixed Problems

## Problem 20

Determine which method should be used.

### (a)

Maximize

`Z = 5x1 + 4x2`

subject to only `<=` constraints with positive RHS.

### Answer

**Simplex Method**

---

### (b)

An LPP contains `>=` and `=` constraints and the Big M approach is requested.

### Answer

**Big M Method**

---

### (c)

An LPP contains artificial variables and the question asks for Phase I and Phase II.

### Answer

**Two-Phase Method**

---

### (d)

A large LPP asks for a basis matrix and `B^-1`.

### Answer

**Revised Simplex Method**

---

# 27. Complete Exam Problem

## Problem 21

Maximize

`Z = 5x1 + 4x2`

subject to

`6x1 + 4x2 <= 24`

`x1 + 2x2 <= 6`

`x1, x2 >= 0`

---

## Step 1 — Standard Form

`6x1 + 4x2 + s1 = 24`

`x1 + 2x2 + s2 = 6`

---

## Step 2 — Initial Tableau

Basis:

`s1, s2`

`CB = [0,0]`

`Cj = [5,4,0,0]`

Therefore:

`Zj = [0,0,0,0]`

`Cj-Zj = [5,4,0,0]`

Entering:

`x1`

---

## Step 3 — Ratio Test

`24/6 = 4`

`6/1 = 6`

Therefore:

`s1` leaves.

Pivot:

`6`

---

## Step 4

After pivoting, calculate the new:

- Basis
- CB
- Zj
- Cj-Zj
- RHS

If a positive reduced cost remains, continue.

---

## Final Answer

The optimal solution is:

`x1 = 3`

`x2 = 1.5`

`Z = 5(3) + 4(1.5)`

`Z = 21`

---

# 28. Quick Revision Sheet

## Standard Form

`<=` → `+ slack`

`>=` → `- surplus + artificial`

`=` → `+ artificial`

---

## Simplex

For maximization:

`Cj-Zj <= 0` → optimal

Entering:

`largest positive Cj-Zj`

Leaving:

`minimum positive RHS / pivot-column coefficient`

---

## Big M

Artificial variable receives:

`-M` for maximization

`+M` for minimization

Artificial variables must be zero in the final feasible solution.

---

## Two-Phase

### Phase I

Minimize:

`W = sum of artificial variables`

If:

`W = 0`

→ feasible

If:

`W > 0`

→ infeasible

### Phase II

Restore original objective and optimize.

---

## Matrix Form

`Max Z = c^T x`

subject to

`Ax = b`

`x >= 0`

---

## Revised Simplex

`x_B = B^-1b`

`y^T = C_BB^-1`

`Zj = y^Ta_j`

`Cj-Zj = Cj-y^Ta_j`

---

## Special Cases

| Condition | Result |
|---|---|
| All `Cj-Zj <= 0` | Optimal |
| Positive reduced cost, no positive ratio | Unbounded |
| Non-basic zero reduced cost at optimum | Alternate optimum may exist |
| Basic variable = 0 | Degeneracy |
| Phase I `W > 0` | Infeasible |

---

# 29. Final Unit I Practice Checklist

Before the exam, make sure you can solve these without notes:

- [ ] Identify whether a problem is an LPP
- [ ] Convert `<=` constraints to standard form
- [ ] Convert `>=` constraints
- [ ] Handle equality constraints
- [ ] Construct an initial Simplex tableau
- [ ] Calculate `Zj`
- [ ] Calculate `Cj-Zj`
- [ ] Select entering variable
- [ ] Perform ratio test
- [ ] Select leaving variable
- [ ] Perform pivot operations
- [ ] Detect optimality
- [ ] Detect degeneracy
- [ ] Detect alternate optimum
- [ ] Detect unboundedness
- [ ] Detect infeasibility
- [ ] Construct Big M tableau
- [ ] Explain artificial variables
- [ ] Solve Phase I
- [ ] Decide whether Phase II is possible
- [ ] Solve Phase II
- [ ] Convert an LPP to matrix form
- [ ] Calculate `B^-1`
- [ ] Calculate `x_B = B^-1b`
- [ ] Calculate `y^T = C_BB^-1`
- [ ] Calculate reduced costs
- [ ] Apply Revised Simplex