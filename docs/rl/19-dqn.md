# Deep Reinforcement Learning — DQN

## Source PDFs

- [Deep RL Tutorial](pdfs/Deep-RL-Tutorial%20%281%29.pdf)
- [RL Question Bank](pdfs/QUESTIONS%20_rl%20%282%29.pdf)
- [L6 — Reinforcement Learning](pdfs/L6%20%283%29.pdf)

---

# 1. Why Deep Reinforcement Learning?

Tabular Q-learning stores a separate value for every state-action pair:

\[
Q(s,a)
\]

This works when the state space is small.

For large state spaces, a Q-table becomes impractical.

For example, if a state contains:

- image pixels;
- position;
- velocity;
- environment information;

the number of possible states can become enormous.

Deep RL solves this by using a neural network to approximate the Q-function.

\[
\boxed{
Q(s,a;\theta)
}
\]

where:

- \(s\) = state
- \(a\) = action
- \(\theta\) = neural-network parameters

---

# 2. Deep Q-Network

A **Deep Q-Network (DQN)** is a neural network that approximates the action-value function.

Instead of storing:

\[
Q(s,a)
\]

in a table, the network receives a state and outputs Q-values for all possible actions.

For example:

```text
             State s
                │
                ▼
        ┌───────────────┐
        │ Neural Network│
        └───────────────┘
                │
       ┌────────┼────────┐
       ▼        ▼        ▼
     Q(up)   Q(down)   Q(left) ...
```

If the output is:

\[
[2.1,\;5.7,\;1.3,\;4.2]
\]

then:

\[
a^*=\arg\max_aQ(s,a)
\]

gives:

\[
\boxed{a^*=\text{down}}
\]

---

# 3. DQN is Based on Q-Learning

Recall the Q-learning target:

