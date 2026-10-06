# Solutions — QUESTIONS_rl (2)

## Source PDF

[Open QUESTIONS_rl (2).pdf](pdfs/QUESTIONS%20_rl%20%282%29.pdf)

---

# Q1. Q-Learning with DQN

> A robot uses a Deep Q-Network (DQN) for navigating a grid. The network has four actions: up, down, left, and right, each giving a reward of +10 if it reaches the goal state or -1 otherwise. The robot starts from the top-left cell (0,0) and the goal is located at the bottom-right cell (4,4).
>
> If the discount factor is 0.9 and learning rate is 0.1, calculate the Q-value update for taking an action that moves from (1,1) to (1,2) with the current Q-value at 5. Show the Q-value update calculation using the Bellman equation.

## Given

\[
Q(s,a)=5
\]

\[
\alpha=0.1
\]

\[
\gamma=0.9
\]

The transition is:

\[
(1,1)\rightarrow(1,2)
\]

Since \((1,2)\) is not the goal:

\[
r=-1
\]

---

## DQN / Q-Learning update

\[
Q_{\text{new}}(s,a)
=
Q(s,a)
+
\alpha
\left[
r+\gamma\max_{a'}Q(s',a')
-Q(s,a)
\right]
\]

Therefore:

\[
Q_{\text{new}}
=
5+
0.1
\left[
-1+
0.9\max_{a'}Q((1,2),a')
-5
\right]
\]

Let:

\[
M=\max_{a'}Q((1,2),a')
\]

Then:

\[
Q_{\text{new}}
=
5+0.1[-6+0.9M]
\]

\[
\boxed{
Q_{\text{new}}=4.4+0.09M
}
\]

### Important source limitation

The question does **not provide the four Q-values at the next state \((1,2)\)**.

Therefore a unique numerical Q-value cannot be calculated from the supplied question.

The complete answer supported by the given data is:

\[
\boxed{
Q_{\text{new}}=4.4+0.09
\max_{a'}Q((1,2),a')
}
\]

A numerical answer would require:

\[
\max_{a'}Q((1,2),a')
\]

---

# Q2. Double DQN Update

> In Double DQN, two networks, the primary network and the target network, are used to avoid overestimation. Consider a state where the primary network outputs:
>
> \[
> Q_{\text{up}}=5,\quad
> Q_{\text{down}}=7,\quad
> Q_{\text{left}}=4,\quad
> Q_{\text{right}}=6
> \]
>
> The target network outputs:
>
> \[
> Q_{\text{up}}=5,\quad
> Q_{\text{down}}=6,\quad
> Q_{\text{left}}=4,\quad
> Q_{\text{right}}=7
> \]
>
> Calculate the Q-value update if the agent selects the action "down" in the current state. Assume the discount factor is 0.95 and the reward received is 2.

## Step 1 — Select the next action using the primary network

Primary network:

\[
(5,7,4,6)
\]

The maximum is:

\[
\max(5,7,4,6)=7
\]

Therefore:

\[
\boxed{a^*=\text{down}}
\]

---

## Step 2 — Evaluate that action using the target network

The target network gives:

\[
Q_{\text{target}}(\text{down})=6
\]

Therefore the Double-DQN target is:

\[
y=
r+\gamma Q_{\text{target}}(s',a^*)
\]

\[
y=2+0.95(6)
\]

\[
y=2+5.7
\]

\[
\boxed{y=7.7}
\]

---

## What is the actual updated Q-value?

The question does **not provide**:

- the current \(Q(s,\text{down})\);
- a learning rate \(\alpha\).

Therefore the target can be calculated, but a final updated Q-value cannot.

If the current Q-value is \(Q_{\text{old}}\), then:

\[
\boxed{
Q_{\text{new}}
=
Q_{\text{old}}
+
\alpha(7.7-Q_{\text{old}})
}
\]

### Exam takeaway

Double DQN:

\[
\boxed{\text{Primary selects → Target evaluates}}
\]

Here:

\[
\boxed{y=7.7}
\]

---

# Q3. Actor-Critic Policy Update

> In the Actor-Critic method, an agent gets a reward of +5 for reaching a target and -2 for each step taken. Given that the Critic network provides a value estimate of the current state as 3, and the policy network output for the selected action is 0.6.
>
> Calculate the Actor-Critic gradient update assuming the discount factor is 0.8, and that the agent takes two steps to reach the target.

## Given

\[
R_{\text{goal}}=+5
\]

\[
R_{\text{step}}=-2
\]

\[
V(s)=3
\]

\[
\pi(a|s)=0.6
\]

\[
\gamma=0.8
\]

There are two step penalties before reaching the target.

---

## Step 1 — Calculate the discounted return

Assuming the reward sequence is:

\[
-2,\;-2,\;+5
\]

the return from the initial state is:

\[
G
=
-2
+
0.8(-2)
+
0.8^2(5)
\]

\[
=-2-1.6+3.2
\]

\[
\boxed{G=-0.4}
\]

---

## Step 2 — Calculate the advantage

Using:

\[
A(s,a)=G-V(s)
\]

we get:

\[
A=-0.4-3
\]

\[
\boxed{A=-3.4}
\]

The negative advantage means the selected action performed worse than the Critic expected.

Therefore the Actor should reduce the probability of that action.

---

## Step 3 — Actor gradient

The policy-gradient expression is:

\[
\nabla_\theta J
=
A(s,a)
\nabla_\theta\log\pi_\theta(a|s)
\]

Therefore:

\[
\boxed{
\nabla_\theta J
=
-3.4
\nabla_\theta\log(0.6)
}
\]

The negative sign means the action should be discouraged.

---

## Important limitation

The question gives:

\[
\pi(a|s)=0.6
\]

but does **not** give:

\[
\nabla_\theta\pi_\theta(a|s)
\]

or the actual policy-network parameterization.

Therefore a numerical parameter-gradient vector cannot be calculated.

If one only differentiates with respect to the action probability itself:

\[
\frac{d}{dp}\log p=\frac1p
\]

so:

\[
\frac{dJ}{dp}
=
\frac{-3.4}{0.6}
\]

\[
\boxed{
\frac{dJ}{dp}\approx-5.667
}
\]

But this is **not** the complete neural-network parameter gradient.

### Final exam answer

\[
\boxed{A=-3.4}
\]

and:

\[
\boxed{
\nabla_\theta J
=
-3.4\nabla_\theta\log\pi_\theta(a|s)
}
\]

Thus the selected action is discouraged.

---

# Q4. Prioritized Experience Replay

> In Prioritized Experience Replay, each experience is assigned a priority score based on the TD error. Assume four experiences have TD errors of 0.3, 0.5, 0.2, and 0.8. Calculate the probability of selecting each experience when the priority exponent \(\alpha=0.6\).
>
> Find the normalized probabilities of selection for each experience based on their priority scores.

## Given

\[
\delta=
[0.3,0.5,0.2,0.8]
\]

\[
\alpha=0.6
\]

Priority:

\[
p_i=|\delta_i|^\alpha
\]

Sampling probability:

\[
\boxed{
P(i)=\frac{p_i}{\sum_jp_j}
}
\]

---

## Step 1 — Calculate priorities

### Experience 1

\[
p_1=(0.3)^{0.6}
\]

\[
\boxed{p_1\approx0.4856}
\]

### Experience 2

\[
p_2=(0.5)^{0.6}
\]

\[
\boxed{p_2\approx0.6598}
\]

### Experience 3

\[
p_3=(0.2)^{0.6}
\]

\[
\boxed{p_3\approx0.3807}
\]

### Experience 4

\[
p_4=(0.8)^{0.6}
\]

\[
\boxed{p_4\approx0.8747}
\]

---

## Step 2 — Sum the priorities

\[
\sum p_i
=
0.4856+0.6598+0.3807+0.8747
\]

\[
\boxed{\sum p_i\approx2.4008}
\]

---

## Step 3 — Calculate probabilities

### Experience 1

\[
P_1=
\frac{0.4856}{2.4008}
\]

\[
\boxed{P_1\approx0.2023}
\]

### Experience 2

\[
P_2=
\frac{0.6598}{2.4008}
\]

\[
\boxed{P_2\approx0.2748}
\]

### Experience 3

\[
P_3=
\frac{0.3807}{2.4008}
\]

\[
\boxed{P_3\approx0.1586}
\]

### Experience 4

\[
P_4=
\frac{0.8747}{2.4008}
\]

\[
\boxed{P_4\approx0.3643}
\]

---

## Final answer

| Experience | TD Error | Priority | Probability |
|---|---:|---:|---:|
| 1 | 0.3 | 0.4856 | 0.2023 |
| 2 | 0.5 | 0.6598 | 0.2748 |
| 3 | 0.2 | 0.3807 | 0.1586 |
| 4 | 0.8 | 0.8747 | 0.3643 |

As percentages:

\[
\boxed{
20.23\%,\;27.48\%,\;15.86\%,\;36.43\%
}
\]

The experience with the largest TD error has the highest probability.

---

# Q5. Replay Buffer with Experience Sampling

> A Replay Buffer can hold up to 1000 experiences. After every 10 episodes, the agent adds 50 new experiences. If the buffer starts empty, calculate how many experiences are in the buffer after 200 episodes.
>
> At which episode will the buffer become full, and how many experiences will it hold thereafter?

## Given

Buffer capacity:

\[
C=1000
\]

Experiences added every:

\[
10\text{ episodes}
\]

Experiences added:

\[
50
\]

---

## Step 1 — Number of additions

After 200 episodes:

\[
\frac{200}{10}=20
\]

So there are 20 additions.

---

## Step 2 — Total experiences

\[
20\times50=1000
\]

Therefore:

\[
\boxed{1000}
\]

experiences are present after 200 episodes.

---

## Step 3 — When does the buffer become full?

The buffer needs:

\[
\frac{1000}{50}=20
\]

insertions.

Each insertion occurs every 10 episodes.

Therefore:

\[
20\times10=200
\]

\[
\boxed{\text{Buffer becomes full at episode 200}}
\]

---

## After episode 200

The buffer has a maximum capacity of:

\[
\boxed{1000}
\]

Additional experiences cannot increase its size beyond 1000.

Normally, the oldest experiences are discarded when new experiences are added.

Therefore:

\[
\boxed{
\text{Buffer size remains 1000 thereafter}
}
\]

---

# Q6. Exploration–Exploitation Trade-off in DQN

> In a DQN setup, an agent needs to balance between exploration and exploitation. Explain the importance of the exploration-exploitation tradeoff in DQN. What techniques can be used to maintain this balance, and how do they impact learning?

## Solution

Exploration means trying actions whose quality is uncertain.

Exploitation means choosing the action currently believed to be best:

\[
a^*=\arg\max_aQ(s,a)
\]

---

## Why is the trade-off necessary?

Only exploitation:

\[
\rightarrow
\text{may get stuck in a suboptimal policy}
\]

Only exploration:

\[
\rightarrow
\text{wastes time taking poor actions}
\]

Therefore:

\[
\boxed{
\text{Good RL requires both exploration and exploitation}
}
\]

---

## Epsilon-greedy

With probability:

\[
\epsilon
\]

choose a random action.

With probability:

\[
1-\epsilon
\]

choose the greedy action.

Usually:

\[
\epsilon
\]

is gradually decreased.

Thus:

\[
\boxed{
\text{Early training → exploration}
}
\]

\[
\boxed{
\text{Later training → exploitation}
}
\]

---

## Other techniques

- epsilon decay;
- softmax/Boltzmann exploration;
- optimistic initialization;
- noisy networks;
- exploration bonuses.

### Exam conclusion

> Exploration helps discover better actions, while exploitation uses existing knowledge. Epsilon-greedy with epsilon decay is a common DQN strategy because it encourages exploration early and exploitation later.

---

# Q7. Role of Target Network in DQN

> DQN uses a separate target network to stabilize training. Describe why the target network is necessary. How would learning be affected if both target and primary networks were updated simultaneously?

## Solution

DQN uses:

### Online network

\[
Q(s,a;\theta)
\]

### Target network

\[
Q(s,a;\theta^-)
\]

The target is:

\[
\boxed{
y=
r+\gamma\max_{a'}Q(s',a';\theta^-)
}
\]

The target network is updated less frequently.

---

## Why?

Without a target network:

\[
y=
r+\gamma\max_{a'}Q(s',a';\theta)
\]

The same network would generate both:

- prediction;
- target.

Therefore the target would continuously move as the network changes.

This creates a moving-target problem.

---

## Result without target network

Potential consequences:

- unstable learning;
- oscillating Q-values;
- divergence;
- slower convergence.

### Exam conclusion

> The target network provides a relatively stable target for the online network. Simultaneously updating both networks would make the target change continuously, increasing feedback and instability.

---

# Q8. Double DQN and Q-Value Overestimation

> Explain how Double DQN mitigates Q-value overestimation. What is the conceptual difference between DQN and Double DQN?

## Solution

Standard DQN uses:

\[
y=
r+\gamma\max_{a'}Q(s',a';\theta^-)
\]

The max operation can select an overestimated Q-value.

Double DQN separates action selection and action evaluation.

### Step 1

Online network selects:

\[
\boxed{
a^*=
\arg\max_{a'}Q(s',a';\theta)
}
\]

### Step 2

Target network evaluates:

\[
\boxed{
Q(s',a^*;\theta^-)
}
\]

Therefore:

\[
\boxed{
y=
r+\gamma
Q(s',
\arg\max_{a'}Q(s',a';\theta);
\theta^-)
}
\]

### Memory trick

\[
\boxed{\text{Online picks, Target evaluates}}
\]

This reduces overestimation bias.

---

# Q9. Actor-Critic

> Describe the roles of the Actor and Critic. How does the Critic guide the Actor, and why is separating the functions advantageous?

## Solution

## Actor

The Actor represents:

\[
\pi(a|s)
\]

It chooses actions.

---

## Critic

The Critic estimates:

\[
V(s)
\]

It evaluates how good the current state/action outcome is.

---

## TD error

A common signal is:

\[
\boxed{
\delta=r+\gamma V(s')-V(s)
}
\]

If:

\[
\delta>0
\]

the action performed better than expected.

The Actor increases its probability.

If:

\[
\delta<0
\]

the action performed worse than expected.

The Actor decreases its probability.

---

## Why separate them?

| Actor | Critic |
|---|---|
| Chooses actions | Evaluates behavior |
| Learns policy | Learns value |
| "What should I do?" | "How good was it?" |

Separating these functions allows the Critic to provide a useful learning signal to the Actor.

---

# Q10. Prioritized Experience Replay

> Describe PER and its benefits over uniform sampling. How does prioritizing experiences improve learning, and what drawbacks may arise?

## Solution

Uniform replay gives experiences approximately equal sampling probability.

PER gives greater priority to experiences with large TD errors.

A common formulation is:

\[
p_i=|\delta_i|^\alpha
\]

and:

\[
P(i)=
\frac{p_i}{\sum_jp_j}
\]

---

## Why does this help?

Large TD error means:

\[
\text{current prediction differs significantly from target}
\]

Therefore the experience may contain more useful information.

PER causes such experiences to be replayed more frequently.

---

## Advantages

- improved sample efficiency;
- faster learning;
- important/rare experiences receive more attention.

## Disadvantages

- non-uniform sampling introduces bias;
- additional computational complexity;
- very high-priority experiences can dominate;
- importance-sampling correction may be required.

---

# Q11. Replay Buffer

> Discuss why the Replay Buffer is essential in DQN and how it differs from training without one. What happens if it is too small or too large?

## Solution

A replay buffer stores:

\[
\boxed{
(s,a,r,s',done)
}
\]

The agent later samples random mini-batches.

---

## Why use it?

### 1. Breaks correlation

Consecutive transitions are highly correlated.

Random replay produces more independent training samples.

### 2. Reuses experience

The same transition can be used multiple times.

### 3. Improves sample efficiency

The agent extracts more learning from environment interactions.

---

## Too small

A small buffer:

- has low diversity;
- quickly replaces old experiences;
- may produce correlated batches.

\[
\boxed{\text{Too small → poor diversity}}
\]

---

## Too large

A very large buffer:

- requires more memory;
- may contain stale experiences;
- can make learning less responsive to recent changes.

\[
\boxed{\text{Too large → memory + stale-data problems}}
\]

---

# Q12. DyNa-Q Framework

> Explain how DyNa-Q uses simulated experiences to improve learning efficiency. What are the benefits of planning steps, and how does it differ from pure model-free learning?

## Solution

DyNa-Q combines:

\[
\boxed{
\text{Model-based planning + Model-free learning}
}
\]

The agent learns a model of the environment:

\[
(s,a)\rightarrow(\hat r,\hat s')
\]

It can then use the model to generate simulated experiences.

---

## Process

```text
Real interaction
      |
      ▼
Real experience
      |
      ▼
Learn environment model
      |
      ▼
Simulate transitions
      |
      ▼
Extra Q-learning updates
```

---

## Advantage

The agent can perform additional learning without obtaining every transition from the real environment.

Therefore:

\[
\boxed{
\text{Better sample efficiency}
}
\]

---

## Difference from model-free RL

Model-free:

\[
\boxed{\text{learn directly from real experience}}
\]

DyNa-Q:

\[
\boxed{
\text{real experience + model-generated experience}
}
\]

---

## Limitation

If the learned model is inaccurate:

\[
\text{model error}
\rightarrow
\text{incorrect simulated experience}
\rightarrow
\text{incorrect learning}
\]

---

# Q13. Dueling Q-Network

> Explain the motivation behind the Dueling Q-Network architecture. How does separating state and action values help learning?

## Solution

Dueling DQN separates:

\[
Q(s,a)
\]

into:

\[
V(s)
\]

and:

\[
A(s,a)
\]

where:

- \(V(s)\) = value of the state;
- \(A(s,a)\) = advantage of an action.

A common combination is:

\[
\boxed{
Q(s,a)
=
V(s)
+
A(s,a)
-
\frac{1}{|\mathcal A|}
\sum_{a'}A(s,a')
}
\]

---

## Why?

Some states are important regardless of the exact action.

For example, if a drone is far from all obstacles, several actions may have almost the same effect.

The network can learn:

\[
V(s)
\]

without needing large action-specific differences.

---

## Architecture

```text
State
  |
  ▼
Shared layers
  |
  +--------+
  |        |
  ▼        ▼
 V(s)     A(s,a)
  |        |
  +----+---+
       |
       ▼
     Q(s,a)
```

### Exam takeaway

> Dueling DQN separately learns how valuable a state is and how advantageous each action is. This is especially useful when many actions have similar effects in a state.

---

# Q14. Asynchronous Advantage Actor-Critic

> Explain how asynchronous updates in A3C help address convergence issues and lead to faster learning. What are the advantages and challenges compared with synchronized learning?

## Solution

A3C uses multiple workers.

Each worker:

1. interacts with an environment;
2. collects experience;
3. computes gradients;
4. updates shared global parameters.

```text
             Global Network
             /      |      \
            ▼       ▼       ▼
         Worker 1 Worker 2 Worker 3
            |       |       |
            ▼       ▼       ▼
        Environment Environment Environment
```

---

## Why does this help?

Different workers generate different trajectories.

Therefore:

\[
\boxed{\text{experience becomes less correlated}}
\]

They also collect experience simultaneously:

\[
\boxed{\text{more experience per unit time}}
\]

---

## Advantages

- parallel experience collection;
- more diverse trajectories;
- reduced correlation;
- potentially faster training;
- can reduce dependence on replay buffers.

---

## Challenges

- stale parameters/gradients;
- concurrent update conflicts;
- greater implementation complexity;
- higher computational requirements.

---

# Q15. Direct Utility Estimation

> Explain how Direct Utility Estimation works in Passive Learning. Why might it be inefficient in large state spaces or with limited observed data?

## Solution

The agent follows a fixed policy.

For every visited state, it records the observed return:

\[
G_1,G_2,\ldots,G_n
\]

and estimates:

\[
\boxed{
V(s)=
\frac{1}{n}
\sum_{i=1}^{n}G_i
}
\]

---

## Example

Suppose the returns after visiting state \(s\) are:

\[
5,\;7,\;3
\]

Then:

\[
V(s)=
\frac{5+7+3}{3}
\]

\[
\boxed{V(s)=5}
\]

---

## Why inefficient?

In a large state space, many states may be visited rarely.

With limited observations:

\[
\boxed{
\text{few samples}
\Rightarrow
\text{unreliable value estimates}
}
\]

It also generally requires complete episode returns.

---

# Q16. Temporal Difference Learning

> Describe TD learning. How does TD update a state differently from Direct Utility Estimation and Monte Carlo?

## Solution

TD uses:

\[
\boxed{
V(s)
\leftarrow
V(s)+
\alpha[
r+\gamma V(s')-V(s)
]
}
\]

The TD error is:

\[
\boxed{
\delta=
r+\gamma V(s')-V(s)
}
\]

---

## Key idea

TD does not wait for the entire episode.

It uses:

\[
r+\gamma V(s')
\]

as the target.

This is called:

\[
\boxed{\text{bootstrapping}}
\]

---

## Comparison

| Method | Target |
|---|---|
| Direct Utility | Average observed returns |
| Monte Carlo | Complete actual return |
| TD | Immediate reward + estimated next value |

Therefore:

\[
\boxed{\text{TD can learn after each transition}}
\]

---

# Q17. Monte Carlo Methods

> Explain the advantages and disadvantages of Monte Carlo methods in Passive Learning. Why might they be impractical in continuous or highly variable environments?

## Solution

Monte Carlo estimates value using complete returns:

\[
\boxed{
G_t=
R_{t+1}
+\gamma R_{t+2}
+\gamma^2R_{t+3}
+\cdots
}
\]

The state value is estimated from observed returns.

---

## Advantages

- model-free;
- simple;
- uses actual observed returns;
- does not bootstrap.

---

## Disadvantages

### Must wait for episode completion

\[
\boxed{\text{Delayed learning}}
\]

### High variance

Different episodes may produce very different returns.

### Poor for continuing tasks

If an environment has no natural terminal state, complete returns may not be available.

### Long episodes

Long trajectories cause further delays.

Therefore:

\[
\boxed{
\text{continuous/long environment}
\Rightarrow
\text{MC becomes inconvenient}
}
\]

---

# Q18. Compare Direct Utility, TD and Monte Carlo

> Compare Direct Utility Estimation, TD Learning and Monte Carlo Methods. In what environments might each perform best?

## Solution

| Feature | Direct Utility | Monte Carlo | TD |
|---|---|---|---|
| Model-free | Yes | Yes | Yes |
| Complete return | Yes | Yes | No |
| Bootstrapping | No | No | Yes |
| Wait for episode | Yes | Yes | No |
| Online updates | No | No | Yes |
| Continuing tasks | Poor | Poor | Good |
| Simple | Yes | Yes | Yes |

---

## Best use

### Direct Utility

Useful for:

- small state spaces;
- episodic environments;
- abundant observations.

### Monte Carlo

Useful for:

- episodic environments;
- complete episodes;
- situations where actual returns are preferred.

### TD

Useful for:

- online learning;
- long episodes;
- continuing environments;
- incremental updates.

---

# Q19. Exploration–Exploitation in Q-Learning

> Describe the significance of exploration-exploitation in Q-Learning. What methods can balance it?

## Solution

### Exploration

Try uncertain actions.

### Exploitation

Choose:

\[
\boxed{
\arg\max_aQ(s,a)
}
\]

---

## Epsilon-greedy

With probability:

\[
\epsilon
\]

explore.

With probability:

\[
1-\epsilon
\]

exploit.

Usually:

\[
\epsilon\downarrow
\]

as learning progresses.

---

## Other methods

- epsilon decay;
- softmax/Boltzmann exploration;
- optimistic initialization;
- exploration bonuses;
- noisy networks.

---

## Effect

Too much exploration:

\[
\rightarrow
\text{slow exploitation}
\]

Too much exploitation:

\[
\rightarrow
\text{may miss better actions}
\]

---

# Q20. SARSA vs Q-Learning

> Explain the main difference between SARSA and Q-Learning in terms of policy updates. How does SARSA's on-policy learning impact the policies learned?

## Solution

### Q-Learning

Q-Learning is:

\[
\boxed{\text{off-policy}}
\]

Update:

\[
\boxed{
Q(s,a)
\leftarrow
Q(s,a)+
\alpha[
r+\gamma\max_{a'}Q(s',a')
-Q(s,a)]
}
\]

It uses the best possible next action.

---

### SARSA

SARSA is:

\[
\boxed{\text{on-policy}}
\]

Update:

\[
\boxed{
Q(s,a)
\leftarrow
Q(s,a)+
\alpha[
r+\gamma Q(s',a')
-Q(s,a)]
}
\]

where \(a'\) is the actual action selected by the current policy.

---

## Example

Suppose:

\[
Q(s',a_1)=10
\]

\[
Q(s',a_2)=7
\]

but the exploratory policy actually chooses:

\[
a_2
\]

Q-Learning uses:

\[
10
\]

SARSA uses:

\[
7
\]

Therefore SARSA accounts for the actual exploratory behavior.

---

## Consequence

SARSA can learn more conservative policies in risky environments.

Q-Learning targets the optimal greedy behavior independently of the exploratory behavior policy.

---

# Q21. Q-Learning vs SARSA — Advantages and Disadvantages

> Discuss the advantages and disadvantages of Q-Learning versus SARSA. In what scenarios would SARSA be preferred over Q-Learning, and vice versa?

## Q-Learning

### Advantages

- off-policy;
- directly targets the greedy optimal policy;
- exploration policy can be separate from target policy;
- simple update.

### Disadvantages

- can learn aggressive policies;
- does not account for exploratory actions in its target;
- max operator can contribute to overestimation.

---

## SARSA

### Advantages

- on-policy;
- accounts for actual behavior;
- can produce safer policies;
- useful when exploration has real consequences.

### Disadvantages

- depends on the behavior policy;
- may learn a more conservative policy;
- may not directly target the purely greedy optimum.

---

## When to use SARSA

Prefer SARSA when:

- safety matters;
- exploration is risky;
- actual behavior is important;
- the environment has dangerous states.

Example:

\[
\boxed{\text{robot navigation near hazards}}
\]

---

## When to use Q-Learning

Prefer Q-Learning when:

- the goal is the optimal greedy policy;
- exploratory behavior can be separated from the target;
- exploration has relatively low cost.

---

# Final Formula Sheet

## DQN

\[
\boxed{
Q_{\text{new}}
=
Q+
\alpha[
r+\gamma\max Q'-Q]
}
\]

## Double DQN

\[
\boxed{
a^*=\arg\max Q_{\text{online}}(s',a')
}
\]

\[
\boxed{
y=r+\gamma Q_{\text{target}}(s',a^*)
}
\]

## Actor-Critic

\[
\boxed{
\delta=r+\gamma V(s')-V(s)
}
\]

\[
\boxed{
\nabla_\theta J
=
\delta\nabla_\theta\log\pi_\theta(a|s)
}
\]

## PER

\[
\boxed{
p_i=|\delta_i|^\alpha
}
\]

\[
\boxed{
P(i)=\frac{p_i}{\sum_jp_j}
}
\]

## TD

\[
\boxed{
V(s)\leftarrow
V(s)+
\alpha[r+\gamma V(s')-V(s)]
}
\]

## Q-Learning

\[
\boxed{
Q(s,a)\leftarrow
Q(s,a)+
\alpha[
r+\gamma\max_{a'}Q(s',a')-Q(s,a)]
}
\]

## SARSA

\[
\boxed{
Q(s,a)\leftarrow
Q(s,a)+
\alpha[
r+\gamma Q(s',a')-Q(s,a)]
}
\]

## Dueling DQN

\[
\boxed{
Q(s,a)=
V(s)+A(s,a)-\operatorname{mean}_{a'}A(s,a')
}
\]
