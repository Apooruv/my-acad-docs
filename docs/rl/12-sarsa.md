# SARSA

## 1. Definition

SARSA stands for:

\[
\boxed{
\text{State-Action-Reward-State-Action}
}
\]

It is a **model-free, on-policy TD control algorithm**.

The name comes from the sequence used in the update:

\[
S_t,A_t,R_{t+1},S_{t+1},A_{t+1}
\]

The supplied lecture states that SARSA updates \(Q\) and the policy after each step and uses epsilon-soft policies for exploration. :chatgpt-content-reference{index="4"}

---

## 2. SARSA Update Equation

The update is:

\[
\boxed{
Q(s,a)
\leftarrow
Q(s,a)
+
\alpha
[
r+\gamma Q(s',a')-Q(s,a)
]
}
\]

The critical difference from Q-learning is:

\[
\boxed{Q(s',a')}
\]

instead of:

\[
\boxed{\max_{a'}Q(s',a')}
\]

---

## 3. Why Does SARSA Use \(a'\)?

Because SARSA is **on-policy**.

It uses the action that the current policy actually chooses in the next state.

Sequence:

```text
S
 ↓
A
 ↓
R
 ↓
S'
 ↓
A'
```

Then the update uses:

\[
Q(S',A')
\]

---

## 4. On-Policy Meaning

SARSA evaluates/improves the same policy that generates its experience.

If the behavior policy is epsilon-greedy, SARSA learns the value of the epsilon-greedy behavior policy.

Therefore:

> SARSA takes exploration into account when learning.

---

## 5. SARSA Algorithm

```text
Initialize Q(s,a)

Choose action a using policy π

Repeat:

    Execute a

    Observe:
        reward r
        next state s'

    Choose next action a'
    using policy π

    Update:

    Q(s,a) ← Q(s,a)
              + α[r + γQ(s',a')
              - Q(s,a)]

    s ← s'
    a ← a'

Until terminal state
```

---

## 6. SARSA vs Q-Learning

Suppose:

```text
Current:
S, A

Next state:
S'

Possible next actions:
B1, B2, B3
```

Suppose:

\[
Q(S',B_1)=2
\]

\[
Q(S',B_2)=5
\]

\[
Q(S',B_3)=3
\]

### Q-learning

Uses:

\[
\max(2,5,3)=5
\]

### SARSA

Suppose the actual policy selects \(B_1\).

Then SARSA uses:

\[
Q(S',B_1)=2
\]

Therefore, the two algorithms can produce different updates.

---

## 7. Exploration Is Part of SARSA's Learning

Suppose:

\[
\epsilon>0
\]

The agent occasionally takes risky/exploratory actions.

SARSA's update uses the action actually selected by the epsilon-greedy policy.

Therefore the learned values reflect the consequences of following that exploratory policy.

---

## 8. Advantages

### 1. On-policy learning

The learned values reflect the actual behavior policy.

### 2. Naturally accounts for exploration

The update considers the action actually selected.

### 3. Can be safer in risky environments

If exploratory actions can lead to poor outcomes, SARSA incorporates those outcomes into its value estimates.

---

## 9. Disadvantages

### 1. Can learn a more conservative policy

Because it accounts for exploratory behavior.

### 2. Depends on the behavior policy

Changing the exploration strategy can change the learned values.

### 3. Potentially slower to reach a purely greedy optimum

If substantial exploration is maintained.

---

## 10. Exam Definition

> **SARSA is a model-free, on-policy TD control algorithm that updates \(Q(s,a)\) using the actual next action \(a'\) selected by the current policy.**

---

## 11. Memory Trick

### SARSA

\[
\boxed{
S-A-R-S-A
}
\]

Use:

\[
\boxed{
Q(s',a')
}
\]

### Q-learning

Think:

\[
\boxed{
\max Q(s',a')
}
\]

This is the single most important mathematical difference.