\[
Q(s,a)
\leftarrow
r+\gamma\max_{a'}Q(s',a')
\]

DQN uses a neural network to approximate this Q-function.

The target is:

\[
\boxed{
y=r+\gamma\max_{a'}Q(s',a';\theta^-)
}
\]

where:

\[
\theta^-
\]

represents the parameters of the target network.

The online network with parameters:

\[
\theta
\]

is trained to approximate this target.

---

# 4. DQN Loss Function

The network produces:

\[
Q(s,a;\theta)
\]

The target is:

\[
y=
r+\gamma\max_{a'}Q(s',a';\theta^-)
\]

The loss can be written as:

\[
\boxed{
L(\theta)
=
\left[
y-Q(s,a;\theta)
\right]^2
}
\]

In practice, variants such as Huber loss are also commonly used.

For exam purposes, remember:

\[
\boxed{
\text{Loss}
=
(\text{target}-\text{predicted Q})^2
}
\]

---

# 5. Main Components of DQN

The important components are:

1. Online Q-network
2. Target network
3. Replay buffer
4. Epsilon-greedy exploration
5. Bellman target

---

## 5.1 Online Network

The online network contains the parameters:

\[
\theta
\]

It is the network that is actively trained.

It estimates:

\[
Q(s,a;\theta)
\]

---

## 5.2 Target Network

The target network contains:

\[
\theta^-
\]

It is used to calculate the target:

\[
y=r+\gamma\max_{a'}Q(s',a';\theta^-)
\]

The target network is updated periodically from the online network.

For example:

```text
Online network
      │
      │ periodically copy parameters
      ▼
Target network
```

---

# 6. Why Does DQN Need a Target Network?

Without a target network, the same network would be used to calculate both:

### Prediction

\[
Q(s,a;\theta)
\]

and:

### Target

\[
r+\gamma\max_{a'}Q(s',a';\theta)
\]

Therefore, the target itself would continuously move as the network is updated.

This creates an unstable learning target.

The target network keeps:

\[
\theta^-
\]

fixed for a number of updates.

This makes the target change more slowly.

### Exam answer

> The target network stabilizes DQN training by providing a relatively fixed target while the online network is updated. Without it, both prediction and target would change simultaneously, causing oscillations or instability.

The supplied question bank directly asks this in Q7. QUESTIONS \_rl (2)

---

# 7. Target Network Update

A common strategy is a hard update:

\[
\boxed{
\theta^-\leftarrow\theta
}
\]

every \(C\) training steps.

For example:

```text
Train online network
Train online network
Train online network
...
After C steps
       ↓
θ⁻ ← θ
```

Another approach is a soft update:

\[
\theta^-
\leftarrow
\tau\theta+(1-\tau)\theta^-
\]

where:

\[
0<\tau<1
\]

---

# 8. Replay Buffer

DQN stores previous experiences in a replay buffer.

An experience is:

\[
\boxed{
(s,a,r,s',done)
}
\]

The buffer contains many such transitions.

Example:

```text
Experience 1: (s1,a1,r1,s2)
Experience 2: (s2,a2,r2,s3)
Experience 3: (s3,a3,r3,s4)
...
```

During training, a random mini-batch is sampled.

---

# 9. Why Replay Buffer Is Needed

Consecutive experiences are strongly correlated.

For example:

\[
s_1\rightarrow s_2\rightarrow s_3\rightarrow s_4
\]

Training directly on these sequential samples can cause poor learning.

Replay breaks this correlation by randomly sampling old experiences.

```text
Environment
     ↓
Experience
     ↓
Replay Buffer
     ↓
Random mini-batch
     ↓
Neural Network
```

---

# 10. Benefits of Replay Buffer

### 1. Breaks correlation

Random sampling makes training data less sequentially correlated.

### 2. Reuses experience

One experience can be used multiple times.

### 3. Improves sample efficiency

The agent does not need to discard an experience after using it once.

### 4. Stabilizes learning

Random mini-batches make neural-network training more suitable.

---

# 11. Replay Buffer Too Small

If the buffer is too small:

- experiences are quickly overwritten;
- samples may remain highly correlated;
- diversity decreases;
- the agent may forget older experiences.

Therefore:

\[
\boxed{
\text{Too small}
\Rightarrow
\text{low diversity + instability}
}
\]

---

# 12. Replay Buffer Too Large

A very large buffer has a different problem.

Old experiences may remain for a long time.

If the environment or policy changes significantly, these old experiences may become less relevant.

Therefore:

\[
\boxed{
\text{Too large}
\Rightarrow
\text{stale experiences + higher memory usage}
}
\]

The supplied question bank explicitly asks about both extremes in Q11. QUESTIONS \_rl (2)

---

# 13. Exploration in DQN

DQN commonly uses:

\[
\epsilon\text{-greedy}
\]

With probability:

\[
1-\epsilon
\]

choose:

\[
\arg\max_aQ(s,a)
\]

With probability:

\[
\epsilon
\]

choose a random action.

Thus:

```text
             Action
                │
        ┌───────┴───────┐
        │               │
     1 - ε               ε
        │               │
        ▼               ▼
     Greedy           Random
```

Usually:

\[
\epsilon
\]

is gradually reduced during training.

---

# 14. Complete DQN Training Cycle

The complete process is:

```text
             Environment
                  │
                  ▼
               State s
                  │
                  ▼
           ε-greedy action
                  │
                  ▼
          Environment step
                  │
          ┌───────┴───────┐
          ▼               ▼
       Reward r         State s'
          │               │
          └───────┬───────┘
                  ▼
             Replay Buffer
                  │
                  ▼
            Random batch
                  │
          ┌───────┴────────┐
          ▼                ▼
   Online Q-network   Target network
          │                │
          │                ▼
          │          Bellman target
          │                │
          └───────┬────────┘
                  ▼
                Loss
                  │
                  ▼
          Update θ
                  │
                  ▼
       Periodically update θ⁻
```

---

# 15. DQN Algorithm

```text
Initialize online network Q(s,a;θ)

Initialize target network Q(s,a;θ⁻)

Initialize replay buffer D

For each episode:

    Initialize state s

    Repeat:

        Choose action a using ε-greedy

        Execute a

        Observe r and s'

        Store:
            (s,a,r,s',done)

        in D

        Sample random mini-batch from D

        For each transition:

            y =
            r + γ max Q(s',a';θ⁻)

        Update θ by minimizing:

            (y - Q(s,a;θ))²

        Periodically:

            θ⁻ ← θ

        s ← s'

    Until terminal
```

---

# 16. DQN Advantages

### 1. Handles large state spaces

Neural networks replace an enormous Q-table.

### 2. Can process high-dimensional inputs

For example, images can be used as states.

### 3. Experience replay

Allows experience reuse.

### 4. Target network

Improves training stability.

---

# 17. DQN Limitations

Important exam points:

- high computational cost;
- requires large amounts of experience;
- training can be unstable;
- sensitive to hyperparameters;
- Q-value overestimation can occur;
- standard DQN is mainly designed for discrete action spaces.

The overestimation problem motivates:

\[
\boxed{\text{Double DQN}}
\]

---

# 18. Double DQN

Standard DQN uses:

\[
\max_{a'}Q(s',a';\theta^-)
\]

The same target network effectively performs both:

1. action selection;
2. action evaluation.

Because neural-network estimates contain noise, the maximum tends to select overestimated values.

This produces:

\[
\boxed{\text{Q-value overestimation bias}}
\]

---

# 19. Double DQN Idea

Double DQN separates:

### Action selection

Use the online network:

\[
\boxed{
a^*=
\arg\max_{a'}Q(s',a';\theta)
}
\]

### Action evaluation

Use the target network:

\[
\boxed{
Q(s',a^*;\theta^-)
}
\]

Therefore:

\[
\boxed{
y=
r+
\gamma
Q
\left(
s',
\arg\max_{a'}Q(s',a';\theta);
\theta^-
\right)
}
\]

The supplied tutorial emphasizes exactly this separation: the online network selects the action while the target network evaluates it. Deep-RL-Tutorial (1)

---

# 20. DQN vs Double DQN

| Feature | DQN | Double DQN |
|---|---|---|
| Action selection | Target network | Online network |
| Action evaluation | Target network | Target network |
| Max operation | Direct max target Q | Argmax online, evaluate target |
| Overestimation | Higher | Reduced |
| Main purpose | Stable Q learning | Reduce overestimation |

### Memory trick

> **DQN:** target chooses and evaluates.

> **Double DQN:** online chooses, target evaluates.

---

# 21. Numerical Example from the Tutorial

Suppose:

\[
r=1
\]

\[
\gamma=0.9
\]

Online network:

\[
Q_\theta(a_1)=3
\]

\[
Q_\theta(a_2)=2
\]

Target network:

\[
Q_{\theta^-}(a_1)=1
\]

\[
Q_{\theta^-}(a_2)=2.5
\]

### Vanilla DQN

Take the maximum target-network value:

\[
\max(1,2.5)=2.5
\]

Therefore:

\[
y=1+0.9(2.5)
\]

\[
\boxed{y=3.25}
\]

### Double DQN

First select using the online network:

\[
a^*=\arg\max(3,2)=a_1
\]

Then evaluate \(a_1\) using the target network:

\[
Q_{\theta^-}(a_1)=1
\]

Therefore:

\[
y=1+0.9(1)
\]

\[
\boxed{y=1.9}
\]

Thus:

\[
3.25\rightarrow1.9
\]

The target becomes less inflated.

This exact numerical illustration is given in the supplied Deep RL tutorial. Deep-RL-Tutorial (1)

---

# 22. Dueling DQN

Dueling DQN changes the architecture of DQN.

Instead of directly estimating Q-values, it separates:

1. State value
2. Action advantage

The decomposition is:

\[
\boxed{
Q(s,a)
=
V(s)
+
\left(
A(s,a)-\frac{1}{|A|}\sum_{a'}A(s,a')
\right)
}
\]

where:

\[
V(s)
\]

represents:

> How good is it to be in state \(s\)?

and:

\[
A(s,a)
\]

represents:

> How much better or worse is action \(a\) compared with the other actions?

The supplied tutorial gives this exact formulation. Deep-RL-Tutorial (1)

---

# 23. Why Dueling DQN?

Consider a state where almost all actions have similar consequences.

A normal DQN has to estimate a Q-value separately for every action.

Dueling DQN first learns:

\[
V(s)
\]

which captures the overall quality of the state.

It then learns:

\[
A(s,a)
\]

to distinguish between actions.

This can make learning more efficient, particularly when the choice of action has little effect in many states.

---

# 24. Dueling DQN Architecture

```text
              State
                │
                ▼
          Shared Network
                │
         ┌──────┴──────┐
         ▼             ▼
     Value Stream   Advantage Stream
         │             │
       V(s)         A(s,a)
         │             │
         └──────┬──────┘
                ▼
          Combine streams
                │
                ▼
              Q(s,a)
```

---

# 25. Dueling DQN Numerical Example

Given:

\[
V(s)=5
\]

and:

\[
A=[3,1,2]
\]

First calculate the mean advantage:

\[
\bar A=
\frac{3+1+2}{3}
\]

\[
\bar A=2
\]

Now:

\[
Q(s,a)=V(s)+(A(s,a)-\bar A)
\]

### Action 1

\[
Q(a_1)=5+(3-2)
\]

\[
\boxed{Q(a_1)=6}
\]

### Action 2

\[
Q(a_2)=5+(1-2)
\]

\[
\boxed{Q(a_2)=4}
\]

### Action 3

\[
Q(a_3)=5+(2-2)
\]

\[
\boxed{Q(a_3)=5}
\]

Therefore:

\[
\boxed{a_1\text{ is the best action}}
\]

This numerical example is directly provided in the supplied tutorial. Deep-RL-Tutorial (1)

---

# 26. DQN Variants in This Syllabus

The important DQN-related methods are:

### Vanilla DQN

Basic deep Q-learning.

### Double DQN

Reduces Q-value overestimation.

### Dueling DQN

Separates:

\[
V(s)
\]

and:

\[
A(s,a)
\]

### Prioritized Experience Replay

Samples important experiences more frequently.

These methods can also be combined.

For example:

\[
\boxed{\text{Dueling Double DQN + PER}}
\]

---

# 27. Q1. Q-Learning with DQN

> **Question:** A robot uses a Deep Q-Network (DQN) for navigating a grid. The network has four actions: up, down, left, and right, each giving a reward of +10 if it reaches the goal state or -1 otherwise. The robot starts from the top-left cell (0,0) and the goal is located at the bottom-right cell (4,4).
>
> **Problem:** If the discount factor is 0.9 and learning rate is 0.1, calculate the Q-value update for taking an action that moves from (1,1) to (1,2) with the current Q-value at 5. Show the Q-value update calculation using the Bellman equation.

## Solution

The DQN/Q-learning update is:

\[
Q_{\text{new}}
=
Q_{\text{old}}
+
\alpha
[
r+\gamma\max_{a'}Q(s',a')
-Q_{\text{old}}
]
\]

Given:

\[
Q_{\text{old}}=5
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

Since this is not the goal:

\[
r=-1
\]

However, the question does **not provide the Q-values of the four possible actions from \((1,2)\)**.

Therefore:

\[
\max_{a'}Q((1,2),a')
\]

is unknown.

Let:

\[
M=\max_{a'}Q((1,2),a')
\]

Then:

\[
Q_{\text{new}}
=
5+
0.1[-1+0.9M-5]
\]

Simplify:

\[
Q_{\text{new}}
=
5+
0.1(0.9M-6)
\]

\[
\boxed{
Q_{\text{new}}
=
4.4+0.09M
}
\]

### Important

A numerical final Q-value **cannot be calculated from the supplied question** because \(M\) is missing.

Do not invent a value for it in the exam.

The correct response is to substitute the known quantities and leave the missing maximum Q-value symbolic.

---

# 28. Q2. Double DQN Update

> **Question:** In Double DQN, two networks, the primary network, and the target network are used to avoid overestimation. Consider a state where the primary network outputs the Q-values:
>
> \[
> Q_{up}=5,\quad Q_{down}=7,\quad Q_{left}=4,\quad Q_{right}=6
> \]
>
> The target network outputs:
>
> \[
> Q_{up}=5,\quad Q_{down}=6,\quad Q_{left}=4,\quad Q_{right}=7
> \]
>
> **Problem:** Calculate the Q-value update if the agent selects the action “down” in the current state. Assume the discount factor is 0.95 and the reward received is 2.

## Solution

Double DQN separates action selection from action evaluation.

### Step 1 — Select action using primary/online network

Primary network:

\[
[5,7,4,6]
\]

The maximum is:

\[
7
\]

corresponding to:

\[
\boxed{a^*=\text{down}}
\]

This agrees with the action specified in the question.

---

### Step 2 — Evaluate selected action using target network

Target network gives:

\[
Q_{\text{target}}(\text{down})=6
\]

Therefore:

\[
Q_{\text{target}}(s',a^*)=6
\]

---

### Step 3 — Calculate the Double DQN target

\[
y=r+\gamma Q_{\text{target}}(s',a^*)
\]

Substitute:

\[
y=2+0.95(6)
\]

\[
y=2+5.7
\]

\[
\boxed{y=7.7}
\]

### Important qualification

The question says "calculate the Q-value update", but it does **not provide the current Q-value \(Q(s,a)\) for the current state/action** or a learning rate.

Therefore, the actual updated Q-value cannot be calculated.

What can be calculated is the **Double DQN target**:

\[
\boxed{y=7.7}
\]

If a current Q-value \(Q_{\text{old}}\) and learning rate \(\alpha\) were supplied, the update would be:

\[
Q_{\text{new}}
=
Q_{\text{old}}
+
\alpha(7.7-Q_{\text{old}})
\]

---

# 29. Q3. Actor-Critic Policy Update

> **Question:** In the Actor-Critic method, an agent gets a reward of +5 for reaching a target and -2 for each step taken. Given that the Critic network provides a value estimate of the current state as 3, and the policy network output for the selected action is 0.6.
>
> **Problem:** Calculate the Actor-Critic gradient update assuming the discount factor is 0.8, and that the agent takes two steps to reach the target.

## Solution

This question requires care because it does not provide enough information for a complete numerical gradient.

The Actor-Critic method uses the TD/advantage signal to determine whether the selected action was better or worse than expected.

A common policy-gradient form is:

\[
\boxed{
\nabla J
\propto
\delta\nabla\log\pi(a|s)
}
\]

where:

\[
\delta
=
r+\gamma V(s')-V(s)
\]

The supplied tutorial describes the TD error as the shared learning signal between Actor and Critic. Deep-RL-Tutorial (1)

---

## Step 1 — Calculate the return

The agent takes two steps.

The reward structure says:

- \(-2\) for each step;
- \(+5\) for reaching the target.

Interpreting this as:

\[
r_1=-2
\]

and:

\[
r_2=+5
\]

the discounted return from the starting point is:

\[
G=-2+0.8(5)
\]

\[
G=-2+4
\]

\[
\boxed{G=2}
\]

---

## Step 2 — Compare with Critic's estimate

The Critic estimates:

\[
V(s)=3
\]

Therefore, using the return as the learning target:

\[
A=G-V(s)
\]

\[
A=2-3
\]

\[
\boxed{A=-1}
\]

The negative advantage means:

> The observed outcome was worse than what the Critic expected.

Therefore, the Actor should reduce the probability of selecting this action.

---

## Step 3 — Actor update

The policy probability is:

\[
\pi(a|s)=0.6
\]

The policy-gradient term is proportional to:

\[
A\nabla\log\pi(a|s)
\]

Thus:

\[
\boxed{
\nabla J
\propto
-1\cdot\nabla\log(0.6)
}
\]

### Why no exact gradient?

The question gives the probability \(0.6\), but does not provide:

- the policy-network parameters;
- \(\nabla_\theta\log\pi(a|s)\);
- learning rate.

Therefore, an actual numerical parameter update cannot be calculated.

The important exam conclusion is:

\[
\boxed{A<0\Rightarrow\text{decrease probability of the selected action}}
\]

---

# 30. Q4. Prioritized Experience Replay

> **Question:** In Prioritized Experience Replay, each experience is assigned a priority score based on the TD error. Assume four experiences have TD errors of 0.3, 0.5, 0.2, 0.8. Calculate the probability of selecting each experience when the priority exponent \(\alpha=0.6\).**
>
> **Problem:** Find the normalized probabilities of selection for each experience based on their priority scores.

## Solution

In PER, the priority is proportional to:

\[
p_i=|\delta_i|^\alpha
\]

Given:

\[
\alpha=0.6
\]

and TD errors:

\[
0.3,\;0.5,\;0.2,\;0.8
\]

---

## Step 1 — Calculate priorities

### Experience 1

\[
p_1=(0.3)^{0.6}
\]

\[
p_1\approx0.486
\]

### Experience 2

\[
p_2=(0.5)^{0.6}
\]

\[
p_2\approx0.660
\]

### Experience 3

\[
p_3=(0.2)^{0.6}
\]

\[
p_3\approx0.381
\]

### Experience 4

\[
p_4=(0.8)^{0.6}
\]

\[
p_4\approx0.875
\]

Therefore:

| Experience | TD error | Priority |
|---|---:|---:|
| 1 | 0.3 | 0.486 |
| 2 | 0.5 | 0.660 |
| 3 | 0.2 | 0.381 |
| 4 | 0.8 | 0.875 |

---

## Step 2 — Normalize

The sum is approximately:

\[
0.486+0.660+0.381+0.875
\]

\[
\approx2.402
\]

Therefore:

\[
P(i)=\frac{p_i}{\sum_jp_j}
\]

### Experience 1

\[
P(1)\approx\frac{0.486}{2.402}
\]

\[
\boxed{P(1)\approx0.202}
\]

### Experience 2

\[
P(2)\approx\frac{0.660}{2.402}
\]

\[
\boxed{P(2)\approx0.275}
\]

### Experience 3

\[
P(3)\approx\frac{0.381}{2.402}
\]

\[
\boxed{P(3)\approx0.159}
\]

### Experience 4

\[
P(4)\approx\frac{0.875}{2.402}
\]

\[
\boxed{P(4)\approx0.364}
\]

---

## Final Answer

| Experience | TD Error | Selection Probability |
|---|---:|---:|
| 1 | 0.3 | **0.202 ≈ 20.2%** |
| 2 | 0.5 | **0.275 ≈ 27.5%** |
| 3 | 0.2 | **0.159 ≈ 15.9%** |
| 4 | 0.8 | **0.364 ≈ 36.4%** |

Check:

\[
0.202+0.275+0.159+0.364
\approx1
\]

The experience with the largest TD error:

\[
0.8
\]

has the highest probability of being replayed.

### Exam shortcut

Remember:

\[
\boxed{
P(i)=
\frac{|\delta_i|^\alpha}
{\sum_j|\delta_j|^\alpha}
}
\]

---

# 31. Q5. Replay Buffer with Experience Sampling

> **Question:** A Replay Buffer can hold up to 1000 experiences. After every 10 episodes, the agent adds 50 new experiences. If the buffer starts empty, calculate how many experiences are in the buffer after 200 episodes.
>
> **Problem:** At which episode will the buffer become full, and how many experiences will it hold thereafter?

## Solution

The buffer receives:

\[
50
\]

experiences every:

\[
10
\]

episodes.

Therefore, the number of additions by episode \(200\) is:

\[
\frac{200}{10}=20
\]

Each addition contains 50 experiences:

\[
20\times50=1000
\]

Therefore:

\[
\boxed{1000\text{ experiences}}
\]

are present after 200 episodes.

---

## When does the buffer become full?

After:

\[
20
\]

batches:

\[
20\times50=1000
\]

The 20th batch is added after episode:

\[
20\times10
\]

\[
\boxed{200}
\]

Therefore, the buffer becomes full at:

\[
\boxed{\text{Episode 200}}
\]

---

## What happens after episode 200?

The buffer capacity is:

\[
1000
\]

Therefore it cannot exceed:

\[
\boxed{1000}
\]

New experiences replace old experiences once the buffer is full.

For example:

```text
Before full:
[old experiences ............]

At episode 200:
[1000 experiences]

After episode 210:
[oldest experiences removed]
[new experiences inserted]
```

The number of experiences remains:

\[
\boxed{1000}
\]

---

# 32. Unit 5 — DQN Formula Sheet

## DQN target

\[
\boxed{
y=
r+\gamma\max_{a'}Q(s',a';\theta^-)
}
\]

## DQN loss

\[
\boxed{
L=
(y-Q(s,a;\theta))^2
}
\]

## Q-learning update

\[
\boxed{
Q_{\text{new}}
=
Q_{\text{old}}
+
\alpha
[
y-Q_{\text{old}}
]
}
\]

## Double DQN target

\[
\boxed{
y=
r+\gamma
Q
\left(
s',
\arg\max_{a'}Q(s',a';\theta);
\theta^-
\right)
}
\]

## PER probability

\[
\boxed{
P(i)=
\frac{|\delta_i|^\alpha}
{\sum_j|\delta_j|^\alpha}
}
\]

## Dueling DQN

\[
\boxed{
Q(s,a)=
V(s)+
\left(
A(s,a)-\operatorname{mean}_{a'}A(s,a')
\right)
}
\]

---

# 33. Exam Memory Table

| Concept | Remember |
|---|---|
| DQN | Neural network approximates \(Q(s,a)\) |
| Online network | Gets updated |
| Target network | Provides stable target |
| Replay buffer | Stores and randomly samples experience |
| Epsilon-greedy | Balances exploration/exploitation |
| Double DQN | Online selects, target evaluates |
| Dueling DQN | \(Q=V+(A-\text{mean}(A))\) |
| PER | High TD-error experiences sampled more |
| Q-learning target | \(r+\gamma\max Q\) |
| DQN problem | Q-value overestimation |
| Double DQN solution | Separate selection and evaluation |
```

### Important source-based corrections

For **Q1, Q2 and Q3**, the supplied question does **not contain enough numerical information for a unique final parameter/Q-value update**. I have deliberately not invented missing values:

- **Q1:** missing \(\max Q(s',a')\).
- **Q2:** missing current \(Q(s,a)\) and learning rate, so \(7.7\) is the **Double-DQN target**, not the final updated Q-value.
- **Q3:** missing the policy-gradient derivative and learning rate, so the exact network-parameter update cannot be calculated. The meaningful result is the negative advantage and therefore a decrease in the selected action's probability.

