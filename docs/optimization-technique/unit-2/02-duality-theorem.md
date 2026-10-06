# The Duality Theorem

The Duality Theorem establishes the relationship between the
optimal values of the primal and dual problems.

There are three central ideas:

1. Weak Duality
2. Strong Duality
3. Complementary Slackness

---

# 1. Weak Duality Theorem

Consider a primal maximization problem:

$$
\max c^Tx
$$

subject to:

$$
Ax\leq b,\quad x\geq0.
$$

Its dual is:

$$
\min b^Ty
$$

subject to:

$$
A^Ty\geq c,\quad y\geq0.
$$

For **any feasible primal solution** $x$ and **any feasible dual
solution** $y$:

$$
\boxed{
c^Tx\leq b^Ty.
}
$$

This is the Weak Duality Theorem.

---

# 2. Why Is This Important?

Suppose we have:

Primal feasible solution:

$$
Z=100
$$

and dual feasible solution:

$$
W=120.
$$

Weak duality guarantees:

$$
100\leq120.
$$

Therefore the dual objective gives an upper bound on the primal
maximization problem.

Similarly, the primal gives a lower bound on the dual minimization
problem.

---

# 3. Proof of Weak Duality

Since the dual is feasible:

$$
A^Ty\geq c.
$$

Since:

$$
x\geq0,
$$

multiplying by $x^T$ preserves the inequality:

$$
x^TA^Ty\geq x^Tc.
$$

But:

$$
x^TA^Ty=(Ax)^Ty.
$$

Since the primal is feasible:

$$
Ax\leq b.
$$

and:

$$
y\geq0,
$$

we obtain:

$$
(Ax)^Ty\leq b^Ty.
$$

Therefore:

$$
x^Tc\leq b^Ty.
$$

Since:

$$
x^Tc=c^Tx,
$$

we obtain:

$$
\boxed{
c^Tx\leq b^Ty.
}
$$

---

# 4. Strong Duality Theorem

If the primal and dual have optimal feasible solutions, then:

$$
\boxed{
Z^*=W^*
}
$$

where:

- $Z^*$ = optimal primal objective;
- $W^*$ = optimal dual objective.

Therefore:

$$
\boxed{
\text{Optimal primal value}
=
\text{Optimal dual value}.
}
$$

This is the Strong Duality Theorem.

---

# 5. Why Strong Duality Matters

Suppose we solve the primal and obtain:

$$
Z^*=2100.
$$

Then the optimal dual solution must satisfy:

$$
W^*=2100.
$$

Therefore solving either problem can provide the optimal objective
value of the other.

---

# 6. Weak vs Strong Duality

| Property | Weak Duality | Strong Duality |
|---|---|---|
| Applies to feasible solutions | Yes | Optimal solutions |
| Relationship | $Z\leq W$ | $Z^*=W^*$ |
| Gives bound | Yes | Exact optimum |
| Main use | Verify bounds | Verify optimality |

---

# 7. Example

Suppose a primal maximization problem produces:

$$
Z=1800.
$$

Suppose a feasible dual solution produces:

$$
W=2000.
$$

Then:

$$
1800\leq2000.
$$

This is consistent with Weak Duality.

But this does **not** prove that either solution is optimal.

If we find another primal solution with:

$$
Z=2000
$$

then we have:

$$
Z=W=2000.
$$

Therefore both are optimal.

---

# 8. Optimality Certificate

Suppose:

- $x$ is primal feasible;
- $y$ is dual feasible;
- $c^Tx=b^Ty$.

Then both are optimal.

This is extremely useful in examinations.

To prove optimality, you can provide:

$$
\boxed{
\text{Primal feasible}
+
\text{Dual feasible}
+
\text{equal objective values}.
}
$$

---

# 9. Important Result

For a primal maximization problem and its dual minimization
problem:

$$
\boxed{
Z_{\text{primal}}\leq W_{\text{dual}}
}
$$

for any feasible pair.

At optimum:

$$
\boxed{
Z^*=W^*.
}
$$

---

# 10. Infeasibility and Unboundedness

Duality also provides useful relationships.

For the standard primal-dual pair:

### If primal is unbounded

The dual cannot have a feasible solution.

### If dual is unbounded

The primal cannot have a feasible solution.

### If both are feasible

Their optimal objective values are equal.

---

# 11. Exam Questions

## Q1. State Weak Duality.

For every feasible primal solution $x$ and feasible dual solution $y$:

$$
\boxed{
c^Tx\leq b^Ty.
}
$$

---

## Q2. State Strong Duality.

If optimal feasible solutions exist:

$$
\boxed{
Z^*=W^*.
}
$$

---

## Q3. How can you prove that a solution is optimal?

Show:

1. primal feasibility;
2. dual feasibility;
3. equal objective values.

---

# 12. Quick Memory Trick

Weak:

$$
\boxed{
\text{Primal value}\leq\text{Dual value}
}
$$

Strong:

$$
\boxed{
\text{Primal optimum}=\text{Dual optimum}
}
$$