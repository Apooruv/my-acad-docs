# Revised Simplex Method

The Revised Simplex Method is a matrix-based implementation of the
Simplex Method.

The main idea is to avoid maintaining the complete simplex tableau.

Instead, calculations are performed using:

$$
B^{-1}
$$

the inverse of the current basis matrix.

The course syllabus explicitly includes Revised Simplex Method in
Unit I, and the laboratory includes a separate Revised Simplex
implementation. 

---

# 1. Why Revised Simplex?

The ordinary Simplex tableau contains many entries.

For a large LPP, maintaining and updating the complete tableau can
be computationally expensive.

The Revised Simplex Method calculates only the quantities needed
to determine:

- current basic solution;
- objective value;
- reduced costs;
- entering variable;
- search direction;
- leaving variable.

---

# 2. Standard Form

Start with:

$$
\boxed{
\max Z=c^Tx
}
$$

subject to:

$$
\boxed{
Ax=b
}
$$

$$
x\geq0.
$$

Partition the variables into basic and non-basic variables.

---

# 3. Basis Matrix

Select $m$ linearly independent columns of $A$.

These columns form:

$$
\boxed{
B
}
$$

with inverse:

$$
\boxed{
B^{-1}.
}
$$

---

# 4. Step 1 — Calculate the Basic Solution

The current basic variables satisfy:

$$
Bx_B=b.
$$

Therefore:

$$
\boxed{
x_B=B^{-1}b.
}
$$

If:

$$
x_B\geq0,
$$

the current basis is feasible.

---

# 5. Step 2 — Calculate the Current Objective

Let:

$$
C_B
$$

be the objective coefficients of the basic variables.

Then:

$$
\boxed{
Z=C_Bx_B.
}
$$

---

# 6. Step 3 — Calculate Simplex Multipliers

Calculate:

$$
\boxed{
y^T=C_BB^{-1}.
}
$$

---

# 7. Step 4 — Calculate Reduced Costs

For every non-basic variable $x_j$:

$$
\boxed{
C_j-Z_j=C_j-y^Ta_j.
}
$$

For a maximization problem:

$$
\boxed{
C_j-Z_j\leq0
}
$$

for all $j$ means the current solution is optimal.

---

# 8. Step 5 — Select Entering Variable

For maximization:

$$
C_j-Z_j>0
$$

indicates that increasing $x_j$ can improve the objective.

Therefore choose the variable with the largest positive value:

$$
\boxed{
\text{Entering variable}
=
\arg\max_j(C_j-Z_j).
}
$$

---

# 9. Step 6 — Calculate the Direction Vector

Suppose variable $x_k$ enters.

Take its column:

$$
a_k.
$$

Calculate:

$$
\boxed{
d=B^{-1}a_k.
}
$$

This is the direction in which the current basic solution changes
when $x_k$ enters.

---

# 10. Step 7 — Ratio Test

The current basic solution is:

$$
x_B.
$$

After increasing $x_k$ by $\theta$:

$$
x_B(\theta)=x_B-\theta d.
$$

To maintain feasibility:

$$
x_B-\theta d\geq0.
$$

For every $d_i>0$:

$$
\theta\leq\frac{x_{B_i}}{d_i}.
$$

Therefore:

$$
\boxed{
\theta^*
=
\min_{d_i>0}
\frac{x_{B_i}}{d_i}.
}
$$

The row producing the minimum ratio determines the leaving variable.

---

# 11. Important Special Case — Unboundedness

If:

$$
C_k-Z_k>0
$$

but

$$
d_i\leq0
$$

for every $i$,

then no positive ratio exists.

The entering variable can increase indefinitely without violating
the constraints.

Therefore:

$$
\boxed{
\text{The LPP is unbounded.}
}
$$

---

# 12. Step 8 — Update the Basis

If basic variable $x_{B_r}$ leaves and $x_k$ enters:

$$
B_{\text{new}}
=
(B\text{ with column }r\text{ replaced by }a_k).
$$

Then calculate:

$$
B_{\text{new}}^{-1}.
$$

The process repeats.

---

# 13. Complete Revised Simplex Algorithm

### Step 1

Convert the LPP to standard form.

### Step 2

Select an initial basis $B$.

### Step 3

Calculate:

$$
B^{-1}.
$$

### Step 4

Calculate:

$$
x_B=B^{-1}b.
$$

### Step 5

Check feasibility:

$$
x_B\geq0.
$$

### Step 6

Calculate:

$$
y^T=C_BB^{-1}.
$$

