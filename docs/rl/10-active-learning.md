# Active Learning

## 1. What is Active Learning?

In **active reinforcement learning**, the agent does not receive a fixed policy.

Instead, the agent must learn:

- which actions to take
- which actions are valuable
- an increasingly better policy

The goal is to find an optimal policy:

\[
\pi^*
\]

that maximizes cumulative reward.

---

## 2. Passive vs Active Learning

### Passive Learning

The policy is already given.

The agent learns:

\[
\pi \rightarrow V^\pi
\]

Example:

> Always move right whenever possible.

The agent only evaluates this policy.

### Active Learning

The agent must decide which actions are good.

```text
Experience
    ↓
Estimate action values
    ↓
Choose actions
    ↓
Receive rewards
    ↓
Improve estimates
    ↓
Improve policy
```

---

## 3. Main Active Learning Methods in This Syllabus

The important methods are:

1. Q-Learning
2. SARSA

Both learn action values:

\[
Q(s,a)
\]

rather than only:

\[
V(s)
\]

This is important because the agent must decide **which action is best**.

---

## 4. Why Q-values?

Suppose the agent is in state \(S\):

```text
       S
    /  |  \
   A   B   C
```

The state-value function tells us:

\[
V(S)
\]

But the agent needs to know:

\[
Q(S,A)
\]

\[
Q(S,B)
\]

\[
Q(S,C)
\]

Then it can choose:

\[
\arg\max_aQ(S,a)
\]

---

## 5. Exploration vs Exploitation

An active agent faces a fundamental problem.

### Exploitation

Choose the action currently believed to be best.

\[
a=\arg\max_aQ(s,a)
\]

### Exploration

Try other actions to discover whether they may actually be better.

```text
Known action
     ↓
Good reward
     ↓
Exploit

Unknown action
     ↓
Try it
     ↓
Maybe discover better action
     ↓
Explore
```

---

## 6. Why Pure Exploitation Fails

Suppose:

\[
Q(A)=5
\]

\[
Q(B)=3
\]

A greedy agent always chooses A.

But suppose the true values are:

\[
Q^*(A)=5
\]

\[
Q^*(B)=10
\]

The agent will never discover that B is better.

Therefore:

> An agent must explore sufficiently before relying on exploitation.

The supplied lecture explicitly notes that a deterministic/greedy policy may fail to explore all actions and recommends soft policies. reinforcement-learning (5) (2) …

---

## 7. Epsilon-Greedy Strategy

The most important exploration strategy for this syllabus is:

\[
\epsilon\text{-greedy}
\]

With probability:

\[
1-\epsilon
\]

choose the greedy action.

With probability:

\[
\epsilon
\]

choose an exploratory action.

So:

```text
             Choose action
                  │
          ┌───────┴───────┐
          │               │
       1 - ε               ε
          │               │
          ▼               ▼
      Greedy            Random
       action            action
```

The supplied RL material describes exactly this mechanism. reinforcement-learning (5) (2) …

---

## 8. Decaying Epsilon

A common strategy is to gradually reduce \(\epsilon\).

Example:

\[
\epsilon=1.0
\rightarrow0.8
\rightarrow0.5
\rightarrow0.2
\rightarrow0.1
\]

Early training:

> Explore heavily.

Later training:

> Exploit more of what has been learned.

---

## 9. Other Exploration Methods

For exam purposes, know these names:

### 1. Epsilon-greedy

Random exploration with probability \(\epsilon\).

### 2. Softmax/Boltzmann exploration

Actions are selected probabilistically based on their estimated values.

### 3. Decaying epsilon

Start with high exploration and gradually reduce it.

### 4. Optimistic initialization

Initialize action values optimistically so that unexplored actions are attractive initially.

---

## 10. Active Learning vs Passive Learning

| Feature | Passive | Active |
|---|---|---|
| Policy | Fixed | Learned/improved |
| Main objective | Evaluate policy | Find good policy |
| Main value | \(V^\pi(s)\) | \(Q(s,a)\) |
| Exploration | Usually not central | Essential |
| Examples | MC, TD policy evaluation | Q-learning, SARSA |

---

## 11. Exam Definition

> **Active reinforcement learning is a setting in which the agent must learn which actions to take while interacting with the environment, rather than merely evaluating a fixed policy.**

---

## 12. Key Exam Points

Remember:

- Active learning requires policy improvement.
- Q-learning and SARSA learn \(Q(s,a)\).
- Exploration is required to discover potentially better actions.
- Exploitation uses the currently best-known action.
- Epsilon-greedy balances exploration and exploitation.
- Usually \(\epsilon\) is reduced during training.

