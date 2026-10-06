# Reinforcement Learning

Complete exam-oriented notes for **Reinforcement Learning**.

---

## Unit 4 — Foundations of Reinforcement Learning

### 1. Markov Decision Process

[MDP](01-mdp.md)

- Markov property
- States and actions
- Rewards
- Transition model
- Policies
- Returns
- Episodes

---

### 2. Returns and Value Functions

[Returns and Value Functions](02-returns-and-value-functions.md)

- Return
- Discount factor
- State-value function
- Action-value function
- Relationship between value functions

---

### 3. Bellman Equations

[Bellman Equations](03-bellman-equations.md)

- Bellman expectation equation
- Bellman optimality equation
- State-value formulation
- Action-value formulation
- Numerical problems

---

### 4. Policy Iteration

[Policy Iteration](04-policy-iteration.md)

- Policy evaluation
- Policy improvement
- Policy iteration algorithm
- Numerical examples

---

### 5. Passive Learning

[Passive Learning](05-passive-learning.md)

- Passive learning
- Fixed policy
- Utility estimation
- Learning process
- Methods of passive learning

---

### 6. Direct Utility Estimation

[Direct Utility Estimation](06-direct-utility-estimation.md)

- Monte Carlo utility estimation
- Episode returns
- Utility calculation
- Advantages and disadvantages

---

### 7. Monte Carlo Methods

[Monte Carlo Methods](07-monte-carlo-methods.md)

- First-visit Monte Carlo
- Every-visit Monte Carlo
- Return estimation
- Policy evaluation
- Advantages and disadvantages

---

### 8. Temporal Difference Learning

[Temporal Difference Learning](08-temporal-difference-learning.md)

- TD prediction
- TD error
- TD update
- Bootstrapping
- TD vs Monte Carlo

---

### 9. Passive Learning Comparison

[Passive Learning Comparison](09-passive-learning-comparison.md)

- Direct Utility Estimation
- Monte Carlo
- Temporal Difference Learning
- Comparison
- Advantages and disadvantages

---

### 10. Active Learning

[Active Learning](10-active-learning.md)

- Exploration
- Exploitation
- Epsilon-greedy strategy
- Learning action values
- Active learning process

---

### 11. Q-Learning

[Q-Learning](11-q-learning.md)

- Q-learning algorithm
- Q-value update
- Learning rate
- Discount factor
- Exploration
- Numerical problems

---

### 12. SARSA

[SARSA](12-sarsa.md)

- SARSA algorithm
- On-policy learning
- SARSA update
- Numerical problems

---

### 13. Q-Learning vs SARSA

[Q-Learning vs SARSA](13-q-learning-vs-sarsa.md)

- On-policy vs off-policy
- Update equations
- Exploration
- Comparison
- Numerical example

---

### 14. Model-Based vs Model-Free RL

[Model-Based vs Model-Free](14-model-based-vs-model-free.md)

- Model-based reinforcement learning
- Model-free reinforcement learning
- Differences
- Advantages and disadvantages
- Examples

---

### 15. Unit 4 Problems — 1

[Unit 4 Problems 1](15-unit-4-problems-1.md)

---

### 16. Unit 4 Problems — 2

[Unit 4 Problems 2](16-unit-4-problems-2.md)

---

### 17. Unit 4 Problems — 3

[Unit 4 Problems 3](17-unit-4-problems-3.md)

---

## Unit 5 — Deep Reinforcement Learning

### 18. Deep Q-Network

[DQN](19-dqn.md)

- Deep Q-Network
- Neural network approximation
- Replay buffer
- Target network
- DQN architecture
- DQN algorithm

---

### 19. DQN Problems

[Unit 5 DQN Problems](20-unit-5-dqn-problems-2.md)

- DQN numerical problems
- Target calculation
- Q-value updates
- Experience replay
- Target network

---

### 20. Passive and Active Learning

[Unit 5 Passive and Active Learning](21-unit-5-passive-active-learning.md)

- Passive learning
- Active learning
- Comparison
- Reinforcement learning workflow

---

### 21. Proximal Policy Optimization

[PPO](22-ppo.md)

- Policy gradient
- Actor-Critic
- PPO
- Clipped objective
- Advantages
- PPO numerical problems

---

## Revision — Unit 4

### MDP, Bellman Equation and Policy Iteration

[MDP, Bellman & Policy Iteration](23-mdp-bellman-policy-iteration.md)

- MDP revision
- Bellman equations
- Policy iteration
- Important formulas
- Numerical problems

