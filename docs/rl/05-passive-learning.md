# Passive Learning

## 1. What is Passive Learning?

In **passive reinforcement learning**, the agent follows a **fixed policy**.

The agent does not try to improve the policy.

Its task is to learn how good the states are under that policy.

```text
Fixed Policy π
      ↓
Interact with environment
      ↓
Observe episodes
      ↓
Estimate Vπ(s)
```

The main objective is:

\[
\boxed{V^\pi(s)}
\]

That is:

> Estimate the expected return obtained from state \(s\) when the agent follows policy \(\pi\).

---

## 2. Passive vs Active Learning

### Passive Learning

The policy is given.

The agent learns:

\[
\pi \rightarrow V^\pi
\]

Example:

```text
Policy:
If possible → move right
Otherwise → move down
```

The agent simply learns how good this policy is.

---

### Active Learning

The agent must learn which actions to take.

It learns both:

- values
- better actions/policy

Examples:

- Q-learning
- SARSA

```text
Passive:

Policy given
    ↓
Learn value


Active:

Experience
    ↓
Learn values
    ↓
Improve policy
```

---

## 3. Main Passive Learning Methods

The syllabus and supplied questions focus on:

1. Direct Utility Estimation
2. Monte Carlo Methods
3. Temporal Difference Learning

All three attempt to estimate state values.

---

## 4. Common Objective

For all these methods, the goal is related to estimating:

\[
V^\pi(s)
=
E_\pi[G_t|S_t=s]
\]

where:

\[
G_t=
R_{t+1}
+\gamma R_{t+2}
+\gamma^2R_{t+3}
+\cdots
\]

The difference is **how the estimate is obtained and updated**.

---

## 5. Passive Learning Example

Consider:

```text
A → B → C → Goal
```

Suppose the agent always follows a fixed policy.

The agent observes many episodes:

```text
Episode 1:
A → B → C → Goal

Episode 2:
A → B → Goal

Episode 3:
A → C → Goal
```

The learning algorithm uses these experiences to estimate:

\[
V^\pi(A),V^\pi(B),V^\pi(C)
\]

The policy itself remains fixed.

---

## 6. Important Exam Point

Passive learning is primarily about:

\[
\boxed{\text{Policy evaluation}}
\]

not policy improvement.

Therefore:

> Passive RL asks **"How good is this policy?"**

Active RL asks:

> **"What should I do?"**

---

## 7. Comparison of Passive Methods

| Method | Main idea | Needs complete episode? | Model required? |
|---|---|---:|---:|
| Direct Utility Estimation | Average observed returns | Yes, generally | No |
| Monte Carlo | Average sampled returns | Yes | No |
| TD Learning | Bootstrap from next-state estimate | No | No |

The supplied lecture describes MC as averaging sample returns and TD as learning directly from experience while using successor values. L6 (3)

---

## 8. Exam Definition

> **Passive reinforcement learning is an RL setting in which the agent follows a fixed policy and learns the value/utility of states under that policy.**