### Step 7

Calculate reduced costs:

$$
C_j-Z_j=C_j-y^Ta_j.
$$

### Step 8

Check optimality.

For maximization:

$$
C_j-Z_j\leq0.
$$

### Step 9

Select the entering variable with the largest positive
$C_j-Z_j$.

### Step 10

Calculate:

$$
d=B^{-1}a_k.
$$

### Step 11

Perform the ratio test:

$$
\frac{x_{B_i}}{d_i},
\qquad d_i>0.
$$

### Step 12

Identify the leaving variable.

### Step 13

Replace the corresponding basis column.

### Step 14

Calculate the new $B^{-1}$.

### Step 15

Repeat until optimality.

---

# 14. Full Worked Problem

Solve using the Revised Simplex Method:

$$
\max Z=40x_1+30x_2
$$

subject to

$$
2x_1+x_2\leq90
$$

$$
x_1+3x_2\leq120
$$

$$
3x_1+2x_2\leq150
$$

$$
x_1,x_2\geq0.
$$

This is also representative of the Simplex implementation problems
provided in the course laboratory material. 

---

## Step 1 — Standard Form

Introduce slack variables:

$$
2x_1+x_2+s_1=90
$$

$$
x_1+3x_2+s_2=120
$$

$$
3x_1+2x_2+s_3=150.
$$

Therefore:

$$
A=
\begin{bmatrix}
2&1&1&0&0\\
1&3&0&1&0\\
3&2&0&0&1
\end{bmatrix}
$$

and

$$
b=
\begin{bmatrix}
90\\
120\\
150
\end{bmatrix}.
$$

The objective coefficients are:

$$
c=
\begin{bmatrix}
40\\
30\\
0\\
0\\
0
\end{bmatrix}.
$$

---

# Iteration 0

## Step 2 — Initial Basis

Choose:

$$
B=[a_3,a_4,a_5]
$$

corresponding to:

$$
s_1,s_2,s_3.
$$

Thus:

$$
B=
\begin{bmatrix}
1&0&0\\
0&1&0\\
0&0&1
\end{bmatrix}
=I.
$$

Therefore:

$$
B^{-1}=I.
$$

---

## Step 3 — Basic Solution

$$
x_B=B^{-1}b
$$

$$
=
\begin{bmatrix}
90\\
120\\
150
\end{bmatrix}.
$$

Thus:

$$
s_1=90,\quad s_2=120,\quad s_3=150.
$$

and:

$$
x_1=x_2=0.
$$

The solution is feasible.

---

## Step 4 — Objective Value

Since:

$$
C_B=
\begin{bmatrix}
0&0&0
\end{bmatrix},
$$

we have:

$$
Z=0.
$$

---

## Step 5 — Simplex Multipliers

$$
y^T=C_BB^{-1}.
$$

Therefore:

$$
y^T=
\begin{bmatrix}
0&0&0
\end{bmatrix}.
$$

---

## Step 6 — Reduced Costs

For $x_1$:

$$
C_1-Z_1
=
40-y^Ta_1
$$

$$
=40.
$$

For $x_2$:

$$
C_2-Z_2=30.
$$

For slack variables:

$$
C_j-Z_j=0.
$$

Therefore:

| Variable | $C_j-Z_j$ |
|---|---:|
| $x_1$ | 40 |
| $x_2$ | 30 |
| $s_1$ | 0 |
| $s_2$ | 0 |
| $s_3$ | 0 |

Largest positive value:

$$
40.
$$

Therefore:

$$
\boxed{x_1\text{ enters}}.
$$

---

# Iteration 0 → 1

## Step 7 — Direction Vector

The column corresponding to $x_1$ is:

$$
a_1=
\begin{bmatrix}
2\\
1\\
3
\end{bmatrix}.
$$

Calculate:

$$
d=B^{-1}a_1.
$$

Since:

$$
B^{-1}=I,
$$

we get:

$$
d=
\begin{bmatrix}
2\\
1\\
3
\end{bmatrix}.
$$

---

## Step 8 — Ratio Test

Current basic solution:

$$
x_B=
\begin{bmatrix}
90\\
120\\
150
\end{bmatrix}.
$$

Calculate:

$$
\frac{90}{2}=45
$$

$$
\frac{120}{1}=120
$$

$$
\frac{150}{3}=50.
$$

Minimum:

$$
45.
$$

Therefore:

$$
\boxed{s_1\text{ leaves}}.
$$

So the new basis is:

