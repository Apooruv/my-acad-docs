# Complementary Slackness

Complementary Slackness connects the optimal primal solution with
the optimal dual solution.

It is particularly useful for:

- checking optimality;
- finding the dual solution from the primal;
- finding the primal solution from the dual;
- solving duality problems without solving both problems completely.

---

# 1. Basic Idea

At optimality, certain primal constraints can have slack only when
the corresponding dual variable is zero.

Similarly, a primal variable can be positive only when its
corresponding dual constraint is tight.

---

# 2. Primal-Dual Pair

Consider:

$$
\max c^Tx
$$

subject to:

$$
Ax\leq b,\quad x\geq0
$$

and:

$$
\min b^Ty
$$

subject to:

$$
A^Ty\geq c,\quad y\geq0.
$$

---

# 3. First Complementary Slackness Condition

For each primal constraint:

$$
(Ax)_i\leq b_i.
$$

The slack is:

$$
b_i-(Ax)_i.
$$

Complementary slackness requires:

$$
\boxed{
y_i[b_i-(Ax)_i]=0.
}
$$

Therefore:

- if $y_i>0$, the primal constraint must be tight;
- if the primal constraint has positive slack, then $y_i=0$.

---

# 4. Second Complementary Slackness Condition

For each dual constraint:

$$
(A^Ty)_j\geq c_j.
$$

The slack is:

$$
(A^Ty)_j-c_j.
$$

Complementary slackness requires:

$$
\boxed{
x_j[(A^Ty)_j-c_j]=0.
}
$$

Therefore:

- if $x_j>0$, the dual constraint must be tight;
- if the dual constraint has positive slack, then $x_j=0$.

---

# 5. Compact Form

The two conditions are:

$$
\boxed{
y_i[b_i-(Ax)_i]=0
}
$$

for every primal constraint, and:

$$
\boxed{
x_j[(A^Ty)_j-c_j]=0
}
$$

for every dual constraint.

---

# 6. Example

Suppose the primal optimal solution is:

$$
x_1=30,\qquad x_2=30.
$$

For:

$$
2x_1+x_2\leq90
$$

we have:

$$
2(30)+30=90.
$$

The constraint is tight.

For:

$$
x_1+3x_2\leq120
$$

we have:

$$
30+90=120.
$$

This is also tight.

For:

$$
3x_1+2x_2\leq150,
$$

we have:

$$
90+60=150.
$$

All three are tight.

Therefore complementary slackness does not force any of the
corresponding dual variables to zero.

---

# 7. Using Complementary Slackness to Find the Dual

Suppose a primal optimal solution has:

$$
x_1>0,\qquad x_2>0.
$$

Then both corresponding dual constraints must be equalities.

Suppose:

$$
2y_1+y_2+3y_3=40
$$

and:

$$
y_1+3y_2+2y_3=30.
$$

If one primal constraint has slack, its dual variable must be zero.

This can drastically reduce the number of equations that must be
solved.

---

# 8. Practical Procedure

Given a primal optimal solution:

### Step 1

Calculate slack in every primal constraint.

### Step 2

If a primal constraint has positive slack:

$$
y_i=0.
$$

### Step 3

Identify positive primal variables.

For every:

$$
x_j>0,
$$

set the corresponding dual constraint to equality.

### Step 4

Solve the resulting equations.

### Step 5

Check dual feasibility.

### Step 6

Calculate the dual objective.

It should equal the primal optimum.

---

# 9. Key Memory Rule

Remember:

$$
\boxed{
\text{Positive dual variable}
\Rightarrow
\text{primal constraint is tight}
}
$$

and:

$$
\boxed{
\text{Positive primal variable}
\Rightarrow
\text{dual constraint is tight}.
}
$$

The converse is not necessarily true.

A constraint can be tight while its corresponding multiplier is zero.

---

# 10. Exam Question

State complementary slackness.

### Answer

For an optimal primal-dual pair:

$$
\boxed{
y_i[b_i-(Ax)_i]=0
}
$$

and:

$$
\boxed{
x_j[(A^Ty)_j-c_j]=0.
}
$$

These conditions provide necessary and sufficient conditions for
optimality when the primal and dual are feasible.