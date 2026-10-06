# 05 — Sensitivity Analysis

## 1. What is Sensitivity Analysis?

Sensitivity analysis studies:

> What happens to the optimal solution when the coefficients or resources of an LPP change?

After solving an LPP, we may ask:

- What if the available resources increase?
- What if a profit coefficient changes?
- What is the value of one additional unit of a resource?
- How much can a coefficient change before the current solution stops being optimal?

---

## 2. RHS Sensitivity

Consider:

\[
\max Z=c^Tx
\]

subject to

\[
Ax=b,\qquad x\geq0
\]

Suppose the current basis is \(B\).

The basic solution is:

\[
x_B=B^{-1}b
\]

If the RHS changes:

\[
b\rightarrow b+\Delta b
\]

then:

\[
x_B'=B^{-1}(b+\Delta b)
\]

Therefore:

\[
\boxed{x_B'=x_B+B^{-1}\Delta b}
\]

The current basis remains feasible if:

\[
x_B'\geq0
\]

---

## 3. Shadow Price

The dual variable \(y_i\) associated with constraint \(i\) is called its **shadow price**.

It represents the change in the optimal objective value caused by increasing the RHS of constraint \(i\) by one unit, provided the current basis remains valid.

\[
y^T=C_BB^{-1}
\]

If:

\[
y_i=18
\]

then one additional unit of that resource increases the objective by 18 units within the allowable range.

---

## 4. Dual Simplex

Ordinary simplex starts with a primal-feasible solution.

Dual simplex starts with:

\[
\boxed{\text{Dual feasible}}
\]

but:

\[
\boxed{\text{Primal infeasible}}
\]

It restores primal feasibility while maintaining dual feasibility.

For the maximization convention used in the lab:

\[
C_j-Z_j\leq0
\]

### Algorithm

1. Check \(C_j-Z_j\leq0\).
2. Find the most negative RHS.
3. That row is the leaving row.
4. Consider only columns with \(a_{ij}<0\).
5. Calculate:

\[
\frac{C_j-Z_j}{a_{ij}}
\]

6. Choose the smallest non-negative ratio.
7. Pivot.
8. Repeat until all RHS values are non-negative.

If a negative RHS row contains no negative coefficient, the problem is infeasible.

---

## Simplex vs Dual Simplex

| Property | Simplex | Dual Simplex |
|---|---|---|
| Initial primal feasibility | Yes | No |
| Initial dual feasibility | Not necessarily | Yes |
| First selection | Entering variable | Leaving variable |
| Row selection | Ratio test | Most negative RHS |
| Candidate columns | \(a_{ij}>0\) | \(a_{ij}<0\) |
| Final condition | RHS ≥ 0 and \(C_j-Z_j\leq0\) | Same |