$$
\boxed{
B=[a_1,a_4,a_5].
}
$$

---

# Iteration 1

## Step 9 — New Basis

The new basis matrix is:

$$
B=
\begin{bmatrix}
2&0&0\\
1&1&0\\
3&0&1
\end{bmatrix}.
$$

Calculate its inverse:

$$
\boxed{
B^{-1}
=
\begin{bmatrix}
\frac12&0&0\\
-\frac12&1&0\\
-\frac32&0&1
\end{bmatrix}.
}
$$

---

## Step 10 — Basic Solution

Calculate:

$$
x_B=B^{-1}b.
$$

Therefore:

$$
\begin{bmatrix}
x_1\\
s_2\\
s_3
\end{bmatrix}
=
\begin{bmatrix}
\frac12&0&0\\
-\frac12&1&0\\
-\frac32&0&1
\end{bmatrix}
\begin{bmatrix}
90\\
120\\
150
\end{bmatrix}.
$$

First component:

$$
x_1=45.
$$

Second:

$$
s_2=-45+120=75.
$$

Third:

$$
s_3=-135+150=15.
$$

Therefore:

$$
\boxed{
x_1=45,\quad s_2=75,\quad s_3=15.
}
$$

---

## Step 11 — Objective

The basic objective coefficients are:

$$
C_B=
\begin{bmatrix}
40&0&0
\end{bmatrix}.
$$

Therefore:

$$
Z=40(45)=1800.
$$

---

## Step 12 — Simplex Multipliers

$$
y^T=C_BB^{-1}.
$$

Therefore:

$$
y^T=
\begin{bmatrix}
40&0&0
\end{bmatrix}
\begin{bmatrix}
\frac12&0&0\\
-\frac12&1&0\\
-\frac32&0&1
\end{bmatrix}.
$$

Thus:

$$
\boxed{
y^T=
\begin{bmatrix}
20&0&0
\end{bmatrix}.
}
$$

---

## Step 13 — Reduced Costs

For $x_2$:

$$
a_2=
\begin{bmatrix}
1\\
3\\
2
\end{bmatrix}.
$$

Therefore:

$$
Z_2=y^Ta_2
$$

$$
=
20(1)+0(3)+0(2)
$$

$$
=20.
$$

Hence:

$$
C_2-Z_2=30-20=10.
$$

For $s_1$:

$$
Z_{s_1}=20
$$

so:

$$
C_{s_1}-Z_{s_1}
=
0-20=-20.
$$

For $s_2,s_3$:

$$
C_j-Z_j=0.
$$

Thus:

| Variable | $C_j-Z_j$ |
|---|---:|
| $x_1$ | 0 |
| $x_2$ | 10 |
| $s_1$ | -20 |
| $s_2$ | 0 |
| $s_3$ | 0 |

Since $x_2$ has a positive reduced cost:

$$
\boxed{x_2\text{ enters}}.
$$

---

# Iteration 1 → 2

## Step 14 — Direction Vector

Calculate:

$$
d=B^{-1}a_2.
$$

$$
d=
\begin{bmatrix}
\frac12&0&0\\
-\frac12&1&0\\
-\frac32&0&1
\end{bmatrix}
\begin{bmatrix}
1\\
3\\
2
\end{bmatrix}.
$$

First component:

$$
\frac12.
$$

Second:

$$
-\frac12+3=\frac52.
$$

Third:

$$
-\frac32+2=\frac12.
$$

Therefore:

$$
\boxed{
d=
\begin{bmatrix}
\frac12\\
\frac52\\
\frac12
\end{bmatrix}.
}
$$

---

## Step 15 — Ratio Test

Current basic solution:

$$
x_B=
\begin{bmatrix}
45\\
75\\
15
\end{bmatrix}.
$$

Ratios:

$$
\frac{45}{1/2}=90
$$

$$
\frac{75}{5/2}=30
$$

$$
\frac{15}{1/2}=30.
$$

The minimum ratio is:

$$
30.
$$

There is a tie between rows 2 and 3.

A valid choice is to let:

$$
\boxed{s_2\text{ leave}}.
$$

Then:

$$
\boxed{x_2\text{ enters}}.
$$

New basis:

$$
\boxed{
B=[a_1,a_2,a_5].
}
$$

---

# Iteration 2

## Step 16 — New Basis Matrix

$$
B=
\begin{bmatrix}
2&1&0\\
1&3&0\\
3&2&1
\end{bmatrix}.
$$

Its inverse is:

