
# Returns and Value Functions

## 1. Return

The **return** is the cumulative reward obtained from a state onward.

For an undiscounted episodic task:

\[
G_t=R_{t+1}+R_{t+2}+R_{t+3}+\cdots
\]

For discounted rewards:

\[
G_t=
R_{t+1}
+\gamma R_{t+2}
+\gamma^2R_{t+3}
+\cdots
\]

where:

\[
0\leq\gamma\leq1
\]

---

## 2. Discount Factor

The discount factor \(\gamma\) determines how much importance is given to future rewards.

### If \(\gamma=0\)

Only the immediate reward matters.

\[
G_t=R_{t+1}
\]

The agent is extremely short-sighted.

### If \(\gamma\approx1\)

Future rewards are highly important.

The agent becomes more long-term oriented.

---

## 3. Example of Discounted Return

Suppose an agent receives:

```text
Reward 1 = -1
Reward 2 = -1
Reward 3 = +10
```

with:

\[
\gamma=0.9
\]

Then:

\[
G_0=-1+0.9(-1)+0.9^2(10)
\]

\[
G_0=-1-0.9+8.1
\]

\[
\boxed{G_0=6.2}
\]

---

## 4. State-Value Function

The state-value function measures the expected return from a state when following policy \(\pi\).

\[
\boxed{
V^\pi(s)=E_\pi[G_t|S_t=s]
}
\]

In words:

> \(V^\pi(s)\) tells us how good it is to be in state \(s\) when following policy \(\pi\).

---

## 5. Action-Value Function

The action-value function measures the expected return when:

1. starting from state \(s\),
2. taking action \(a\),
3. then following policy \(\pi\).

\[
\boxed{
Q^\pi(s,a)=E_\pi[G_t|S_t=s,A_t=a]
}
\]

In words:

> \(Q^\pi(s,a)\) tells us how good it is to take action \(a\) in state \(s\).

---

## 6. Difference Between V and Q

| Function | Meaning |
|---|---|
| \(V^\pi(s)\) | Value of a state |
| \(Q^\pi(s,a)\) | Value of taking an action in a state |

Example:

```text
State S
 ├── Up      → Q(S,Up)
 ├── Down    → Q(S,Down)
 ├── Left    → Q(S,Left)
 └── Right   → Q(S,Right)
```

The state value summarizes the expected outcome under the policy.

The action value tells us which particular action is useful.

---

## 7. Relationship Between V and Q

For a stochastic policy:

\[
V^\pi(s)
=
\sum_a\pi(a|s)Q^\pi(s,a)
\]

This means the value of a state is the weighted average of the values of its possible actions.

For a deterministic policy:

\[
V^\pi(s)=Q^\pi(s,\pi(s))
\]

---

## 8. Optimal Value Function

The optimal state-value function is:

\[
\boxed{
V^*(s)=\max_\pi V^\pi(s)
}
\]

It represents the maximum expected return achievable from state \(s\).

Similarly:

\[
\boxed{
Q^*(s,a)=\max_\pi Q^\pi(s,a)
}
\]

---

## 9. Optimal Policy

Once \(Q^*(s,a)\) is known:

\[
\boxed{
\pi^*(s)=\arg\max_a Q^*(s,a)
}
\]

Therefore, choose the action with the largest optimal Q-value.

Similarly, using the optimal value function:

\[
\pi^*(s)
=
\arg\max_a
\sum_{s'}P(s'|s,a)
[R+\gamma V^*(s')]
\]

---

## 10. Why Value Functions Matter

Instead of searching through complete future action sequences, RL algorithms use value functions to summarize future rewards.

For example:

```text
Current state
     ↓
Value function
     ↓
Estimate future return
     ↓
Choose better action
```

This is the basis for:

- Bellman equations
- Dynamic Programming
- Policy Iteration
- Value Iteration
- Q-Learning
- SARSA
- DQN

---

## 11. Exam Trap: Reward vs Return vs Value

These three terms are different.

### Reward

Immediate feedback:

\[
R_{t+1}
\]

### Return

Cumulative future reward:

\[
G_t=R_{t+1}+\gamma R_{t+2}+\cdots
\]

### Value

Expected return:

\[
V^\pi(s)=E_\pi[G_t|S_t=s]
\]

Remember:

> **Reward = immediate**

> **Return = accumulated**

> **Value = expected return**

---

## 12. Exam Shortcut

When a question asks:

> "What is the value of state \(s\)?"

Think:

\[
V(s)=\text{expected future return from }s
\]

When it asks:

> "What is the value of taking action \(a\) in state \(s\)?"

Think:

\[
Q(s,a)=\text{expected future return after taking }a
\]
```

---
