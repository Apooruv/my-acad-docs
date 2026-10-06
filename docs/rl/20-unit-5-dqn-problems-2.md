# Unit 5 — DQN, PER, Dyna-Q, Dueling DQN and A3C

## Source PDFs

- [Deep RL Tutorial](pdfs/Deep-RL-Tutorial%20%281%29.pdf)
- [RL Question Bank](pdfs/QUESTIONS%20_rl%20%282%29.pdf)
- [L6 — Reinforcement Learning](pdfs/L6%20%283%29.pdf)
- [DRL Class Assignment](pdfs/Real%20%281%29.pdf)

---

# Q6. Exploration–Exploitation Trade-off in DQN

> **Question:** In a Deep Q-Network (DQN) setup, an agent needs to balance between exploration (trying new actions) and exploitation (choosing the best-known actions).
>
> **Problem:** Explain the importance of the exploration-exploitation tradeoff in DQN. What techniques can be used to maintain this balance, and how do they impact learning?

## Answer

The agent has two competing objectives:

### Exploration

The agent tries actions that may not currently appear optimal.

Purpose:

- discover better actions;
- collect new experiences;
- avoid getting stuck with a poor policy.

### Exploitation

The agent chooses the action with the highest estimated Q-value:

\[
a^*=\arg\max_a Q(s,a)
\]

Purpose:

- use the knowledge already learned;
- obtain high rewards based on current estimates.

---

## Why is the trade-off important?

If the agent only exploits:

\[
\boxed{\text{Too much exploitation}}
\]

it may repeatedly select a suboptimal action and never discover better actions.

If the agent only explores:

\[
\boxed{\text{Too much exploration}}
\]

it spends too much time taking random actions and may learn slowly.

Therefore, DQN needs a balance.

---

## 1. Epsilon-Greedy

The most common method is:

\[
\epsilon\text{-greedy}
\]

With probability:

\[
\epsilon
\]

choose a random action.

With probability:

\[
1-\epsilon
\]

choose:

\[
\arg\max_aQ(s,a)
\]

Therefore:

```text
                    Action
                       |
             +---------+---------+
             |                   |
        probability ε       probability 1-ε
             |                   |
             ▼                   ▼
        Random action       Best Q action
          Explore             Exploit
```

### Epsilon decay

Initially:

\[
\epsilon\approx1
\]

so the agent explores heavily.

As learning progresses:

\[
\epsilon\downarrow
\]

and exploitation increases.

Typical concept:

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

## 2. Other exploration strategies

Other possible strategies include:

- decaying epsilon;
- softmax/Boltzmann action selection;
- noisy networks;
- exploration bonuses.

For an exam answer, **epsilon-greedy with epsilon decay** is the most important technique.

---

## Effect on learning

| Strategy | Effect |
|---|---|
| High exploration | More states/actions discovered |
| High exploitation | Faster use of learned knowledge |
| Too much exploration | Slow convergence |
| Too much exploitation | May get stuck in poor policy |
| Decaying epsilon | Exploration early, exploitation later |

### Exam conclusion

> The exploration-exploitation trade-off is essential because the agent must discover potentially better actions while also exploiting actions that are already known to produce good rewards. Epsilon-greedy, especially with a decaying epsilon, provides a simple mechanism for achieving this balance.

---

# Q7. Role of Target Network in DQN

> **Question:** DQN uses a separate target network to stabilize training.
>
> **Problem:** Describe why the target network is necessary in DQN. How would the learning process be affected if both the target and primary networks were updated simultaneously?

## Answer

DQN uses two networks:

1. **Online/primary network**
2. **Target network**

---

## Online network

The online network has parameters:

\[
\theta
\]

It is continuously updated during training.

It estimates:

\[
Q(s,a;\theta)
\]

---

## Target network

The target network has parameters:

\[
\theta^-
\]

It is used to calculate the Bellman target:

\[
\boxed{
y=
r+\gamma\max_{a'}Q(s',a';\theta^-)
}
\]

The target network is updated less frequently.

For example:

\[
\boxed{\theta^-\leftarrow\theta}
\]

after a fixed number of training steps.

---

## Why is it necessary?

Without a target network, the same network would be responsible for both:

### Prediction

\[
Q(s,a;\theta)
\]

and:

### Target

\[
r+\gamma\max_{a'}Q(s',a';\theta)
\]

Therefore, when the network parameters change, the target also changes immediately.

This creates a **moving target**.

The resulting feedback can cause:

- unstable learning;
- oscillating Q-values;
- divergence;
- slower convergence.

The supplied tutorial describes the target network as the network used to produce the DQN target while the online network is trained toward it. Deep-RL-Tutorial (1)

---

## If both networks were updated simultaneously

Suppose:

\[
\theta\rightarrow\theta'
\]

and the target also immediately becomes:

\[
\theta^-\rightarrow\theta'
\]

Then:

\[
y=r+\gamma\max Q(s',a';\theta^-)
\]

would change whenever the prediction changes.

Thus the network would continuously chase a target that is itself moving.

### Exam answer

> The target network provides a relatively stable reference for calculating the Bellman target. If the target and primary networks were updated simultaneously, the target would change continuously with the prediction network, increasing feedback and instability and potentially causing oscillation or divergence.

---

# Q8. Double DQN and Q-Value Overestimation

> **Question:** One of the limitations of DQN is that it tends to overestimate Q-values, leading to suboptimal policies in some cases.
>
> **Problem:** Explain how Double DQN mitigates the problem of Q-value overestimation. What is the main conceptual difference between DQN and Double DQN, and how does it improve the reliability of action selection?

## Answer

## Problem in standard DQN

Standard DQN calculates:

\[
y=
r+
\gamma
\max_{a'}Q(s',a';\theta^-)
\]

The maximum operation selects the largest estimated value.

Because neural-network Q-values contain estimation errors, the maximum may preferentially select an overestimated value.

Therefore:

\[
\boxed{\text{DQN can suffer from overestimation bias}}
\]

---

# Double DQN solution

Double DQN separates:

1. **Action selection**
2. **Action evaluation**

### Step 1 — Online network selects action

\[
\boxed{
a^*
=
\arg\max_{a'}Q(s',a';\theta)
}
\]

### Step 2 — Target network evaluates that action

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

The supplied Deep RL tutorial explicitly describes this as the key difference between vanilla DQN and Double DQN. Deep-RL-Tutorial (1)

---

## DQN vs Double DQN

| DQN | Double DQN |
|---|---|
| Target network performs max | Online network selects action |
| Same target estimate determines selection/evaluation | Target network evaluates selected action |
| More susceptible to overestimation | Reduces overestimation |
| Can produce overly optimistic Q-values | More reliable Q-value estimates |

### Memory trick

\[
\boxed{\text{Double DQN = Online picks + Target evaluates}}
\]

---

## Why does this improve reliability?

Suppose the online network accidentally overestimates one action.

Double DQN does not automatically use that same estimated value as the final evaluation.

Instead:

```text
Online Network
      |
      | selects action
      ▼
     a*
      |
      ▼
Target Network
      |
      | evaluates a*
      ▼
   Target Q-value
```

Thus the two roles are decoupled.

### Exam conclusion

> Double DQN reduces overestimation bias by decoupling action selection from action evaluation. The online network selects the best action, while the target network evaluates that action. This makes the target value more reliable and produces more stable action selection.

---

# Q9. Actor-Critic Method

> **Question:** In the Actor-Critic method, two networks (the Actor and the Critic) work together to optimize the policy.
>
> **Problem:** Describe the roles of the Actor and the Critic in this method. How does the Critic guide the Actor, and why is it advantageous to separate these functions into two networks rather than using a single Q-value network as in DQN?

## Answer

Actor-Critic consists of two components:

\[
\boxed{\text{Actor}+\text{Critic}}
\]

---

# 1. Actor

The Actor represents the policy:

\[
\boxed{\pi(a|s)}
\]

It receives the current state and produces action probabilities.

For example:

```text
State s
   |
   ▼
Actor
   |
   ├── action A: 0.2
   ├── action B: 0.6
   └── action C: 0.2
```

The Actor decides **what action to take**.

---

# 2. Critic

The Critic estimates how good the current state or action is.

A common state-value formulation is:

\[
V(s)
\]

The Critic evaluates the Actor's behavior.

It can calculate a TD error:

\[
\boxed{
\delta=
r+\gamma V(s')-V(s)
}
\]

The supplied tutorial uses this TD error as the shared learning signal between Actor and Critic. Deep-RL-Tutorial (1)

---

# 3. How does the Critic guide the Actor?

The sign of the TD error determines whether the selected action was better or worse than expected.

### If:

\[
\delta>0
\]

the outcome was better than expected.

Therefore:

\[
\boxed{\text{increase probability of the action}}
\]

### If:

\[
\delta<0
\]

the outcome was worse than expected.

Therefore:

\[
\boxed{\text{decrease probability of the action}}
\]

The Actor's policy-gradient term is based on this signal:

\[
\boxed{
\nabla J
\propto
\delta\nabla\log\pi(a|s)
}
\]

---

# 4. Why use two networks?

The two networks have different jobs.

| Actor | Critic |
|---|---|
| Chooses actions | Evaluates actions/state |
| Represents policy | Represents value |
| Improves policy | Provides learning signal |
| Answers "What should I do?" | Answers "How good was that?" |

Separating them allows the Critic to provide a more informative learning signal to the Actor.

---

# 5. Advantage over using only a Q-network

DQN directly learns:

\[
Q(s,a)
\]

and chooses actions based on the estimated Q-values.

Actor-Critic instead learns a policy directly through the Actor while using the Critic as a value estimator.

This is useful when we want a direct policy representation.

The supplied tutorial summarizes Actor-Critic as:

> a policy network that acts + a value network that grades each step through TD error. Deep-RL-Tutorial (1)

### Exam conclusion

> The Actor selects actions according to the policy, while the Critic evaluates the quality of the decisions. The TD error provides feedback to both networks. Separating the two roles allows the Actor to directly learn a policy while the Critic provides a lower-variance learning signal for improving that policy.

---

# Q10. Prioritized Experience Replay

> **Question:** Describe the concept of Prioritized Experience Replay and its benefits over uniform sampling. How does prioritizing certain experiences improve the learning process, and what potential drawbacks might arise from this approach?

## Answer

A standard replay buffer samples experiences approximately uniformly.

For example:

```text
Experience 1 ─┐
Experience 2 ─┤
Experience 3 ─┼── Random sampling
Experience 4 ─┤
Experience 5 ─┘
```

Prioritized Experience Replay (PER) changes this.

Experiences with larger learning errors are given higher priority.

---

# 1. Priority based on TD error

A common priority is:

\[
\boxed{
p_i=|\delta_i|^\alpha
}
\]

where:

- \(\delta_i\) = TD error;
- \(\alpha\) = priority exponent.

The sampling probability is:

\[
\boxed{
P(i)=
\frac{p_i}
{\sum_jp_j}
}
\]

or equivalently:

\[
\boxed{
P(i)=
\frac{|\delta_i|^\alpha}
{\sum_j|\delta_j|^\alpha}
}
\]

---

# 2. Why prioritize experiences?

A large TD error means the current prediction is significantly different from the target.

Therefore, that experience may contain useful information for learning.

Example:

```text
Small TD error
       ↓
Already mostly learned
       ↓
Low priority

Large TD error
       ↓
Prediction is poor
       ↓
High priority
```

---

# 3. Advantages

### 1. Faster learning

Important experiences are replayed more frequently.

### 2. Better sample efficiency

The agent spends more updates on informative experiences.

### 3. Rare important events receive attention

For example, an unusual action leading to a large reward or penalty can be replayed more often.

The supplied class assignment gives exactly this type of maze example: critical experiences that are rare may be replayed more frequently using PER. Real (1)

---

# 4. Drawbacks

### 1. Sampling bias

The replay distribution is no longer uniform.

This can bias learning.

### 2. Computational overhead

Priorities have to be calculated and maintained.

### 3. Very high-error experiences can dominate

The agent may repeatedly train on a small subset of experiences.

### 4. Requires correction

PER commonly uses importance-sampling corrections to reduce the bias introduced by non-uniform sampling.

---

## Uniform vs PER

| Uniform Replay | PER |
|---|---|
| Experiences sampled roughly equally | Experiences have different probabilities |
| Simple | More complex |
| No priority calculation | Uses TD error |
| May waste updates on uninformative data | Focuses on informative data |
| Lower overhead | Higher overhead |

### Exam conclusion

> PER improves sample efficiency by replaying experiences with larger TD errors more frequently. However, non-uniform sampling introduces bias and additional computational complexity, and very high-priority experiences can dominate training.

---

# Q11. Replay Buffer

> **Question:** The Replay Buffer stores past experiences to break correlation between consecutive samples and allow more efficient learning.
>
> **Problem:** Discuss why the Replay Buffer is essential in DQN and how it differs from training without one. What would happen if the Replay Buffer was too small or too large?

## Answer

A replay buffer stores transitions:

\[
\boxed{
(s,a,r,s',done)
}
\]

The agent collects experiences while interacting with the environment.

Instead of immediately training only on the latest experience, DQN stores it and later samples a random mini-batch.

---

# 1. Why is it essential?

## Breaks correlation

Consecutive experiences are highly correlated:

\[
s_1\rightarrow s_2\rightarrow s_3\rightarrow s_4
\]

Random replay produces a more diverse training batch.

---

## Reuses experiences

An experience can be sampled multiple times.

Therefore:

\[
\boxed{\text{one experience can contribute to multiple updates}}
\]

---

## Improves sample efficiency

The agent gets more learning value from each interaction.

---

# 2. Without replay buffer

Without replay:

```text
Environment
    ↓
Current transition
    ↓
Immediate training
    ↓
Next transition
    ↓
Immediate training
```

The samples are strongly correlated.

This can make neural-network training unstable.

---

# 3. With replay buffer

```text
Environment
    ↓
Experiences
    ↓
Replay Buffer
    ↓
Random mini-batch
    ↓
DQN training
```

This reduces correlation and allows old experiences to be reused.

---

# 4. If buffer is too small

A small buffer:

- has low experience diversity;
- quickly overwrites old experiences;
- may produce correlated samples;
- may cause unstable learning.

\[
\boxed{
\text{Too small → poor diversity}
}
\]

---

# 5. If buffer is too large

A very large buffer:

- consumes more memory;
- may retain outdated experiences;
- can make the training distribution stale.

\[
\boxed{
\text{Too large → stale data + high memory use}
}
\]

### Exam conclusion

> The replay buffer is essential because it decorrelates training samples, allows experience reuse, and improves sample efficiency. A buffer that is too small lacks diversity, while an excessively large buffer can consume significant memory and retain stale experiences.

---

# Q12. DyNa-Q Framework

> **Question:** The DyNa-Q framework combines model-based and model-free learning by simulating experience using a learned model of the environment.
>
> **Problem:** Explain how the DyNa-Q framework utilizes simulated experiences to improve learning efficiency. What are the benefits of adding simulated planning steps, and how does it differ conceptually from pure model-free approaches?

## Answer

DyNa-Q combines:

\[
\boxed{
\text{Model-free learning}
+
\text{Model-based planning}
}
\]

The idea is to learn a model of the environment and use that model to generate additional simulated experiences.

---

# 1. Model-free learning

In pure model-free RL, the agent learns from actual interactions:

\[
(s,a,r,s')
\]

It does not explicitly learn the transition dynamics of the environment.

The Q-function is learned directly from experience.

---

# 2. Model-based learning

A model attempts to approximate the environment.

Conceptually:

\[
(s,a)
\rightarrow
(\hat r,\hat s')
\]

The model predicts:

- what next state may occur;
- what reward may be obtained.

The agent can then use these predictions for planning.

---

# 3. DyNa-Q idea

The basic process is:

```text
             Real Environment
                    |
                    ▼
              Real Experience
                    |
                    ▼
              Learned Model
                    |
          ┌─────────┴─────────┐
          ▼                   ▼
     Model-free Q        Simulated Experience
          ▲                   |
          |                   ▼
          └──────── Planning ─┘
```

Instead of learning only from real transitions, the agent also performs simulated planning steps.

---

# 4. Why are simulated experiences useful?

Suppose the agent has collected only a small number of real experiences.

The learned model can generate additional hypothetical transitions.

Thus:

\[
\boxed{
\text{More learning updates from limited real interaction}
}
\]

Potential benefits include:

- improved sample efficiency;
- faster propagation of reward information;
- additional Q-function updates;
- less dependence on real environment interaction.

---

# 5. Difference from pure model-free RL

### Pure model-free

\[
\boxed{
\text{Learn directly from real experience}
}
\]

### DyNa-Q

\[
\boxed{
\text{Learn from real experience + simulated planning}
}
\]

Therefore, DyNa-Q can extract additional learning from the experiences already collected.

---

# 6. Main limitation

The simulated experience is only useful if the learned model is reasonably accurate.

If the model makes errors:

\[
\text{model error}
\rightarrow
\text{incorrect simulated transition}
\rightarrow
\text{incorrect learning}
\]

The supplied L6 material specifically highlights this problem: model-based deep RL can suffer from **compounding errors**, where transition-model errors accumulate along a simulated trajectory. L6 (3)

Thus:

\[
\boxed{
\text{Planning improves efficiency but introduces model error}
}
\]

### Exam conclusion

> DyNa-Q combines model-free Q-learning with model-based planning. A learned model is used to simulate additional transitions, allowing the Q-function to receive more training updates from limited real experience. Its main advantage is improved sample efficiency, while its main limitation is that inaccurate model predictions can introduce errors into the simulated experience.

---

# Q13. Dueling Q-Network

> **Question:** The Duelling Q-Network architecture separates the Q-value function into a state value function and an action advantage function.
>
> **Problem:** Describe the motivation behind the Duelling Q-Network architecture. How does separating state and action values help the network focus on learning critical states more effectively?

## Answer

Dueling DQN changes the architecture used to estimate Q-values.

Instead of directly producing:

\[
Q(s,a)
\]

the network produces two components:

1. State value:

\[
V(s)
\]

2. Action advantage:

\[
A(s,a)
\]

---

# 1. State value

\[
V(s)
\]

answers:

> How good is it to be in state \(s\)?

It does not distinguish between individual actions.

---

# 2. Action advantage

\[
A(s,a)
\]

answers:

> How much better or worse is action \(a\) compared with the other actions in state \(s\)?

---

# 3. Combining them

The Dueling DQN combines the two:

\[
\boxed{
Q(s,a)
=
V(s)
+
\left[
A(s,a)-\operatorname{mean}_{a'}A(s,a')
\right]
}
\]

The mean-subtraction term makes the decomposition identifiable.

The supplied tutorial gives this exact equation and explains that subtracting the mean prevents \(V\) and \(A\) from freely drifting. Deep-RL-Tutorial (1)

---

# 4. Why is this useful?

Consider a state where most actions have approximately the same effect.

A conventional DQN must learn the Q-value for every action.

Dueling DQN can instead learn:

\[
V(s)
\]

to capture the overall quality of the state.

Then the advantage stream only needs to determine which actions are better or worse.

Therefore:

\[
\boxed{
\text{State importance is learned separately from action importance}
}
\]

---

# 5. Example

Suppose a drone is far away from obstacles.

Actions:

- move slightly left;
- move slightly right;
- move forward;
- hover.

At this point, several actions may have nearly identical effects.

The important information is:

\[
\boxed{\text{the current state is relatively safe/good}}
\]

Dueling DQN can learn this through:

\[
V(s)
\]

without needing large differences between every action's Q-value.

The supplied class assignment uses autonomous drone navigation as an example of this motivation. Real (1)

---

# 6. Architecture

```text
                 State
                   |
                   ▼
             Shared layers
                   |
             ┌─────┴─────┐
             ▼           ▼
       Value stream   Advantage stream
             |           |
            V(s)       A(s,a)
             |           |
             └─────┬─────┘
                   ▼
            Combine streams
                   |
                   ▼
                Q(s,a)
```

---

# 7. Advantages

- learns state value separately;
- focuses the advantage stream on action differences;
- can learn useful state representations more efficiently;
- particularly useful when many actions have similar effects.

### Exam conclusion

> Dueling DQN separates the overall value of a state from the relative advantage of each action. This allows the network to learn how valuable a state is independently of the precise action taken and can improve learning efficiency in states where many actions have similar outcomes.

---

# Q14. Asynchronous Advantage Actor-Critic (A3C)

> **Question:** In Asynchronous Advantage Actor-Critic (A3C), multiple agents operate in parallel, updating a shared global policy asynchronously.
>
> **Problem:** Explain how asynchronous updates in A3C help address convergence issues and lead to faster learning. What are the key advantages and challenges of asynchronous learning compared to synchronized learning methods?

## Answer

A3C stands for:

\[
\boxed{\text{Asynchronous Advantage Actor-Critic}}
\]

The main idea is to run multiple instances of agents in parallel.

Each worker interacts with its own environment and periodically updates a shared global network.

---

# 1. Basic architecture

```text
                  Global Network
                  /      |      \
                 /       |       \
                ▼        ▼        ▼
             Worker 1  Worker 2  Worker 3
                |        |        |
                ▼        ▼        ▼
            Environment Environment Environment
```

Each worker:

1. interacts with its environment;
2. collects experience;
3. calculates gradients;
4. updates the shared global parameters.

The L6 material describes asynchronous deep RL as executing many agent instances in parallel with shared network parameters. L6 (3)

---

# 2. Why multiple workers?

A single agent produces highly correlated experiences:

\[
s_1\rightarrow s_2\rightarrow s_3\rightarrow s_4
\]

Different workers interact with environments at different times and can encounter different states.

Therefore, the collected experiences are naturally more diverse.

This helps decorrelate the training data.

---

# 3. Asynchronous updates

Workers do not have to wait for all other workers before applying their updates.

Conceptually:

```text
Worker 1 ──► Global Network
Worker 2 ───────► Global Network
Worker 3 ──► Global Network
Worker 4 ───────────► Global Network
```

The updates occur asynchronously.

---

# 4. How does this help learning?

### 1. Data decorrelation

Different workers experience different trajectories.

Therefore, training data becomes less correlated.

### 2. Parallel experience collection

Several environments are explored simultaneously.

Thus:

\[
\boxed{
\text{more experience per unit of wall-clock time}
}
\]

### 3. Reduced dependence on replay

The L6 material specifically notes that parallelism decorrelates data and can provide an alternative to experience replay. L6 (3)

### 4. Faster learning

Multiple workers collect experiences concurrently rather than relying on one sequential interaction stream.

---

# 5. Actor-Critic component

A3C uses:

### Actor

Policy:

\[
\pi(a|s)
\]

### Critic

Value estimate:

\[
V(s)
\]

The advantage is used to determine whether the action was better than expected.

A common form is:

\[
A(s,a)=R-V(s)
\]

and the policy gradient uses:

\[
\boxed{
\nabla J
\propto
A(s,a)\nabla\log\pi(a|s)
}
\]

The L6 material gives the advantage actor-critic formulation in terms of:

\[
(R_t-V(s_t,\theta))
\nabla_\omega\log\pi(a_t|s_t,\omega)
\]

L6 (3)

---

# 6. Advantages of asynchronous learning

## Advantage 1 — Parallelism

Multiple agents collect experience simultaneously.

## Advantage 2 — Better exploration

Different workers may explore different parts of the environment.

## Advantage 3 — Data decorrelation

Different trajectories reduce the correlation problem.

## Advantage 4 — Can avoid replay memory

The natural diversity of parallel workers can reduce the need for an experience replay buffer.

## Advantage 5 — Faster practical training

Parallel workers can increase the rate at which useful experience is generated.

---

# 7. Challenges

## 1. Stale parameters

A worker may calculate an update using slightly older global parameters.

By the time the update is applied, another worker may already have changed the network.

---

## 2. Asynchronous conflicts

Multiple workers can update shared parameters at nearly the same time.

This makes optimization more complicated.

---

## 3. Hardware requirements

Multiple workers require additional CPU/GPU resources.

---

## 4. Implementation complexity

Synchronization and shared-parameter management make the system more complicated than a simple single-agent implementation.

---

# 8. Asynchronous vs Synchronous Learning

| Asynchronous | Synchronous |
|---|---|
| Workers update independently | Workers synchronize |
| Updates can occur at different times | Updates are coordinated |
| Less waiting | More waiting |
| Naturally decorrelated data | Batch synchronization needed |
| Can have stale gradients | Gradients are more consistent |
| More implementation complexity | Simpler coordination |

---

# 9. Why A3C can converge better

The important idea is not simply "asynchronous = guaranteed convergence."

Rather, parallel workers:

\[
\boxed{
\text{produce diverse trajectories}
}
\]

which helps reduce the correlation in sequential experience.

The shared global network then receives updates from these different trajectories.

Thus learning can become more stable and efficient than relying on a single correlated trajectory.

### Exam conclusion

> A3C uses multiple parallel workers that interact with environments independently and asynchronously update a shared global Actor-Critic network. The parallel workers generate diverse, less-correlated experience and allow faster experience collection. However, asynchronous learning introduces stale gradients, shared-update conflicts, implementation complexity and additional computational requirements.

---

# Quick Revision — Q6 to Q14

| Question | Core idea |
|---|---|
| Q6 | Exploration vs exploitation |
| Q7 | Target network stabilizes DQN |
| Q8 | Double DQN reduces overestimation |
| Q9 | Actor acts, Critic evaluates |
| Q10 | PER samples high-TD-error experiences |
| Q11 | Replay buffer decorrelates/reuses experience |
| Q12 | Dyna-Q combines model-free learning with simulated planning |
| Q13 | Dueling DQN separates \(V(s)\) and \(A(s,a)\) |
| Q14 | A3C uses parallel asynchronous workers |

---

# Must-Memorize Formulas

## DQN

\[
\boxed{
y=r+\gamma\max_{a'}Q(s',a';\theta^-)
}
\]

## Double DQN

\[
\boxed{
a^*=\arg\max_{a'}Q(s',a';\theta)
}
\]

\[
\boxed{
y=r+\gamma Q(s',a^*;\theta^-)
}
\]

## Actor-Critic TD error

\[
\boxed{
\delta=r+\gamma V(s')-V(s)
}
\]

## Policy-gradient form

\[
\boxed{
\nabla J\propto
\delta\nabla\log\pi(a|s)
}
\]

## PER

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
Q(s,a)
=
V(s)
+
A(s,a)-\operatorname{mean}_{a'}A(s,a')
}
\]

---

# One-Line Memory Tricks

**DQN**

> Neural network approximates Q-values.

**Target Network**

> Fixed/slow target prevents the network from chasing itself.

**Double DQN**

> Online picks, target evaluates.

**Actor-Critic**

> Actor acts, Critic judges.

**PER**

> Large TD error → higher replay priority.

**Replay Buffer**

> Store → random sample → learn.

**Dyna-Q**

> Real experience → learned model → simulated experience → extra learning.

**Dueling DQN**

> State value + action advantage.

**A3C**

> Many workers → shared network → asynchronous updates.
