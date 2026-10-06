Yes. Since this is the **main landing page for OT**, I would keep it clean rather than putting too much theory into it. It should act like a dashboard for your notes.

Replace your current `ot-index.md` with this:


# Optimization Techniques

> Midsem notes and problem-solving material for Optimization Techniques.

---

## Course Overview

Optimization Techniques deals with mathematical methods for finding the best solution to an optimization problem under given constraints.

### Current Midsem Coverage

- Unit I — Linear Programming
- Unit II — Duality and Unconstrained Optimization

> **Note:** Unit III is part of the official syllabus, but the current notes are focused on Unit I and Unit II for midsem preparation.

---

# Unit I — Linear Programming

## Theory

| Topic | Notes |
|---|---|
| Optimization Problems | [01 — Optimization Problems](unit-1/01-optimization-problems.md) |
| Linear Programming | [02 — Linear Programming](unit-1/02-linear-programming.md) |
| Standard Form | [03 — Standard Form](unit-1/03-standard-form.md) |
| Simplex Method | [04 — Simplex Method](unit-1/04-simplex-method.md) |
| Artificial Variables | [05 — Artificial Variables](unit-1/05-artificial-variables.md) |
| Big M Method | [06 — Big M Method](unit-1/06-big-m-method.md) |
| Two-Phase Method | [07 — Two-Phase Method](unit-1/07-two-phase-method.md) |
| Matrix Form | [08 — Matrix Form](unit-1/08-matrix-form.md) |
| Revised Simplex | [09 — Revised Simplex](unit-1/09-revised-simplex.md) |

## Problems

[Unit I — Problems & Solutions](unit-1/10-unit-i-problems-and-solutions.md)

### Important Methods

```text
Linear Programming
       │
       ├── Standard Form
       │
       ├── Simplex Method
       │
       ├── Artificial Variables
       │       ├── Big M
       │       └── Two-Phase
       │
       ├── Matrix Form
       │
       └── Revised Simplex
```

---

# Unit II — Duality & Unconstrained Optimization

## Theory

| Topic | Notes |
|---|---|
| Duality | [01 — Duality](unit-2/01-duality.md) |
| Duality Theorem | [02 — Duality Theorem](unit-2/02-duality-theorem.md) |
| Primal-Dual Construction | [03 — Primal-Dual Construction](unit-2/03-primal-dual-construction.md) |
| Complementary Slackness | [04 — Complementary Slackness](unit-2/04-complementary-slackness.md) |
| Sensitivity Analysis | [05 — Sensitivity Analysis](unit-2/05-sensitivity-analysis.md) |
| Dual Simplex | [06 — Dual Simplex](unit-2/06-dual-simplex.md) |
| Matrix Calculus | [07 — Matrix Calculus](unit-2/07-matrix-calculation.md) |
| Unconstrained Optimization | [08 — Conditions for Unconstrained Optimization](unit-2/08-conditions-unconstrained-optimization.md) |

## Problems

[Unit II — Problems & Solutions](unit-2/09-unit-ii-problems-and-solutions.md)

### Important Concepts


Duality
  │
  ├── Primal ↔ Dual
  │
  ├── Weak Duality
  │
  ├── Strong Duality
  │
  ├── Complementary Slackness
  │
  ├── Sensitivity Analysis
  │
  └── Dual Simplex

Unconstrained Optimization
  │
  ├── Gradient
  ├── Stationary Points
  ├── Hessian
  ├── Second-Order Conditions
  └── Convexity


---

# Quick Revision

## Unit I

### Must Know

- [ ] Types of optimization problems
- [ ] LPP formulation
- [ ] Standard form conversion
- [ ] Slack and surplus variables
- [ ] Artificial variables
- [ ] Simplex tableau
- [ ] Entering variable
- [ ] Leaving variable
- [ ] Pivot operation
- [ ] Optimality condition
- [ ] Big M Method
- [ ] Two-Phase Method
- [ ] Unbounded solution
- [ ] Infeasible solution
- [ ] Degeneracy
- [ ] Alternate optimal solutions
- [ ] Matrix form
- [ ] Revised Simplex Method

---

## Unit II

### Must Know