---

## Question Banks and Solutions

### Questions RL

[Solutions — Questions RL](24-solutions-questions-rl.md)

---

### RL CSAI Sample Questions

[Solutions — RL CSAI Sample](25-solutions-rl-csai-sample.md)

---

### Real Deep RL Assignment

[Solutions — Real DRL Assignment](26-solutions-real-drl-assignment.md)

---

## Additional Exam Practice

### Additional Exam Numericals and Practice

[Additional Exam Numericals and Practice](27-additional-exam-numericals-and-practice.md)

This section contains additional exam-oriented problems covering:

- MDP
- Returns
- Bellman equations
- Policy evaluation
- Policy improvement
- Direct Utility Estimation
- Monte Carlo
- Temporal Difference Learning
- Q-Learning
- SARSA
- DQN
- Double DQN
- Dueling DQN
- Actor-Critic
- PPO
- Prioritized Experience Replay
- Replay Buffer
- Dyna-Q
- Model-Based vs Model-Free RL

---

## Exam Revision Order

For the exam, revise in this order:

1. [MDP](01-mdp.md)
2. [Returns and Value Functions](02-returns-and-value-functions.md)
3. [Bellman Equations](03-bellman-equations.md)
4. [Policy Iteration](04-policy-iteration.md)
5. [Passive Learning](05-passive-learning.md)
6. [Direct Utility Estimation](06-direct-utility-estimation.md)
7. [Monte Carlo Methods](07-monte-carlo-methods.md)
8. [Temporal Difference Learning](08-temporal-difference-learning.md)
9. [Passive Learning Comparison](09-passive-learning-comparison.md)
10. [Active Learning](10-active-learning.md)
11. [Q-Learning](11-q-learning.md)
12. [SARSA](12-sarsa.md)
13. [Q-Learning vs SARSA](13-q-learning-vs-sarsa.md)
14. [Model-Based vs Model-Free](14-model-based-vs-model-free.md)
15. [DQN](19-dqn.md)
16. [PPO](22-ppo.md)
17. [Additional Exam Numericals](27-additional-exam-numericals-and-practice.md)

---

## Quick Revision

### Unit 4

**MDP → Bellman → Policy Iteration → Passive Learning → MC → TD → Active Learning → Q-Learning → SARSA → Model-Based/Model-Free**

### Unit 5

**DQN → Double DQN → Dueling DQN → Replay Buffer → PER → Actor-Critic → PPO → Dyna-Q → Asynchronous Deep RL**

---

## Important Numerical Topics

Before the exam, make sure you can solve:

- Return calculation
- Bellman expectation equation
- Bellman optimality equation
- Policy evaluation
- Policy improvement
- Direct Utility Estimation
- Monte Carlo update
- TD update
- Q-Learning update
- SARSA update
- DQN target calculation
- Double DQN target calculation
- Dueling DQN calculation
- Actor-Critic TD error
- PPO objective
- Prioritized Experience Replay
- Dyna-Q update

---

## Final Formula Revision

### Return

\[
G_t = R_{t+1} + \gamma R_{t+2} + \gamma^2R_{t+3} + \cdots
\]

### Bellman Expectation

\[
V^\pi(s)
=
\sum_a \pi(a|s)
\sum_{s',r}
P(s',r|s,a)
[r+\gamma V^\pi(s')]
\]

### Bellman Optimality

\[
V^*(s)
=
\max_a
\sum_{s',r}
P(s',r|s,a)
[r+\gamma V^*(s')]
\]

### TD Update

\[
V(s)
\leftarrow
V(s)+\alpha
[r+\gamma V(s')-V(s)]
\]

### Q-Learning

\[
Q(s,a)
\leftarrow
Q(s,a)+
\alpha
[r+\gamma\max_{a'}Q(s',a')-Q(s,a)]
\]

### SARSA

\[
Q(s,a)
\leftarrow
Q(s,a)+
\alpha
[r+\gamma Q(s',a')-Q(s,a)]
\]

### DQN Target

\[
y =
r+\gamma\max_{a'}Q_{\text{target}}(s',a')
\]

### TD Error

\[
\delta =
r+\gamma V(s')-V(s)
\]

---

## Complete Coverage

This folder contains:

- Unit 4 theory
- Unit 4 numerical problems
- Unit 5 DQN material
- PPO
- Question-bank solutions
- Assignment solutions
- Additional exam-oriented numericals
- Final formula revision
