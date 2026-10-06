# Artificial Variables

Artificial variables are temporary variables introduced when an
initial Basic Feasible Solution cannot be obtained directly.

They are particularly important for:

- $\geq$ constraints;
- equality constraints.

They are used in:

- Big-M Method;
- Two-Phase Method.

---

# 1. Why Are Artificial Variables Needed?

Consider:

$$
x_1+x_2\geq5.
$$

After subtracting a surplus variable:

$$
x_1+x_2-s_1=5.
$$

The coefficient of $s_1$ is $-1$.

Therefore, $s_1$ does not provide the required identity column
for a straightforward initial basis.

Introduce an artificial variable:

$$
\boxed{
x_1+x_2-s_1+a_1=5
}
$$

Now $a_1$ provides a basic column.

---

# 2. Equality Constraints

Consider:

$$
x_1+x_2=5.
$$

There is no slack variable.

Introduce:

$$
\boxed{
x_1+x_2+a_1=5
}
$$

Again, $a_1$ supplies the initial basic variable.

---

# 3. Important Rule

### $\leq$ constraint

$$
Ax\leq b
$$

usually requires:

$$
Ax+s=b.
$$

No artificial variable is needed if this creates an initial identity basis.

---

### $\geq$ constraint

$$
Ax\geq b
$$

becomes:

$$
Ax-s=b.
$$

An artificial variable is generally required:

$$
Ax-s+a=b.
$$

---

### Equality constraint

$$
Ax=b
$$

may require:

$$
Ax+a=b.
$$

---

# 4. Artificial Variables Are Not Real Variables

An artificial variable does not represent a physical quantity.

It exists only to construct an initial basis.

Therefore, at the final solution:

$$
\boxed{a_i=0}
$$

must hold.

If an artificial variable remains positive at the end,
the original LPP is infeasible.

---

# 5. Two Ways to Remove Artificial Variables

The two standard approaches are:

### Big-M Method

Assign a very large penalty $M$ to artificial variables.

### Two-Phase Method

Phase I removes artificial variables by minimizing their sum.

These are covered separately.

---

# Worked Example

Convert:

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

## Step 1 — First constraint

$$
x_1+x_2\leq4
$$

Add slack:

$$
x_1+x_2+s_1=4.
$$

---

## Step 2 — Second constraint

$$
x_1+2x_2\geq6.
$$

Subtract surplus:

$$
x_1+2x_2-s_2=6.
$$

Add artificial variable:

$$
x_1+2x_2-s_2+a_2=6.
$$

---

## Final form

$$
x_1+x_2+s_1=4
$$

$$
x_1+2x_2-s_2+a_2=6.
$$

Initial basis:

$$
s_1,a_2.
$$

The artificial variable $a_2$ must eventually be removed.

---

# Exam Rule

Whenever you see:

$$
\boxed{\geq}
$$

think:

$$
-\text{surplus}+\text{artificial}.
$$

Whenever you see:

$$
\boxed{=}
$$

think:

$$
+\text{artificial}
$$

when an initial basis is required.

---

# Practice

Convert the following to equality form and identify all artificial
variables.

### Problem 1

$$
2x_1+x_2\geq10
$$

### Problem 2

$$
x_1+3x_2=12
$$

### Problem 3

$$
x_1+x_2\leq8
$$

### Problem 4

$$
x_1+x_2\geq5
$$

$$
2x_1+x_2=8
$$

### Problem 5

Convert:

$$
\max Z=4x_1+3x_2
$$

subject to

$$
x_1+x_2\leq5
$$

$$
2x_1+x_2\geq8
$$

$$
x_1+2x_2=6
$$

$$
x_1,x_2\geq0.
$$

Identify:

1. slack variables;
2. surplus variables;
3. artificial variables;
4. initial basis.