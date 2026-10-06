# Unit 4 — Passive and Active Reinforcement Learning

## Source PDF

[RL Question Bank](pdfs/QUESTIONS%20_rl%20%282%29.pdf)

---

# 1. Passive vs Active Learning

Before solving the questions, distinguish these two types.

## Passive Learning

The agent follows a fixed policy:

\[
\pi
\]

and learns how good that policy is.

The agent does **not** try to improve the policy.

The main objective is:

\[
\boxed{\text{Estimate }V^\pi(s)}
\]

Important methods:

1. Direct Utility Estimation
2. Monte Carlo Learning
3. Temporal Difference Learning

---

## Active Learning

The agent must learn:

1. which actions are good;
2. which policy to follow.

Therefore:

\[
\boxed{\text{Learn both values and a good policy}}
\]

Important methods:

1. Q-Learning
2. SARSA

---

# Q15. Direct Utility Estimation

> **Question:** Explain how Direct Utility Estimation works in Passive Learning. Why might this method be inefficient in environments with large state spaces or with limited observed data?

## Answer

Direct Utility Estimation estimates the utility/value of a state by observing the actual returns obtained after visiting that state.

The agent follows a fixed policy:

\[
\pi
\]

and observes complete episodes.

For a state \(s\), suppose the agent visits the state several times and obtains returns:

\[
G_1,G_2,\ldots,G_n
\]

The estimated utility is the average return:

\[
\boxed{
V(s)\approx
\frac{1}{n}
\sum_{i=1}^{n}G_i
}
\]

---

# Example

Suppose state \(A\) is visited three times.

The observed returns are:

\[
5,\;7,\;3
\]

Then:

\[
V(A)
=
\frac{5+7+3}{3}
\]

\[
\boxed{V(A)=5}
\]

If another episode gives return \(9\):

\[
V(A)
=
\frac{5+7+3+9}{4}
\]

\[
\boxed{V(A)=6}
\]

Thus the value estimate is simply based on observed returns.

---

# Advantages

### 1. Simple

The method is easy to understand and implement.

### 2. Model-free

It does not require:

- transition probabilities;
- reward model;
- environment dynamics.

### 3. Direct estimate

The actual returns provide direct information about the utility.

---

# Limitations

## 1. Requires complete episodes

The return is known only after the outcome of the episode is observed.

Therefore, learning can be slow when episodes are long.

---

## 2. Large state spaces

Suppose there are thousands or millions of states.

Each state may need to be visited many times to obtain a reliable average.

Therefore:

\[
\boxed{
\text{Large state space}
\Rightarrow
\text{poor state coverage}
}
\]

---

## 3. Limited data

If a state is observed only a few times, its estimated utility can have high variance.

For example, if state \(A\) is observed once:

\[
V(A)=G_1
\]

There is no averaging over multiple experiences.

---

## 4. No generalization

A state must generally be observed to estimate its value.

Information from one state is not automatically transferred to another state.

---

# Exam conclusion

> Direct Utility Estimation estimates a state's value by averaging the returns observed after visits to that state. It is simple and model-free, but inefficient for large state spaces or limited data because many visits may be required to obtain reliable estimates.

---

# Q16. Temporal Difference Learning

> **Question:** Describe the key concept of Temporal Difference Learning. How does TD learning update the value of a state differently from Direct Utility Estimation and Monte Carlo Methods?

## Answer

Temporal Difference (TD) learning is a model-free learning method that updates value estimates using:

\[
\boxed{\text{current reward + estimated value of the next state}}
\]

The important idea is that TD learning does **not** need to wait until the complete episode finishes.

---

# TD Update

For a state-value function:

\[
\boxed{
V(s)
\leftarrow
V(s)
+
\alpha
[
r+\gamma V(s')-V(s)
]
}
\]

where:

- \(V(s)\) = current estimate;
- \(r\) = immediate reward;
- \(\gamma\) = discount factor;
- \(V(s')\) = estimate of next state;
- \(\alpha\) = learning rate.

The quantity:

\[
\boxed{
\delta=
r+\gamma V(s')-V(s)
}
\]

is called the **TD error**.

Therefore:

\[
\boxed{
V(s)\leftarrow V(s)+\alpha\delta
}
\]

---

# Example

Suppose:

\[
V(s)=4
\]

\[
r=2
\]

\[
\gamma=0.9
\]

\[
V(s')=6
\]

and:

\[
\alpha=0.1
\]

First calculate the TD target:

\[
r+\gamma V(s')
=
2+0.9(6)
\]

\[
=7.4
\]

TD error:

\[
\delta=7.4-4
\]

\[
\delta=3.4
\]

Update:

\[
V_{\text{new}}(s)
=
4+0.1(3.4)
\]

\[
\boxed{V_{\text{new}}(s)=4.34}
\]

---

# TD vs Direct Utility Estimation

Direct Utility Estimation uses complete observed returns:

\[
\boxed{
V(s)\approx\text{average of complete returns}
}
\]

TD instead bootstraps from the estimated value of the next state:

\[
\boxed{
V(s)\leftarrow
V(s)+
\alpha[r+\gamma V(s')-V(s)]
}
\]

Therefore TD can learn before the episode terminates.

---

# TD vs Monte Carlo

Monte Carlo uses the actual return:

\[
G_t=
R_{t+1}
+\gamma R_{t+2}
+\gamma^2R_{t+3}
+\cdots
\]

and updates after the episode/trajectory reaches its terminal point.

TD uses:

\[
r+\gamma V(s')
\]

and therefore updates after each transition.

---

# Comparison

| Method | Target | Must wait until episode ends? |
|---|---|---|
| Direct Utility Estimation | Average observed return | Yes |
| Monte Carlo | Actual complete return \(G_t\) | Yes |
| TD | \(r+\gamma V(s')\) | No |

---

# Key concept: Bootstrapping

TD uses an estimate to improve another estimate:

\[
\boxed{
V(s')\rightarrow\text{target for }V(s)
}
\]

This is called **bootstrapping**.

Monte Carlo does not bootstrap from \(V(s')\).

---

# Exam conclusion

> Temporal Difference learning updates a state's value after each transition using the immediate reward and the estimated value of the next state. Unlike Monte Carlo and Direct Utility Estimation, TD does not need to wait for the complete episode to finish. Its defining feature is bootstrapping.

---

# Q17. Monte Carlo Methods in Passive Learning

> **Question:** Explain the advantages and disadvantages of Monte Carlo methods in Passive Learning. Why might it be impractical to use Monte Carlo methods in continuous or highly variable environments?

## Answer

Monte Carlo (MC) methods estimate state values from complete episodes.

For a state \(s_t\), the return is:

\[
\boxed{
G_t=
R_{t+1}
+\gamma R_{t+2}
+\gamma^2R_{t+3}
+\cdots
}
\]

The value estimate is based on observed returns.

For example:

\[
V(s)
\approx
\text{average of observed }G_t
\]

---

# How Monte Carlo Learning Works

1. Follow the policy.
2. Generate an episode.
3. Observe the complete sequence of rewards.
4. Calculate the return for visited states.
5. Update their value estimates.
6. Repeat for many episodes.

---

# Advantages

## 1. Model-free

MC does not require:

\[
P(s'|s,a)
\]

or a reward model.

---

## 2. Uses actual returns

The target is based on the actual outcome:

\[
G_t
\]

rather than a bootstrapped estimate.

---

## 3. Conceptually simple

The method is straightforward:

\[
\boxed{
\text{Observe return}
\rightarrow
\text{update value}
}
\]

---

## 4. No bootstrapping

MC does not use:

\[
V(s')
\]

to estimate:

\[
V(s)
\]

The actual observed return is used.

---

# Disadvantages

## 1. Must wait for episode completion

The agent cannot calculate the final return until the episode finishes.

Therefore:

\[
\boxed{
\text{Long episode}
\Rightarrow
\text{delayed learning}
}
\]

---

## 2. High variance

Returns can vary significantly between episodes.

For example:

\[
G_1=2
\]

\[
G_2=15
\]

\[
G_3=-4
\]

The resulting estimate can fluctuate substantially.

---

## 3. Problem with continuous environments

In continuous or very long environments:

- episodes may be extremely long;
- terminal states may rarely occur;
- there may be no natural episode boundary.

Therefore calculating complete returns becomes impractical.

---

## 4. Inefficient in highly variable environments

If the environment produces highly variable trajectories, many complete episodes may be needed to obtain a reliable average.

---

# Why TD can be preferable

TD can update after every transition:

\[
V(s)
\leftarrow
V(s)
+
\alpha[
r+\gamma V(s')-V(s)
]
\]

Therefore, it can learn incrementally without waiting for the final outcome.

---

# Exam conclusion

> Monte Carlo methods are simple and model-free and use actual complete returns without bootstrapping. However, they must wait until an episode ends and can have high variance. These disadvantages make them less practical for very long, continuous, or highly variable environments.

---

# Q18. Comparison of Passive Learning Methods

> **Question:** Compare and contrast Direct Utility Estimation, Temporal Difference Learning, and Monte Carlo Methods. In what types of environments or scenarios might each method perform best, and why?

## Answer

The three methods estimate the value of states under a policy, but they use different targets.

---

# 1. Direct Utility Estimation

The value is estimated by averaging observed returns:

\[
\boxed{
V(s)=
\frac{1}{N}
\sum_{i=1}^{N}G_i
}
\]

### Best suited for

- small state spaces;
- episodic environments;
- situations where sufficient complete episodes are available.

### Main limitation

Requires enough visits to each state.

---

# 2. Monte Carlo

MC also uses complete returns:

\[
\boxed{
G_t=
R_{t+1}
+\gamma R_{t+2}
+\cdots
}
\]

### Best suited for

- episodic environments;
- situations where complete episodes are easy to generate;
- problems where using actual returns is desirable.

### Main limitation

Must wait until the episode ends.

---

# 3. Temporal Difference

TD uses:

\[
\boxed{
r+\gamma V(s')
}
\]

as its target.

### Best suited for

- continuing environments;
- long episodes;
- online learning;
- situations where frequent incremental updates are useful.

---

# Comparison Table

| Feature | Direct Utility | Monte Carlo | TD |
|---|---|---|---|
| Model-free | Yes | Yes | Yes |
| Uses complete return | Yes | Yes | No |
| Bootstrapping | No | No | Yes |
| Episode must finish | Generally yes | Yes | No |
| Online updates | No | No | Yes |
| Variance | Can be high | High | Lower generally |
| Bias | Low from bootstrapping | Low | Some bootstrapping bias |
| Good for continuing tasks | Poor | Poor | Good |

---

# Important distinction

The key difference is the learning target.

### Direct Utility Estimation

\[
\boxed{\text{Average observed returns}}
\]

### Monte Carlo

\[
\boxed{\text{Complete actual return}}
\]

### TD

\[
\boxed{\text{Immediate reward + estimated next value}}
\]

---

# Exam conclusion

> Direct Utility Estimation and Monte Carlo methods rely on complete observed returns, whereas TD learning bootstraps from the estimated value of the next state. MC and direct estimation are natural for episodic environments, while TD is generally better suited to online, long-running or continuing environments because it can update after every transition.

---

# Q19. Exploration–Exploitation in Q-Learning

> **Question:** Describe the significance of the exploration-exploitation tradeoff in Q-Learning. What methods can be used to balance this tradeoff, and how does the choice of method affect the agent’s learning process?

## Answer

In Q-Learning, the agent must decide between:

### Exploration

Trying actions whose value is uncertain.

### Exploitation

Choosing the action with the highest known Q-value:

\[
\boxed{
a^*=\arg\max_aQ(s,a)
}
\]

---

# Why is the trade-off important?

If the agent always exploits:

\[
\boxed{
\text{It may never discover a better action}
}
\]

If the agent explores too much:

\[
\boxed{
\text{Learning becomes inefficient}
}
\]

Therefore:

\[
\boxed{
\text{Good learning requires a balance}
}
\]

---

# Methods

## 1. Epsilon-Greedy

With probability:

\[
\epsilon
\]

choose randomly.

With probability:

\[
1-\epsilon
\]

choose the greedy action.

Usually:

\[
\epsilon\downarrow
\]

during training.

### Effect

- early: more exploration;
- later: more exploitation.

---

# 2. Epsilon Decay

Start with high:

\[
\epsilon
\]

and gradually reduce it.

For example:

\[
1.0\rightarrow0.5\rightarrow0.1\rightarrow0.01
\]

This allows the agent to explore early and exploit later.

---

# 3. Softmax/Boltzmann

Actions are selected probabilistically based on their Q-values.

Higher Q-values receive higher probabilities.

Conceptually:

\[
P(a|s)
=
\frac{e^{Q(s,a)/\tau}}
{\sum_b e^{Q(s,b)/\tau}}
\]

where:

\[
\tau
\]

controls exploration.

High temperature:

\[
\tau\uparrow
\Rightarrow
\text{more exploration}
\]

Low temperature:

\[
\tau\downarrow
\Rightarrow
\text{more greedy behavior}
\]

---

# 4. Optimistic Initialization

Initialize Q-values relatively high.

The agent is then encouraged to try actions because untried actions initially appear valuable.

---

# Effect on learning

| More exploration | More exploitation |
|---|---|
| Better discovery | Better immediate reward |
| More diverse experience | Faster use of known knowledge |
| Slower short-term performance | Risk of local/suboptimal policy |
| Useful early | Useful later |

### Exam conclusion

> Exploration allows Q-Learning to discover potentially better actions, while exploitation uses the best actions currently known. Epsilon-greedy with decay is the standard approach because it encourages exploration early and gradually shifts toward exploitation.

---

# Q20. SARSA vs Q-Learning

> **Question:** Explain the main difference between SARSA and Q-Learning in terms of policy updates. How does SARSA’s approach to on-policy learning impact the types of policies the agent learns compared to Q-Learning?

## Answer

The central difference is:

\[
\boxed{
\text{SARSA = On-policy}
}
\]

\[
\boxed{
\text{Q-Learning = Off-policy}
}
\]

---

# Q-Learning

Q-Learning uses:

\[
\boxed{
Q(s,a)
\leftarrow
Q(s,a)
+
\alpha[
r+
\gamma\max_{a'}Q(s',a')
-Q(s,a)]
}
\]

It assumes the best possible action in the next state.

Therefore, it learns the optimal greedy policy even if the agent behaves using an exploratory policy.

---

# SARSA

SARSA stands for:

\[
\boxed{
\text{State-Action-Reward-State-Action}
}
\]

The update is:

\[
\boxed{
Q(s,a)
\leftarrow
Q(s,a)
+
\alpha[
r+
\gamma Q(s',a')
-Q(s,a)]
}
\]

where \(a'\) is the **actual next action selected by the policy**.

---

# Main Difference

### Q-Learning

Uses:

\[
\max_{a'}Q(s',a')
\]

It asks:

> What is the best action I could take next?

### SARSA

Uses:

\[
Q(s',a')
\]

It asks:

> What action will my current policy actually take next?

---

# Example

Suppose in state \(s'\):

\[
Q(s',a_1)=10
\]

\[
Q(s',a_2)=7
\]

The agent's exploratory policy selects:

\[
a_2
\]

### Q-Learning

Uses:

\[
\max(10,7)=10
\]

### SARSA

Uses:

\[
Q(s',a_2)=7
\]

Therefore, the two algorithms can learn different values.

---

# Why does SARSA produce a different policy?

SARSA learns the value of the policy that the agent is actually following.

If the policy is exploratory:

\[
\epsilon>0
\]

then SARSA accounts for the possibility that the agent may choose a non-greedy action.

Therefore, SARSA can learn a more conservative policy.

---

# Classic interpretation

Consider a dangerous state near a cliff.

A greedy path may pass close to the cliff.

An exploratory policy has a chance of taking a random action and falling.

### Q-Learning

Assumes the next action will be the best action:

\[
\max Q
\]

Therefore it may learn the shortest risky path.

### SARSA

Accounts for the actual exploratory action.

Therefore it can learn a safer path.

---

# Exam conclusion

> Q-Learning is off-policy because it learns using the maximum next-state Q-value regardless of the action actually taken. SARSA is on-policy because it updates using the Q-value of the actual next action selected by the current policy. Consequently, SARSA incorporates exploration into its learned policy and may produce safer or more conservative behavior.

---

# Q21. Q-Learning vs SARSA

> **Question:** Discuss the advantages and disadvantages of Q-Learning versus SARSA. In what scenarios would SARSA be preferred over Q-Learning, and vice versa?

## Answer

# Q-Learning

Q-Learning is an:

\[
\boxed{\text{Off-policy TD control algorithm}}
\]

Its update is:

\[
\boxed{
Q(s,a)
\leftarrow
Q(s,a)
+
\alpha[
r+
\gamma\max_{a'}Q(s',a')
-Q(s,a)]
}
\]

---

## Advantages of Q-Learning

### 1. Learns the optimal greedy policy

It directly targets:

\[
\max_{a'}Q(s',a')
\]

### 2. Off-policy

The behavior policy can be exploratory while the learned policy approaches the greedy optimal policy.

### 3. Simple

The update rule is straightforward.

---

## Disadvantages

### 1. Can produce risky behavior

It assumes optimal future actions even if the actual behavior is exploratory.

### 2. May ignore exploration risk

In environments where random actions have severe consequences, the learned policy may be less conservative.

### 3. Q-value overestimation

With function approximation and max operations, Q-Learning can suffer from overestimation.

This motivates techniques such as:

\[
\boxed{\text{Double Q-Learning / Double DQN}}
\]

---

# SARSA

SARSA is an:

\[
\boxed{\text{On-policy TD control algorithm}}
\]

Its update is:

\[
\boxed{
Q(s,a)
\leftarrow
Q(s,a)
+
\alpha[
r+
\gamma Q(s',a')
-Q(s,a)]
}
\]

---

## Advantages of SARSA

### 1. Accounts for actual behavior

The next action \(a'\) is the action actually selected.

### 2. Safer in risky environments

If exploration itself can lead to bad outcomes, SARSA learns to account for that.

### 3. Suitable for stochastic/exploratory behavior

The learned values correspond to the behavior policy being followed.

---

## Disadvantages

### 1. Can learn a less optimal greedy policy

Because it evaluates the behavior policy, including exploration.

### 2. Sensitive to exploration strategy

Changing the behavior policy can change the learned values.

### 3. May be slower to reach the purely greedy optimum

It does not directly use:

\[
\max Q
\]

in the update.

---

# When should SARSA be preferred?

SARSA is preferable when:

- safety matters;
- exploratory actions have significant consequences;
- the actual behavior policy matters;
- the environment is risky.

Examples:

- robot navigation near dangerous obstacles;
- autonomous systems;
- safety-critical control.

---

# When should Q-Learning be preferred?

Q-Learning is preferable when:

- the goal is to learn the optimal greedy policy;
- exploration can be separated from the target policy;
- off-policy learning is useful;
- the environment is not highly sensitive to exploratory actions.

---

# Final Comparison

| Feature | Q-Learning | SARSA |
|---|---|---|
| Type | Off-policy | On-policy |
| Next action in update | Best possible action | Actual next action |
| Update target | \(\max Q(s',a')\) | \(Q(s',a')\) |
| Considers exploration in target? | No | Yes |
| Typical behavior | More aggressive/greedy | More conservative |
| Risk-sensitive environments | Less suitable | More suitable |
| Optimal greedy policy | Directly targeted | Depends on behavior policy |

---

# Most Important Formulas for Unit 4

## Direct Utility Estimation

\[
\boxed{
V(s)\approx
\frac{1}{N}
\sum_{i=1}^{N}G_i
}
\]

## Monte Carlo

\[
\boxed{
G_t=
R_{t+1}
+\gamma R_{t+2}
+\gamma^2R_{t+3}
+\cdots
}
\]

## TD Learning

\[
\boxed{
V(s)
\leftarrow
V(s)
+
\alpha[
r+\gamma V(s')-V(s)
]
}
\]

## Q-Learning

\[
\boxed{
Q(s,a)
\leftarrow
Q(s,a)
+
\alpha[
r+\gamma\max_{a'}Q(s',a')
-Q(s,a)
]
}
\]

## SARSA

\[
\boxed{
Q(s,a)
\leftarrow
Q(s,a)
+
\alpha[
r+\gamma Q(s',a')
-Q(s,a)
]
}
\]

---

# The Most Important Differences

## Monte Carlo vs TD

\[
\boxed{
MC:\text{ complete return}
}
\]

\[
\boxed{
TD:\text{ one-step bootstrapping}
}
\]

## Q-Learning vs SARSA

\[
\boxed{
Q\text{-Learning: }\max Q
}
\]

\[
\boxed{
SARSA:\text{ actual next action}
}
\]

## Passive vs Active

\[
\boxed{
Passive:\text{ evaluate fixed policy}
}
\]

\[
\boxed{
Active:\text{ learn which actions/policy is best}
}