$$
\boxed{
B^{-1}
=
\begin{bmatrix}
\frac35&-\frac15&0\\
-\frac15&\frac25&0\\
-\frac75&-\frac15&1
\end{bmatrix}.
}
$$

---

## Step 17 — Basic Solution

Calculate:

$$
x_B=B^{-1}b.
$$

Therefore:

$$
\begin{bmatrix}
x_1\\
x_2\\
s_3
\end{bmatrix}
=
\begin{bmatrix}
\frac35&-\frac15&0\\
-\frac15&\frac25&0\\
-\frac75&-\frac15&1
\end{bmatrix}
\begin{bmatrix}
90\\
120\\
150
\end{bmatrix}.
$$

First:

$$
x_1=54-24=30.
$$

Second:

$$
x_2=-18+48=30.
$$

Third:

$$
s_3=-126-24+150=0.
$$

Therefore:

$$
\boxed{
x_1=30,\quad x_2=30,\quad s_3=0.
}
$$

---

## Step 18 — Objective

$$
Z=40(30)+30(30)
$$

$$
=1200+900
$$

$$
\boxed{Z=2100}.
$$

---

## Step 19 — Optimality Test

Here:

$$
C_B=
\begin{bmatrix}
40&30&0
\end{bmatrix}.
$$

Calculate:

$$
y^T=C_BB^{-1}.
$$

Thus:

$$
y^T=
\begin{bmatrix}
18&4&0
\end{bmatrix}.
$$

Now calculate reduced costs.

For $s_1$:

$$
a_3=
\begin{bmatrix}
1\\
0\\
0
\end{bmatrix}
$$

so:

$$
Z_{s_1}=18.
$$

Therefore:

$$
C_{s_1}-Z_{s_1}
=
0-18
=-18.
$$

For $s_2$:

$$
a_4=
\begin{bmatrix}
0\\
1\\
0
\end{bmatrix}
$$

so:

$$
Z_{s_2}=4.
$$

Therefore:

$$
C_{s_2}-Z_{s_2}
=
-4.
$$

For $x_1$ and $x_2$, because they are basic:

$$
C_j-Z_j=0.
$$

Therefore:

| Variable | $C_j-Z_j$ |
|---|---:|
| $x_1$ | 0 |
| $x_2$ | 0 |
| $s_1$ | -18 |
| $s_2$ | -4 |
| $s_3$ | 0 |

All:

$$
C_j-Z_j\leq0.
$$

Therefore:

$$
\boxed{\text{Optimal solution reached.}}
$$

---

# 15. Final Answer

$$
\boxed{x_1=30}
$$

$$
\boxed{x_2=30}
$$

and

$$
\boxed{Z_{\max}=2100}.
$$

The third constraint is:

$$
3(30)+2(30)=150,
$$

so:

$$
s_3=0.
$$

The first two constraints also become:

$$
2(30)+30=90
$$

and

$$
30+3(30)=120.
$$

Therefore all three constraints are binding at the optimum.

---

# 16. Revised Simplex vs Ordinary Simplex

| Feature | Ordinary Simplex | Revised Simplex |
|---|---|---|
| Main representation | Full tableau | Basis matrix |
| Uses $B^{-1}$ | Implicitly | Explicitly |
| Calculates full tableau | Yes | No |
| Basic solution | Tableau RHS | $B^{-1}b$ |
| Reduced cost | Tableau row | $C_j-C_BB^{-1}a_j$ |
| Direction | Tableau column | $B^{-1}a_j$ |
| Large problems | More computation | More efficient |
| Main mathematical tool | Row operations | Matrix operations |

---

# 17. Ordinary Simplex and Revised Simplex Are the Same Method

The Revised Simplex Method does not use a fundamentally different
optimization principle.

Both methods:

1. start from a BFS;
2. determine whether improvement is possible;
3. choose an entering variable;
4. choose a leaving variable;
5. change the basis;
6. repeat until optimality.

The difference is primarily **how the calculations are organized**.

---

# 18. Important Formulas

Memorize these for the exam.

### Basic solution

$$
\boxed{x_B=B^{-1}b}
$$

### Objective value

$$
\boxed{Z=C_Bx_B}
$$

### Simplex multipliers

$$
\boxed{y^T=C_BB^{-1}}
$$

### $Z_j$

$$
\boxed{Z_j=y^Ta_j}
$$

### Reduced cost

$$
\boxed{C_j-Z_j=C_j-y^Ta_j}
$$

### Direction vector

