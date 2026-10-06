# Q-Learning vs SARSA

## 1. Core Difference

The most important distinction is:

### Q-Learning

Off-policy:

\[
\boxed{
Q(s,a)\leftarrow
Q(s,a)+
\alpha[
r+\gamma\max_{a'}Q(s',a')
-Q(s,a)]
}
\]

### SARSA

On-policy:

\[
\boxed{
Q(s,a)\leftarrow
Q(s,a)+
\alpha[
r+\gamma Q(s',a')
-Q(s,a)]
}
\]

---

# 2. Side-by-Side

| Feature | Q-Learning | SARSA |
|---|---|---|
| Type | Model-free | Model-free |
| Policy | Off-policy | On-policy |
| Target | Greedy next action | Actual next action |
| Formula | \(\max Q(s',a')\) | \(Q(s',a')\) |
| Exploration considered in target? | No | Yes |
| Learns | Optimal greedy policy | Policy being followed |
| Behavior can differ from target? | Yes | No |
| Typical behavior | More aggressive | More conservative |

---

# 3. The Critical Numerical Difference

Suppose:

\[
Q(s',a_1)=2
\]

\[
Q(s',a_2)=8
\]

\[
Q(s',a_3)=4
\]

The actual next action selected is \(a_1\).

### Q-Learning

\[
Q_{\text{target}}
=
r+\gamma\max(2,8,4)
\]

\[
=r+8\gamma
\]

### SARSA

\[
Q_{\text{target}}
=
r+\gamma Q(s',a_1)
\]

\[
=r+2\gamma
\]

Therefore the targets can be very different.

---

# 4. Cliff/Risky Environment Intuition

Consider a risky path:

```text
Start ── Safe ── Goal
  \
   └── Risky ── Cliff
```

Suppose the greedy path appears short but exploration sometimes causes the agent to fall.

### Q-Learning

The target uses:

\[
\max Q(s',a')
\]

It assumes the best action will be taken next.

Therefore it may learn an aggressive shortest path.

### SARSA

SARSA considers the action actually selected under the exploratory policy.

Therefore it can learn that the risky path has a lower expected value when exploration is included.

This is why SARSA can produce safer/more conservative behavior.

---

# 5. Exploration-Exploitation Question

### Question

> Describe the significance of the exploration-exploitation tradeoff in Q-Learning. What methods can be used to balance this tradeoff?

### Answer

The agent must balance exploiting the best-known action with exploring other actions that may produce better rewards.

Pure exploitation can cause the agent to become stuck with a suboptimal action because it never discovers better alternatives. Pure exploration wastes opportunities to use actions that are already known to perform well.

A common solution is epsilon-greedy exploration:

\[
P(\text{greedy})=1-\epsilon
\]

\[
P(\text{explore})=\epsilon
\]

The value of \(\epsilon\) can be gradually reduced during training so that the agent explores more initially and exploits more later. The supplied lecture explicitly recommends soft policies and epsilon-greedy exploration for this reason. reinforcement-learning (5) (2) …

---

# 6. Question: Main Difference Between SARSA and Q-Learning

### Answer

Q-learning is an off-policy algorithm. It updates the current Q-value using the maximum Q-value among possible actions in the next state:

\[
r+\gamma\max_{a'}Q(s',a')
\]

SARSA is on-policy and uses the Q-value of the actual next action selected by the current policy:

\[
r+\gamma Q(s',a')
\]

Therefore SARSA learns the value of the policy actually being followed, including its exploratory behavior, whereas Q-learning learns toward the greedy optimal policy even if the agent is using an exploratory behavior policy.

---

# 7. Advantages of Q-Learning

- Model-free
- Off-policy
- Can learn optimal greedy policy while using exploratory behavior
- Simple update rule
- Does not require an environment model

### Disadvantages

- Requires sufficient exploration
- Can be overly optimistic/aggressive in some environments
- Tabular Q-values do not scale well to huge state spaces
- Sensitive to learning parameters

---

# 8. Advantages of SARSA

- Model-free
- On-policy
- Learns according to actual behavior
- Naturally accounts for exploration
- Can be preferable where risky exploratory behavior should influence the learned policy

### Disadvantages

- More dependent on exploration strategy
- Can learn conservatively
- May converge more slowly toward a purely greedy behavior
- Still suffers from tabular scalability issues

---

# 9. When Should SARSA Be Preferred?

Prefer SARSA when:

- the behavior policy itself matters
- exploration has real consequences
- risky actions should reduce the learned value
- a conservative policy is desirable

Example:

> A robot operating near dangerous states where exploratory actions can cause large penalties.

---

# 10. When Should Q-Learning Be Preferred?

Prefer Q-learning when:

- the goal is to learn the optimal greedy policy
- exploration can be separated from the target policy
- the environment is less sensitive to exploratory actions
- an off-policy method is desirable

---

# 11. Important Exam Table

| Question | Q-Learning | SARSA |
|---|---|---|
| Policy type | Off-policy | On-policy |
| Next action | Best possible action | Actual selected action |
| Target | \(r+\gamma\max Q\) | \(r+\gamma Q(s',a')\) |
| Exploration reflected? | No, in target | Yes |
| Behavior policy = target? | No | Yes |
| More aggressive? | Often | Often more conservative |
| Risk-sensitive setting | Less suitable in some cases | Often preferable |
| Main keyword | **MAX** | **ACTUAL NEXT ACTION** |

---

# 12. One-Line Memory Rule

> **Q-learning asks: "What if I take the best next action?"**

> **SARSA asks: "What action will my current policy actually take next?"**