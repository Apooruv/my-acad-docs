# Standard Form of a Linear Programming Problem

The Simplex Method works on an LPP after it has been transformed
into an appropriate standard form.

The conversion of an arbitrary LPP into standard form is therefore
an essential step.

---

# 1. Why Standard Form?

An LPP may initially contain:

- maximization or minimization objective;
- $\leq$ constraints;
- $\geq$ constraints;
- equality constraints;
- negative RHS values;
- unrestricted variables.

The Simplex Method requires a systematic representation.

Therefore, we transform the original problem before constructing
the Simplex tableau.

---

# 2. Standard Form

A commonly used standard form for a maximization LPP is:

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
x\geq0
}
$$

with

$$
b\geq0.
$$

Thus, the standard form has:

1. maximization objective;
2. equality constraints;
3. non-negative variables;
4. non-negative RHS values.

---

# 3. Converting a Minimization Problem

Suppose

$$
\min Z=f(x).
$$

Define

$$
Z'=-Z.
$$

Then

$$
\max Z'=-\min Z.
$$

Therefore,

$$
\boxed{
\min Z
\quad\Longleftrightarrow\quad
\max(-Z)
}
$$

After solving the maximization problem,

$$
Z=-Z'.
$$

---

# Worked Example 1 — Minimization to Maximization

Convert

$$
\min Z=4x_1+3x_2
$$

into maximization form.

Define

$$
Z'=-Z.
$$

Therefore,

$$
\boxed{
\max Z'=-4x_1-3x_2
}
$$

The constraints remain unchanged.

---

# 4. Converting $\leq$ Constraints

For

$$
a_1x_1+a_2x_2\leq b,
$$

introduce a non-negative slack variable $s$:

$$
s\geq0.
$$

Then

$$
\boxed{
a_1x_1+a_2x_2+s=b
}
$$

The slack variable measures unused resource.

---

## Example

Convert

$$
2x_1+3x_2\leq10.
$$

Introduce $s_1\geq0$:

$$
\boxed{
2x_1+3x_2+s_1=10
}
$$

---

# 5. Converting $\geq$ Constraints

For

$$
a_1x_1+a_2x_2\geq b,
$$

subtract a non-negative surplus variable:

$$
s\geq0.
$$

Then

$$
\boxed{
a_1x_1+a_2x_2-s=b
}
$$

---

## Example

Convert

$$
3x_1+2x_2\geq12.
$$

Introduce surplus variable $s_1$:

$$
\boxed{
3x_1+2x_2-s_1=12
}
$$

However, this usually does **not** provide an obvious initial
basic variable.

An artificial variable may therefore be required when applying
Simplex.

---

# 6. Converting Equality Constraints

An equality constraint is already in equality form.

For

$$
a_1x_1+a_2x_2=b,
$$

no slack or surplus variable is required.

However, an artificial variable may be needed to construct an
initial basis for the Simplex Method.

---

# 7. Artificial Variables

Consider

$$
x_1+x_2=5.
$$

There is no slack variable that can directly provide an identity
column.

Introduce an artificial variable $a_1$:

$$
\boxed{
x_1+x_2+a_1=5
}
$$

The artificial variable is temporary.

It is used only to obtain an initial basic solution and must
eventually be removed.

Methods for handling artificial variables include:

- Big-M Method
- Two-Phase Method

---

# 8. Negative RHS

If a constraint has a negative RHS,

$$
a_1x_1+a_2x_2=-b,
\qquad b>0,
$$

multiply the entire constraint by $-1$:

$$
-a_1x_1-a_2x_2=b.
$$

The inequality direction must also reverse.

---

## Example

Given

$$
2x_1-3x_2\geq-6,
$$

multiply by $-1$:

$$
-2x_1+3x_2\leq6.
$$

---

# 9. Free or Unrestricted Variables

Suppose a variable can take positive, negative, or zero values:

$$
x_j\text{ unrestricted in sign}.
$$

Represent it as

$$
\boxed{
x_j=x_j^+-x_j^-
}
$$

where

$$
x_j^+\geq0,
\qquad
x_j^-\geq0.
$$

Thus an unrestricted variable is replaced by two
non-negative variables.

---

## Example

Suppose

$$
x_2
$$

is unrestricted.

Write

$$
\boxed{
x_2=x_2^+-x_2^-
}
$$

with

$$
x_2^+,x_2^-\geq0.
$$

---

# 10. Complete Conversion Procedure

To convert an arbitrary LPP into standard form:

### Step 1

Make the objective a maximization problem.

---

### Step 2

Ensure all RHS values are non-negative.

---

### Step 3

Convert every inequality into equality.

For $\leq$:

$$
+\text{slack variable}.
$$

For $\geq$:

$$
-\text{surplus variable}.
$$

---

### Step 4

Handle equality constraints.

Introduce artificial variables when an initial basis is required.

---

### Step 5

Replace unrestricted variables.

Use

$$
x=x^+-x^-.
$$

---

### Step 6

Ensure all variables are non-negative.

---

# Worked Problem 1 — Complete Conversion

Convert the following LPP into standard form:

$$
\min Z=4x_1+3x_2
$$

subject to

$$
x_1+2x_2\geq8
$$

$$
3x_1+2x_2\geq12
$$

$$
x_1,x_2\geq0.
$$

---

## Step 1 — Convert minimization

Define

$$
Z'=-Z.
$$

Therefore,

$$
\boxed{
\max Z'=-4x_1-3x_2
}
$$

---

## Step 2 — Convert first constraint

Original:

$$
x_1+2x_2\geq8.
$$

Subtract surplus variable $s_1$:

$$
x_1+2x_2-s_1=8.
$$