$$
\boxed{d=B^{-1}a_j}
$$

### Ratio test

$$
\boxed{
\theta=
\min_{d_i>0}
\frac{x_{B_i}}{d_i}
}
$$

### Maximization optimality

$$
\boxed{
C_j-Z_j\leq0
}
$$

---

# 19. Important Conceptual Questions

## Q1. What is a basis?

A basis is a collection of $m$ linearly independent columns of the
constraint matrix $A$.

---

## Q2. What is the basis matrix?

The matrix formed by the columns corresponding to the current
basic variables:

$$
B=[a_{B_1},a_{B_2},\ldots,a_{B_m}].
$$

---

## Q3. Why must $B$ be nonsingular?

Because we need:

$$
B^{-1}
$$

to obtain:

$$
x_B=B^{-1}b.
$$

---

## Q4. What does $B^{-1}b$ represent?

It gives the values of the current basic variables.

---

## Q5. What does $B^{-1}a_j$ represent?

It gives the direction in which the current basic variables change
when non-basic variable $x_j$ enters.

---

## Q6. Why is the ratio test performed only for positive components
of $d$?

Because:

$$
x_B-\theta d\geq0.
$$

Only $d_i>0$ imposes an upper bound on $\theta$.

---

## Q7. When is a Revised Simplex solution optimal?

For maximization using the $C_j-Z_j$ convention:

$$
C_j-Z_j\leq0
$$

for every variable.

---

# 20. Exam Problem — Matrix Calculation

Given:

$$
B=
\begin{bmatrix}
1&2\\
3&4
\end{bmatrix},
\quad
b=
\begin{bmatrix}
5\\
11
\end{bmatrix},
\quad
C_B=
\begin{bmatrix}
6&5
\end{bmatrix},
$$

calculate:

1. $B^{-1}$
2. $x_B$
3. $Z$
4. $y^T$

### Solution

Determinant:

$$
|B|=(1)(4)-(2)(3)=-2.
$$

Therefore:

$$
B^{-1}
=
-\frac12
\begin{bmatrix}
4&-2\\
-3&1
\end{bmatrix}.
$$

Hence:

$$
\boxed{
B^{-1}
=
\begin{bmatrix}
-2&1\\
\frac32&-\frac12
\end{bmatrix}
}
$$

Now:

$$
x_B=B^{-1}b.
$$

$$
=
\begin{bmatrix}
-2&1\\
\frac32&-\frac12
\end{bmatrix}
\begin{bmatrix}
5\\
11
\end{bmatrix}
$$

Therefore:

$$
x_{B_1}=-10+11=1
$$

and

$$
x_{B_2}=7.5-5.5=2.
$$

Thus:

$$
\boxed{x_B=(1,2)^T}.
$$

Objective:

$$
Z=6(1)+5(2)
$$

$$
\boxed{Z=16}.
$$

Finally:

$$
y^T=C_BB^{-1}
$$

$$
=
\begin{bmatrix}
6&5
\end{bmatrix}
\begin{bmatrix}
-2&1\\
\frac32&-\frac12
\end{bmatrix}.
$$

Therefore:

$$
y_1=-12+7.5=-4.5
$$

$$
y_2=6-2.5=3.5.
$$

Hence:

$$
\boxed{
y^T=
\begin{bmatrix}
-4.5&3.5
\end{bmatrix}.
}
$$

---

# 21. Common Mistakes

### Mistake 1 — Mixing $C_j-Z_j$ and $Z_j-C_j$

If using:

$$
C_j-Z_j,
$$

then for maximization:

$$
C_j-Z_j>0
$$

means improvement is possible.

Optimality:

$$
C_j-Z_j\leq0.
$$

If using:

$$
Z_j-C_j,
$$

all signs reverse.

---

### Mistake 2 — Using $a_j$ instead of $B^{-1}a_j$

The ratio test in Revised Simplex uses:

$$
\boxed{B^{-1}a_j}
$$

not simply the original column $a_j$.

---

### Mistake 3 — Forgetting to calculate the new basis

After selecting the leaving variable, replace that basis column
with the entering variable's column.

---

### Mistake 4 — Checking the wrong vector for feasibility

Feasibility is determined using:

$$
\boxed{x_B=B^{-1}b}.
$$

The current basic variables must satisfy:

$$
x_B\geq0.
$$

---

### Mistake 5 — Ignoring ties

If two ratios are equal, either valid leaving variable may sometimes
be selected, although the choice can affect the number of iterations
and may lead to degeneracy.

---