- [ ] Primal-Dual relationship
- [ ] Rules for constructing the dual
- [ ] Weak Duality Theorem
- [ ] Strong Duality Theorem
- [ ] Complementary Slackness
- [ ] Optimality using primal and dual solutions
- [ ] Sensitivity Analysis
- [ ] Shadow prices
- [ ] RHS sensitivity
- [ ] Dual Simplex Method
- [ ] Gradient
- [ ] Jacobian
- [ ] Hessian
- [ ] Matrix derivatives
- [ ] Positive/negative definite matrices
- [ ] First-order conditions
- [ ] Second-order conditions
- [ ] Convexity
- [ ] Classification of stationary points

---

# Problem Practice

## Unit I

1. Simplex Method
2. Big M Method
3. Two-Phase Method
4. Matrix Form
5. Revised Simplex
6. Special cases of LPP

→ [Unit I Problems](unit-1/10-unit-i-problems-and-solutions.md)

---

## Unit II

1. Construct the dual
2. Verify weak duality
3. Apply strong duality
4. Complementary slackness
5. Sensitivity analysis
6. Dual Simplex
7. Matrix derivatives
8. Hessian-based optimization
9. Classify stationary points

→ [Unit II Problems](unit-2/09-unit-ii-problems-and-solutions.md)

---

# Lab / Assignment Material

## Lab

[LPP Practical Lab](pdfs/LPP_Practical_Lab.pdf)

## Assignment

[LPP Assignment](problems/LPP_Assignment.md)

## Assignment Code Order

[LPP Assignment — Handwritten Code Order](problems/LPP_Assignment_Handwritten_Code_Order.md)

---

# Reference Material

[Optimization Techniques Syllabus](pdfs/Optimization_Techniques_Syllabus.pdf)

---

# Exam Strategy

## Before the Exam

### Step 1 — Revise Concepts

Go through:

- Simplex
- Big M
- Two-Phase
- Revised Simplex
- Duality
- Complementary Slackness
- Sensitivity
- Dual Simplex
- Matrix Calculus
- Unconstrained Optimization

### Step 2 — Solve Problems

Prioritize:

```text
Simplex
   ↓
Big M
   ↓
Two-Phase
   ↓
Revised Simplex
   ↓
Duality
   ↓
Complementary Slackness
   ↓
Sensitivity
   ↓
Dual Simplex
   ↓
Hessian / Unconstrained Optimization
```

### Step 3 — Final Revision

Make sure you can solve without notes:

- 2 Simplex problems
- 1 Big M problem
- 1 Two-Phase problem
- 1 Revised Simplex problem
- 2 Duality problems
- 1 Complementary Slackness problem
- 1 Sensitivity problem
- 1 Dual Simplex problem
- 3–4 Matrix Calculus/Hessian problems
- 3–4 Unconstrained Optimization problems

---

# Navigation

### Unit I

[Optimization Problems](unit-1/01-optimization-problems.md) ·
[Linear Programming](unit-1/02-linear-programming.md) ·
[Standard Form](unit-1/03-standard-form.md) ·
[Simplex](unit-1/04-simplex-method.md) ·
[Artificial Variables](unit-1/05-artificial-variables.md) ·
[Big M](unit-1/06-big-m-method.md) ·
[Two-Phase](unit-1/07-two-phase-method.md) ·
[Matrix Form](unit-1/08-matrix-form.md) ·
[Revised Simplex](unit-1/09-revised-simplex.md)

### Unit II

[Duality](unit-2/01-duality.md) ·
[Duality Theorem](unit-2/02-duality-theorem.md) ·
[Primal-Dual](unit-2/03-primal-dual-construction.md) ·
[Complementary Slackness](unit-2/04-complementary-slackness.md) ·
[Sensitivity](unit-2/05-sensitivity-analysis.md) ·
[Dual Simplex](unit-2/06-dual-simplex.md) ·
[Matrix Calculus](unit-2/07-matrix-calculation.md) ·
[Unconstrained Optimization](unit-2/08-conditions-unconstrained-optimization.md)

---

## Official Material

- [Syllabus](pdfs/Optimization_Techniques_Syllabus.pdf)
- [Practical Lab](pdfs/LPP_Practical_Lab.pdf)
```

### One thing to fix from your screenshot

Your current warning:


contains an absolute link '/pdfs/Optimization_Techniques_Syllabus.pdf'


means the link is probably written like:

[/pdfs/Optimization_Techniques_Syllabus.pdf](/pdfs/Optimization_Techniques_Syllabus.pdf)


For your current folder structure, use:

[Optimization Techniques Syllabus](pdfs/Optimization_Techniques_Syllabus.pdf)