---

## Step 3 — Convert second constraint

Original:

$$
3x_1+2x_2\geq12.
$$

Subtract surplus variable $s_2$:

$$
3x_1+2x_2-s_2=12.
$$

---

## Step 4 — Initial basis issue

The surplus-variable columns contain $-1$, not $+1$.

Therefore, they do not directly provide the required identity
columns for a basic solution.

Introduce artificial variables $a_1,a_2$:

$$
x_1+2x_2-s_1+a_1=8
$$

$$
3x_1+2x_2-s_2+a_2=12.
$$

---

## Final Form

$$
\boxed{
\begin{aligned}
\max\quad
&Z'=-4x_1-3x_2+0s_1+0s_2-Ma_1-Ma_2\\
\text{s.t.}\quad
&x_1+2x_2-s_1+a_1=8\\
&3x_1+2x_2-s_2+a_2=12\\
&x_1,x_2,s_1,s_2,a_1,a_2\geq0.
\end{aligned}
}
$$

The $-M$ terms belong to the Big-M treatment and will be
explained in the Artificial Variables / Big-M topic.

---

# Worked Problem 2 — Mixed Constraints

Convert:

$$
\max Z=3x_1+2x_2
$$

subject to

$$
x_1+2x_2\leq8
$$

$$
2x_1+x_2\geq6
$$

$$
x_1+x_2=5
$$

$$
x_1,x_2\geq0.
$$

---

## Step 1 — First constraint

For

$$
x_1+2x_2\leq8
$$

add slack variable $s_1$:

$$
x_1+2x_2+s_1=8.
$$

---

## Step 2 — Second constraint

For

$$
2x_1+x_2\geq6
$$

subtract surplus variable $s_2$:

$$
2x_1+x_2-s_2=6.
$$

An artificial variable $a_2$ is required for the initial basis:

$$
2x_1+x_2-s_2+a_2=6.
$$

---

## Step 3 — Third constraint

The equality

$$
x_1+x_2=5
$$

requires an artificial variable:

$$
x_1+x_2+a_3=5.
$$

---

## Final Equality Form

$$
\boxed{
\begin{aligned}
\max\quad
Z={}&3x_1+2x_2\\
\text{s.t.}\quad
&x_1+2x_2+s_1=8\\
&2x_1+x_2-s_2+a_2=6\\
&x_1+x_2+a_3=5\\
&x_1,x_2,s_1,s_2,a_2,a_3\geq0.
\end{aligned}
}
$$

---

# 11. Slack vs Surplus vs Artificial

| Variable | Constraint | Operation | Purpose |
|---|---|---|---|
| Slack | $\leq$ | Add | Convert inequality to equality |
| Surplus | $\geq$ | Subtract | Convert inequality to equality |
| Artificial | $=$ or $\geq$ | Add | Obtain initial basis |

Remember:

$$
\leq\quad\Rightarrow\quad +s
$$

$$
\geq\quad\Rightarrow\quad -s
$$

Artificial variables are introduced when necessary to construct
an initial basis.

---

# 12. Standard Form Checklist

Before constructing a Simplex tableau, check:

- [ ] Objective is in required max/min form
- [ ] RHS values are non-negative
- [ ] All constraints are equalities
- [ ] Slack variables added to $\leq$
- [ ] Surplus variables subtracted from $\geq$
- [ ] Artificial variables introduced where required
- [ ] Unrestricted variables replaced
- [ ] Every variable is non-negative

---

# Exam Trap

Do not confuse:

$$
\leq
$$

with

$$
\geq.
$$

For example:

$$
2x_1+x_2\leq10
$$

becomes

$$
2x_1+x_2+s=10,
$$

while

$$
2x_1+x_2\geq10
$$

becomes

$$
2x_1+x_2-s=10.
$$

The sign of the added variable is different.

---

# Quick Revision

### Minimization

$$
\min Z
\Rightarrow
\max(-Z)
$$

### $\leq$ constraint

$$
Ax\leq b
\Rightarrow
Ax+s=b
$$

### $\geq$ constraint

$$
Ax\geq b
\Rightarrow
Ax-s=b
$$

### Equality

$$
Ax=b
$$

May require an artificial variable for Simplex initialization.

### Unrestricted variable

$$
x=x^+-x^-,
\qquad
x^+,x^-\geq0.
$$

---

# Practice Problems

## Problem 1

Convert to standard form:

$$
\max Z=5x_1+4x_2
$$

subject to

$$
2x_1+x_2\leq10
$$

$$
x_1+3x_2\geq12
$$

$$
x_1,x_2\geq0.
$$

---

## Problem 2

Convert:

$$
\min Z=3x_1+2x_2
$$

subject to

$$
x_1+x_2\geq5
$$

$$
2x_1+x_2=8
$$

$$
x_1,x_2\geq0.
$$

---

## Problem 3

Convert:

$$
\max Z=4x_1+3x_2
$$

subject to

$$
x_1-2x_2\leq-4
$$

$$
2x_1+x_2\geq6
$$

$$
x_1,x_2\geq0.
$$

Pay particular attention to the negative RHS.

---

## Problem 4

Suppose $x_2$ is unrestricted in sign.

Convert

$$
\max Z=3x_1+5x_2
$$

into an equivalent problem containing only non-negative variables.

---

# Next Topic

After standard form, the natural progression is:

$$
\boxed{
\text{Simplex Method}
\rightarrow
\text{Artificial Variables}
\rightarrow
\text{Big-M}
\rightarrow
\text{Two-Phase}
\rightarrow
\text{Matrix Form}
\rightarrow
\text{Revised Simplex}
}
$$