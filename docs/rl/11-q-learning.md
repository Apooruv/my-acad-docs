# Q-Learning

## 1. Definition

**Q-Learning** is a model-free, off-policy reinforcement learning algorithm.

It learns the optimal action-value function:

\[
Q^*(s,a)
\]

without requiring an explicit model of the environment.

The supplied RL lecture explicitly characterizes Q-learning as **off-policy** and states that it directly approximates \(Q^*\), independent of the policy being followed. :chatgpt-content-reference{index="3"}

---

## 2. Objective

The objective is to learn:

\[
Q^*(s,a)
\]

Once \(Q^*\) is known, the optimal policy is:

\[
\boxed{
\pi^*(s)=\arg\max_aQ^*(s,a)
}
\]

---

## 3. Q-Learning Update Equation

The fundamental equation is:

\[
\boxed{
Q(s,a)
\leftarrow
Q(s,a)
+
\alpha
\left[
r+
\gamma\max_{a'}Q(s',a')
-
Q(s,a)
\right]
}
\]

where:

| Symbol | Meaning |
|---|---|
| \(Q(s,a)\) | Current Q-value |
| \(\alpha\) | Learning rate |
| \(r\) | Immediate reward |
| \(\gamma\) | Discount factor |
| \(s'\) | Next state |
| \(a'\) | Possible next action |

---

## 4. Q-Learning Target

The target is:

\[
\boxed{
r+\gamma\max_{a'}Q(s',a')
}
\]

Notice the:

\[
\max
\]

The algorithm assumes the best possible action will be selected from the next state.

---

## 5. TD Error

Define:

\[
\delta=
r+\gamma\max_{a'}Q(s',a')-Q(s,a)
\]

Then:

\[
\boxed{
Q(s,a)\leftarrow Q(s,a)+\alpha\delta
}
\]

This makes the formula easier to remember.

---

## 6. Interpretation of Learning Rate

\[
0\leq\alpha\leq1
\]

### Small \(\alpha\)

The update changes Q slowly.

Advantages:

- smoother learning
- less sensitivity to individual experiences

Disadvantage:

- slower adaptation

### Large \(\alpha\)

The new experience has greater influence.

Advantages:

- faster learning
- faster adaptation

Disadvantage:

- potentially unstable/noisy updates

---

## 7. Interpretation of Discount Factor

\[
0\leq\gamma\leq1
\]

### Low \(\gamma\)

Immediate rewards dominate.

### High \(\gamma\)

Future rewards become more important.

---

## 8. Why Is Q-Learning Off-Policy?

This is one of the most important exam questions.

Suppose the agent actually chooses:

\[
a'
\]

in the next state.

Q-learning does **not** necessarily use that action's Q-value.

Instead it uses:

\[
\max_{a'}Q(s',a')
\]

Therefore:

> Q-learning learns about the greedy target policy while potentially following a different behavior policy.

That is the meaning of **off-policy**.

---

## 9. Behavior Policy vs Target Policy

### Behavior policy

The policy used to generate experience.

Example:

\[
\epsilon\text{-greedy}
\]

### Target policy

The policy Q-learning is trying to learn.

For Q-learning:

\[
\boxed{
\pi_{\text{target}}(s)
=
\arg\max_aQ(s,a)
}
\]

The two policies do not have to be identical.

---

## 10. Q-Learning with Epsilon-Greedy

The agent may behave using:

\[
\epsilon\text{-greedy}
\]

but the Q-learning update still uses:

\[
\max_{a'}Q(s',a')
\]

This is exactly why Q-learning remains off-policy.

---

## 11. Basic Algorithm

```text
Initialize Q(s,a)

Repeat:

    Observe state s

    Select action a
    using ε-greedy

    Execute a

    Observe:
        reward r
        next state s'

    Update:

    Q(s,a) ← Q(s,a)
              + α[r + γ max Q(s',a')
              - Q(s,a)]

    s ← s'

Until terminal state
```

---

## 12. Numerical Structure

Whenever you see a Q-learning question:

### Step 1

Write:

\[
Q_{\text{new}}
=
Q_{\text{old}}
+
\alpha[
r+\gamma Q_{\max}(s')
-Q_{\text{old}}
]
\]

### Step 2

Substitute:

- current Q
- reward
- learning rate
- discount factor
- highest next-state Q

### Step 3

Calculate target.

### Step 4

Calculate TD error.

### Step 5

Calculate updated Q.

---

## 13. Advantages

### 1. Model-free

No transition model is required.

### 2. Off-policy

The behavior policy can differ from the target policy.

### 3. Learns optimal Q-values

Under appropriate conditions, Q-learning converges toward \(Q^*\).

### 4. Simple update rule

The algorithm is mathematically straightforward.

---

## 14. Disadvantages

### 1. Exploration problem

If important actions are never explored, their values cannot be learned properly.

### 2. Can be aggressive

The max operation assumes the best next action, even if the actual behavior is exploratory.

### 3. Tabular scalability

A Q-table becomes impractical for very large/continuous state spaces.

This limitation motivates function approximation and eventually DQN.

---

## 15. Exam Definition

> **Q-learning is a model-free, off-policy TD control algorithm that learns the optimal action-value function by updating Q-values toward the reward plus the discounted maximum next-state Q-value.**