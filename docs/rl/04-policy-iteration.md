
# Policy Iteration

## 1. Definition

**Policy Iteration** is a Dynamic Programming method for finding an optimal policy.

It repeatedly performs:

1. Policy Evaluation
2. Policy Improvement

until the policy becomes stable.

```text
Initial Policy
      ↓
Policy Evaluation
      ↓
Vπ
      ↓
Policy Improvement
      ↓
New Policy
      ↓
Policy Evaluation
      ↓
...
      ↓
Optimal Policy
```

---

# 2. Requirement

Classical policy iteration requires a known model of the environment:

- state space
- action space
- transition probabilities
- reward function

Therefore, policy iteration is a **model-based Dynamic Programming method**.

It is not directly a model-free RL algorithm like Q-learning.

---

# 3. Step 1 — Initialize Policy

Start with an arbitrary policy:

\[
\pi_0
\]

Example:

```text
State A → Right
State B → Left
State C → Up
```

The initial policy does not need to be optimal.

---

# 4. Step 2 — Policy Evaluation

For the current policy \(\pi\), calculate:

\[
V^\pi(s)
\]

using the Bellman expectation equation:

\[
\boxed{
V^\pi(s)
=
\sum_a\pi(a|s)
\sum_{s'}P(s'|s,a)
[R+\gamma V^\pi(s')]
}
\]

For a deterministic policy:

\[
\boxed{
V^\pi(s)
=
\sum_{s'}P(s'|s,\pi(s))
[R+\gamma V^\pi(s')]
}
\]

The evaluation is repeated until the values converge sufficiently.

---

# 5. Step 3 — Policy Improvement

Once \(V^\pi\) is available, check whether another action produces a better expected value.

For each state:

\[
\boxed{
\pi'(s)
=
\arg\max_a
\sum_{s'}P(s'|s,a)
[R+\gamma V^\pi(s')]
}
\]

The agent becomes greedy with respect to the current value function.

---

# 6. Policy Improvement Theorem

The policy improvement step produces a policy that is:

- strictly better than the old policy, or
- equally good, in which case the old policy is already optimal.

Therefore:

\[
V^{\pi'}(s)\geq V^\pi(s)
\]

for all states.

If:

\[
\pi'=\pi
\]

the policy is stable and therefore optimal under the standard finite MDP assumptions.

---

# 7. Complete Algorithm

```text
Initialize arbitrary policy π

repeat:

    Evaluate π
        ↓
    Calculate Vπ

    Improve π
        ↓
    For every state:
        choose action with maximum expected value

until policy is unchanged
```

---

# 8. Policy Evaluation in Detail

Suppose a state \(s\) has two actions:

```text
Action A → next state s1
Action B → next state s2
```

Suppose:

\[
V(s_1)=4
\]

\[
V(s_2)=6
\]

and:

\[
R=-1,\qquad\gamma=0.9
\]

If the current policy selects A:

\[
V^\pi(s)
=
-1+0.9(4)
\]

\[
=2.6
\]

If it selects B:

\[
V^\pi(s)
=
-1+0.9(6)
\]

\[
=4.4
\]

Therefore B is better.

---

# 9. Policy Improvement

Compare the expected values:

\[
Q(s,A)=2.6
\]

\[
Q(s,B)=4.4
\]

Therefore:

\[
\pi'(s)=B
\]

The policy has improved.

---

# 10. Policy Iteration vs Value Iteration

These are frequently confused.

## Policy Iteration

Performs:

\[
\boxed{
\pi\rightarrow V^\pi\rightarrow\pi'
}
\]

It explicitly maintains a policy.

### Steps

```text
Policy
  ↓
Evaluate
  ↓
Improve
  ↓
Policy
```

---

## Value Iteration

Value iteration directly applies the Bellman optimality equation:

\[
\boxed{
V_{k+1}(s)
=
\max_a
\sum_{s'}P(s'|s,a)
[R+\gamma V_k(s')]
}
\]

It does not completely evaluate a policy before improving it.

```text
V0
 ↓
Bellman optimality update
 ↓
V1
 ↓
Bellman optimality update
 ↓
V2
 ↓
...
 ↓
V*
```

The supplied lecture explicitly distinguishes policy iteration from value iteration in this way.

---

# 11. Comparison Table

| Feature | Policy Iteration | Value Iteration |
|---|---|---|
| Starts with | Policy | Value function |
| Main operation | Evaluation + improvement | Bellman optimality update |
| Explicit policy | Yes | Extracted at end |
| Uses Bellman expectation | Yes | No |
| Uses Bellman optimality | During improvement | Directly |
| Model required | Yes | Yes |
| Goal | Optimal policy | Optimal value, then policy |

---

# 12. Why Policy Iteration Works

Policy iteration alternates between two tasks:

### Evaluation

"How good is my current policy?"

\[
\pi\rightarrow V^\pi
\]

### Improvement

"Can I make the policy better using those values?"

\[
V^\pi\rightarrow\pi'
\]

Repeating this eventually reaches a stable policy.

---

# 13. Exam Numerical Strategy

When a question asks for policy iteration:

### Step 1 — Write the current policy

Example:

\[
\pi(A)=X,\quad
\pi(B)=X,\quad
\pi(C)=X
\]

### Step 2 — Evaluate the policy

Use:

\[
V^\pi(s)=R+\gamma V^\pi(s')
\]

or the stochastic Bellman equation.

### Step 3 — Calculate action values

For every possible action:

\[
Q^\pi(s,a)
=
R+\gamma\sum_{s'}P(s'|s,a)V^\pi(s')
\]

### Step 4 — Improve

Choose:

\[
\pi'(s)=\arg\max_aQ^\pi(s,a)
\]

### Step 5 — Check stability

If:

\[
\pi'=\pi
\]

stop.

Otherwise repeat.

---

# 14. Policy Iteration vs Q-Learning

This is an important conceptual distinction.

| Policy Iteration | Q-Learning |
|---|---|
| Dynamic Programming | Model-free RL |
| Requires environment model | Does not require model |
| Uses transition probabilities | Learns from experience |
| Explicit policy evaluation | Direct Q-value updates |
| Uses Bellman expectation + improvement | Uses Bellman optimality target |
| Suitable when model is known | Suitable when model is unknown |

---

# 15. Exam Definition

> **Policy Iteration is a Dynamic Programming algorithm that repeatedly evaluates the current policy and improves it greedily with respect to its value function until the policy becomes stable.**

---

# 16. Key Formula Sheet

### Policy evaluation

\[
\boxed{
V^\pi(s)
=
\sum_a\pi(a|s)
\sum_{s'}P(s'|s,a)
[R+\gamma V^\pi(s')]
}
\]

### Policy improvement

\[
\boxed{
\pi'(s)=
\arg\max_a
\sum_{s'}P(s'|s,a)
[R+\gamma V^\pi(s')]
}
\]

### Value iteration

\[
\boxed{
V_{k+1}(s)
=
\max_a
\sum_{s'}P(s'|s,a)
[R+\gamma V_k(s')]
}
\]

---

# 17. What to Remember for the Exam

The entire topic can be reduced to:

```text
POLICY ITERATION

       π
       ↓
  Evaluate π
       ↓
      Vπ
       ↓
 Improve π
       ↓
      π'
       ↓
   π' = π ?
    /     \
  Yes      No
   ↓        ↓
 Stop     Repeat
```

The most important distinction:

> **Policy Iteration = evaluate a policy, then improve it.**

> **Value Iteration = directly apply Bellman optimality updates.**