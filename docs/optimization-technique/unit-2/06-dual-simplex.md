## 4. Dual Simplex Algorithm

### Step 1

Construct the tableau.

Check:

\[ C_j-Z_j`\leq0`{=tex} \]

------------------------------------------------------------------------

### Step 2 --- Choose Leaving Variable

Find a negative RHS.

Usually choose the most negative RHS:

\[ `\boxed{b_r=\min\{b_i:b_i<0\}}`{=tex} \]

The corresponding row is the leaving row.

------------------------------------------------------------------------

### Step 3 --- Find Candidate Entering Variables

In the selected row, only columns satisfying:

\[ `\boxed{a_{rj}<0}`{=tex} \]

can enter.

If there is no negative coefficient in that row:

\[ `\boxed{\text{Infeasible problem}}`{=tex} \]

------------------------------------------------------------------------

### Step 4 --- Ratio Test

For every candidate:

\[ a\_{rj}\<0 \]

calculate:

\[ `\boxed{
\theta_j=
\frac{C_j-Z_j}{a_{rj}}
}`{=tex} \]

Choose the smallest non-negative ratio.

That variable enters.

------------------------------------------------------------------------

### Step 5 --- Pivot

Pivot on the intersection of:

-   selected negative-RHS row
-   selected entering-variable column

------------------------------------------------------------------------

### Step 6 --- Repeat

Recalculate the tableau.

Continue until:

\[ `\boxed{b_i\geq0\quad\forall i}`{=tex} \]

Since dual feasibility has been maintained, the resulting solution is
optimal.

------------------------------------------------------------------------

# 5. Dual Simplex Selection Rule

### Primal Simplex

For max:

\[ `\boxed{\text{largest positive }C_j-Z_j}`{=tex} \]

enters.

Then use:

\[ `\boxed{\frac{b_i}{a_{ij}},\quad a_{ij}>0}`{=tex} \]

for the leaving variable.

### Dual Simplex

Choose:

\[ `\boxed{\text{most negative RHS}}`{=tex} \]

as the leaving row.

Then consider:

\[ `\boxed{a_{ij}<0}`{=tex} \]

and calculate:

\[ `\boxed{
\frac{C_j-Z_j}{a_{ij}}
}`{=tex} \]

Choose the smallest non-negative ratio.

------------------------------------------------------------------------

# 6. Small Example

Consider:

  Basis         (x_1)   (x_2)   (s_1)   (s_2)   RHS
  ----------- ------- ------- ------- ------- -----
  (s_1)             1      -1       1       0    -2
  (s_2)            -1       2       0       1     4
  (C_j-Z_j)        -1      -2       0       0 

We have:

\[ C_j-Z_j=(-1,-2,0,0) \]

so:

\[ C_j-Z_j`\leq0`{=tex} \]

Dual feasibility holds.

But:

\[ RHS=(-2,4) \]

contains a negative value, so the current solution is primal infeasible.

### Leaving variable

Most negative RHS:

\[ -2 \]

Therefore (s_1) leaves.

### Entering variable

Selected row:

\[ \[1,-1,1,0\] \]

Only (x_2) has a negative coefficient:

\[ -1 \]

Therefore (x_2) enters.

### Ratio

\[ `\theta`{=tex}= `\frac{-2}{-1}`{=tex}=2 \]

Thus:

\[ `\boxed{x_2\text{ enters}}`{=tex} \]

\[ `\boxed{s_1\text{ leaves}}`{=tex} \]

and the pivot element is:

\[ `\boxed{-1}`{=tex} \]

------------------------------------------------------------------------

# 7. Infeasibility Test

Suppose a selected row has:

\[ b_i\<0 \]

but every coefficient in that row satisfies:

\[ a\_{ij}`\geq0`{=tex} \]

There is no possible entering variable.

Therefore:

\[ `\boxed{\text{Problem is infeasible}}`{=tex} \]

------------------------------------------------------------------------

# 8. When Is Dual Simplex Useful?

Dual simplex is useful when:

-   An existing optimal solution becomes infeasible.
-   RHS/resource availability changes.
-   A new constraint is added.
-   Re-optimization is required.
-   We want to repair an existing basis rather than start simplex from
    scratch.

------------------------------------------------------------------------

# 9. Dual Simplex --- Exam Algorithm

``` text
1. Construct the tableau.
2. Check Cj - Zj <= 0 for maximization.
3. If all RHS >= 0, the solution is optimal.
4. Select the most negative RHS as the leaving row.
5. In that row, consider only negative coefficients.
6. Compute (Cj - Zj) / aij.
7. Select the smallest non-negative ratio.
8. Pivot.
9. Recalculate the tableau.
10. Repeat until all RHS >= 0.
```

------------------------------------------------------------------------

# 10. Most Important Comparison

  Property             Simplex                           Dual Simplex
  -------------------- --------------------------------- -------------------
  Feasible initially   Primal                            Dual
  Infeasibility        RHS non-negative initially        Some RHS negative
  First selection      Entering variable                 Leaving variable
  Max entering rule    Largest (C_j-Z_j\>0)              Ratio rule
  Row selection        Ratio test                        Most negative RHS
  Candidate columns    (a\_{ij}\>0)                      (a\_{ij}\<0)
  Optimality           (C_j-Z_j`\leq0`{=tex}), RHS ≥ 0   Same

------------------------------------------------------------------------

# Unit II Progress

-   [x] Duality
-   [x] Duality Theorem
-   [x] Primal--Dual Construction
-   [x] Complementary Slackness
-   [x] Sensitivity Analysis
-   [x] Dual Simplex Method
-   [ ] Matrix Calculus
-   [ ] Conditions for Solution of an Unconstrained Problem

## Next

**Matrix Calculus → Gradient → Hessian → Quadratic Forms → First-Order
and Second-Order Conditions for Unconstrained Optimization**