# 22. Revised Simplex Exam Template

For a numerical question, write:

### Given

$$
A,\quad b,\quad c
$$

### Initial Basis

$$
B=...
$$

### Inverse

$$
B^{-1}=...
$$

### Basic Solution

$$
x_B=B^{-1}b.
$$

### Objective

$$
Z=C_Bx_B.
$$

### Multipliers

$$
y^T=C_BB^{-1}.
$$

### Reduced Costs

$$
C_j-Z_j=C_j-y^Ta_j.
$$

### Entering Variable

Largest positive $C_j-Z_j$.

### Direction

$$
d=B^{-1}a_j.
$$

### Ratio Test

$$
\frac{x_{B_i}}{d_i},
\qquad d_i>0.
$$

### Leaving Variable

Smallest positive ratio.

### New Basis

Replace leaving column with entering column.

### Repeat

Until:

$$
C_j-Z_j\leq0.
$$

### Final Answer

State:

$$
x_1,\ldots,x_n
$$

and

$$
Z_{\max}.
$$

---

# 23. Practice Problems

## Problem 1 — Basic Matrix Operations

Given:

$$
B=
\begin{bmatrix}
2&1\\
1&3
\end{bmatrix},
\quad
b=
\begin{bmatrix}
8\\
9
\end{bmatrix},
\quad
C_B=
\begin{bmatrix}
5&4
\end{bmatrix}.
$$

Find:

1. $B^{-1}$
2. $x_B$
3. $Z$
4. $y^T$

---

## Problem 2 — Reduced Cost

Given:

$$
B^{-1}
=
\begin{bmatrix}
1&0\\
-1&1
\end{bmatrix}
$$

and

$$
C_B=
\begin{bmatrix}
4&3
\end{bmatrix}.
$$

For

$$
a_j=
\begin{bmatrix}
2\\
1
\end{bmatrix},
\qquad
C_j=7,
$$

calculate:

$$
y^T
$$

and

$$
C_j-Z_j.
$$

---

## Problem 3 — Direction and Ratio

Suppose:

$$
x_B=
\begin{bmatrix}
20\\
15\\
10
\end{bmatrix}
$$

and

$$
B^{-1}a_j=
\begin{bmatrix}
2\\
-1\\
4
\end{bmatrix}.
$$

Calculate the maximum allowable increase in $x_j$.

---

## Problem 4 — Full Revised Simplex

Solve using Revised Simplex:

$$
\max Z=40x_1+30x_2
$$

subject to

$$
2x_1+x_2\leq90
$$

$$
x_1+3x_2\leq120
$$

$$
3x_1+2x_2\leq150
$$

$$
x_1,x_2\geq0.
$$

Show:

- initial basis;
- $B^{-1}$;
- $x_B$;
- $C_B$;
- $y^T$;
- every reduced cost;
- entering variable;
- $B^{-1}a_j$;
- ratio test;
- leaving variable;
- new basis;
- new $B^{-1}$;
- final optimality check;
- final solution.

---

## Problem 5 — Unboundedness

Suppose a non-basic variable has:

$$
C_j-Z_j=5
$$

but

$$
B^{-1}a_j=
\begin{bmatrix}
-2\\
0\\
-4
\end{bmatrix}.
$$

Determine what happens.

### Answer

There are no positive components in:

$$
B^{-1}a_j.
$$

Therefore the ratio test cannot be performed.

Hence the problem is:

$$
\boxed{\text{Unbounded}}
$$

in that direction.

---

# Final Unit-I Connection

The entire first half of Unit I can now be viewed as:

$$
\boxed{
\text{LPP}
\rightarrow
\text{Standard Form}
\rightarrow
\text{Initial BFS}
\rightarrow
\text{Simplex}
}
$$

When a direct BFS is unavailable:

$$
\boxed{
\text{Artificial Variables}
\rightarrow
\begin{cases}
\text{Big-M}\\
\text{Two-Phase}
\end{cases}
}
$$

Then the matrix representation gives:

$$
\boxed{
Ax=b
\rightarrow
B
\rightarrow
B^{-1}
\rightarrow
\text{Revised Simplex}
}
$$

The key mathematical chain to remember is:

$$
\boxed{
B^{-1}
\rightarrow
x_B=B^{-1}b
\rightarrow
y^T=C_BB^{-1}
\rightarrow
C_j-Z_j
\rightarrow
B^{-1}a_j
\rightarrow
\text{Ratio Test}
\rightarrow
\text{New Basis}
}
$$