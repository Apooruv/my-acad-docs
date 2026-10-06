# Reinforcement Learning

> **Exam-focused notes for Unit 4 and Unit 5**
>
> Coverage is based primarily on the syllabus and the RL resources provided by the course instructor.  
> The notes prioritize **definitions, algorithms, formulas, comparisons, and problem solving** over general RL fluency.

---

# Syllabus

## Unit 4 — Reinforcement Learning

### Core RL Concepts

- MDP
- Bellman Equation
- Policy Iteration

### Passive Learning

- Key concepts
- Process
- Direct Utility Estimation
- Temporal Difference Learning
- Monte Carlo Methods
- Advantages and disadvantages

### Active Learning

- Key concepts
- Process
- Q-Learning
- SARSA
- Advantages and disadvantages

### RL Models

- Model-Based Reinforcement Learning
- Model-Free Reinforcement Learning

---

## Unit 5 — Deep Reinforcement Learning

### DQN

- Deep Q-Network
- Types of DQN
- Components
- Replay Buffer

### Advanced DQN

- Double DQN
- Dueling Q-Network
- Prioritized Experience Replay

### Policy-Based / Actor-Critic

- Actor-Critic Method
- Proximal Policy Optimization

### Other Deep RL

- DyNa-Q Framework
- Asynchronous Deep RL

---

# Unit 4 — Foundations

## 1. MDP

[MDP](01-mdp.md)

Topics:

- Markov Decision Process
- States
- Actions
- Rewards
- Transition probabilities
- Policies
- Discount factor
- Return
- MDP formulation

---

## 2. Bellman Equation

[Bellman Equation](02-bellman-equation.md)

Topics:

- State-value function
- Action-value function
- Bellman expectation equation
- Bellman optimality equation
- Discounted future rewards
- Bellman backup

---

## 3. Policy Iteration

[Policy Iteration](03-policy-iteration.md)

Topics:

- Policy evaluation
- Policy improvement
- Policy iteration algorithm
- Convergence
- Relation to Bellman equations

---

## 4. Passive Learning

[Passive Learning](04-passive-learning.md)

Topics:

- Passive RL
- Fixed policy
- Utility estimation
- Direct Utility Estimation
- Temporal Difference learning
- Monte Carlo learning
- Comparison of methods

---

## 5. Temporal Difference Learning

[Temporal Difference Learning](05-temporal-difference-learning.md)

Topics:

- TD prediction
- TD error
- TD update
- Bootstrapping
- TD vs Monte Carlo

---

## 6. Monte Carlo Methods

[Monte Carlo Methods](06-monte-carlo.md)

Topics:

- Episode-based learning
- Return calculation
- First-visit MC
- Every-visit MC
- Advantages
- Disadvantages

---

## 7. Active Learning

[Active Learning](07-active-learning.md)

Topics:

- Exploration
- Exploitation
- ε-greedy strategy
- Active learning process

---

## 8. Q-Learning

[Q-Learning](08-q-learning.md)

Topics:

- Q-function
- Q-learning algorithm
- Update equation
- Off-policy learning
- Exploration
- Convergence intuition

---

## 9. SARSA

[SARSA](09-sarsa.md)

Topics:

- State-Action-Reward-State-Action
- SARSA update
- On-policy learning
- Exploration
- Q-Learning vs SARSA

---

## 10. Model-Based vs Model-Free RL

[Model-Based vs Model-Free](14-model-based-vs-model-free.md)

Topics:

- Model-based RL
- Model-free RL
- Environment model
- Planning
- Learning directly from experience
- Advantages and disadvantages
- Comparison

---

# Unit 5 — Deep Reinforcement Learning

## 11. Deep Q-Network

[DQN](19-dqn.md)

Topics:

- Motivation for DQN
- Neural-network approximation
- DQN architecture
- Q-value prediction
- Target network
- Experience replay
- DQN training process
- Advantages and limitations

---

## 12. DQN Problems

[DQN Problems](20-unit-5-dqn-problems-2.md)

Focus:

- DQN target calculation
- Q-value updates
- Target network
- Numerical problem solving

---

## 13. Proximal Policy Optimization

[PPO](22-ppo.md)

Topics:

- Policy-gradient motivation
- PPO
- Probability ratio
- Advantage function
- Clipping
- PPO objective
- Advantages and disadvantages

---

# Remaining Unit 5 Topics

The following topics are included in the consolidated numerical/practice file and should be revised together with the corresponding theory notes:

- Double DQN
- Dueling DQN
- Actor-Critic
- Prioritized Experience Replay
- Replay Buffer
- DyNa-Q
- PPO numericals
- Asynchronous Deep RL

---

# Question & Assignment Solutions

## 14. RL Question Paper — Complete Solutions

[Questions RL — Complete Solutions](24-solutions-questions-rl.md)

Source:

[QUESTIONS_rl (2).pdf](pdfs/QUESTIONS_rl%20%282%29.pdf)

Contains complete solutions to:

- Q1–Q21
- Theory questions
- Numerical questions
- Algorithm/application questions

**Use this as the primary question-paper revision file.**

---

## 15. RL CSAI Sample Questions

[RL CSAI Sample — Complete Solutions](25-solutions-rl-csai-sample.md)

Source:

[RL CSAI Sample questions (3).pdf](pdfs/RL%20CSAI%20Sample%20questions%20%283%29.pdf)

Contains complete solutions to:

- Q1–Q17
- Application-based RL questions
- Q-Learning numericals
- Bellman calculations
- Policy questions
- Exploration/exploitation problems

---

## 16. Deep RL Assignment

[Real DRL Assignment — Complete Solutions](26-solutions-real-drl-assignment.md)

Source:

[Real (1).pdf](pdfs/Real%20%281%29.pdf)

Contains complete solutions to:

- Q1–Q10
- PER
- DQN
- Double DQN
- Dueling DQN
- Real-world DRL applications

---

# Final Numerical & Practice File

## 17. Additional Numericals and Exam Practice

[Additional Exam Numericals & Practice](27-additional-exam-numericals-and-practice.md)

This is the **final consolidated numerical practice file**.

It contains:

### Remaining numericals from the supplied resources

- Double DQN numerical
- Dueling DQN numerical
- Actor-Critic numerical

### Additional exam-oriented numericals

- MDP return
- Bellman expectation equation
- Bellman optimality equation
- Policy evaluation
- Policy improvement
- Direct Utility Estimation
- TD learning
- Monte Carlo return
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
- Model-Based vs Model-Free
- Combined Q-Learning vs SARSA problems

### Formula revision

The end of the file contains a compact formula sheet for:

- Return
- Bellman equations
- TD learning
- Q-Learning
- SARSA
- DQN
- Double DQN
- Dueling DQN
- Actor-Critic
- PPO
- PER
- Replay Buffer
- Dyna-Q

---

# Exam Revision Order

For the **highest return in limited preparation time**, use the following order.

## Phase 1 — Understand the Core

1. [MDP](01-mdp.md)
2. [Bellman Equation](02-bellman-equation.md)
3. [Policy Iteration](03-policy-iteration.md)

Then make sure you can solve:

\[
V^\pi(s)
\]

\[
V^*(s)
\]

and policy-improvement calculations.

---

## Phase 2 — Unit 4 Learning Methods

4. [Passive Learning](04-passive-learning.md)
5. [Temporal Difference Learning](05-temporal-difference-learning.md)
6. [Monte Carlo Methods](06-monte-carlo.md)
7. [Active Learning](07-active-learning.md)
8. [Q-Learning](08-q-learning.md)
9. [SARSA](09-sarsa.md)
10. [Model-Based vs Model-Free](14-model-based-vs-model-free.md)

### Must know numericals

\[
G_t
\]

\[
\delta=r+\gamma V(s')-V(s)
\]

\[
V_{\text{new}}=V+\alpha\delta
\]

\[
Q_{\text{new}}
=
Q+\alpha[
r+\gamma\max Q'-Q
]
\]

\[
Q_{\text{SARSA}}
=
Q+\alpha[
r+\gamma Q(s',a')-Q
]
\]

---

# Phase 3 — DQN

11. [DQN](19-dqn.md)
12. [DQN Problems](20-unit-5-dqn-problems-2.md)

Know:

- DQN architecture
- Replay buffer
- Target network
- ε-greedy exploration
- DQN target
- DQN limitations

---

# Phase 4 — Advanced Deep RL

Study:

1. Double DQN
2. Dueling DQN
3. Prioritized Experience Replay
4. Actor-Critic
5. PPO
6. Dyna-Q
7. Asynchronous Deep RL

For each one, know:

- Definition
- Architecture / process
- Core equation
- Algorithm
- Advantages
- Disadvantages
- Difference from related methods
- One numerical/example

---

# Phase 5 — Solve Everything

Use the complete solution files:

1. [RL Questions](24-solutions-questions-rl.md)
2. [RL CSAI Questions](25-solutions-rl-csai-sample.md)
3. [DRL Assignment](26-solutions-real-drl-assignment.md)
4. [Additional Numericals](27-additional-exam-numericals-and-practice.md)

Do not merely read the solutions.

For numerical questions:

> **Hide the solution → solve yourself → compare.**

---

# High-Priority Comparisons

These are especially important for theory questions.

| Comparison | Must Know |
|---|---|
| Monte Carlo vs TD | Yes |
| TD vs Direct Utility Estimation | Yes |
| Q-Learning vs SARSA | **Very important** |
| Model-Based vs Model-Free | **Very important** |
| DQN vs Q-Table | Yes |
| DQN vs Double DQN | **Very important** |
| DQN vs Dueling DQN | **Very important** |
| Uniform Replay vs PER | **Very important** |
| Value-Based vs Policy-Based | Yes |
| Actor-Critic vs Policy Gradient | **Important** |
| PPO vs basic Policy Gradient | **Important** |
| Model-Free vs Dyna-Q | Important |

---

# Formula Checklist

Before the exam, make sure you can write these without looking.

### Return

\[
G_t=
R_{t+1}
+\gamma R_{t+2}
+\gamma^2R_{t+3}
+\cdots
\]

### Bellman Expectation

\[
V^\pi(s)
=
\sum_a\pi(a|s)
[
R+\gamma V^\pi(s')
]
\]

### Bellman Optimality

\[
V^*(s)
=
\max_a
[
R+\gamma V^*(s')
]
\]

### TD Error

\[
\delta=
r+\gamma V(s')-V(s)
\]

### TD Update

\[
V(s)\leftarrow V(s)+\alpha\delta
\]

### Q-Learning

\[
Q(s,a)\leftarrow
Q(s,a)+
\alpha[
r+\gamma\max_{a'}Q(s',a')
-Q(s,a)
]
\]

### SARSA

\[
Q(s,a)\leftarrow
Q(s,a)+
\alpha[
r+\gamma Q(s',a')
-Q(s,a)
]
\]

### DQN Target

\[
y=
r+\gamma\max_{a'}Q_{\text{target}}(s',a')
\]

### Double DQN

\[
a^*=
\arg\max_{a'}Q_{\text{online}}(s',a')
\]

\[
y=
r+\gamma Q_{\text{target}}(s',a^*)
\]

### Dueling DQN

\[
Q(s,a)
=
V(s)+
A(s,a)-\operatorname{mean}(A)
\]

### PER

\[
p_i=|\delta_i|^\alpha
\]

\[
P(i)=
\frac{p_i}{\sum_jp_j}
\]

### Actor-Critic TD Error

\[
\delta=
r+\gamma V(s')-V(s)
\]

### PPO

\[
L^{CLIP}
=
\min
[
r_tA_t,
\operatorname{clip}(r_t,1-\epsilon,1+\epsilon)A_t
]
\]

---

# Last-Day Revision

If only a few hours remain:

### First

Solve all numerical questions in:

[Additional Numericals & Exam Practice](27-additional-exam-numericals-and-practice.md)

### Then

Revise:

- Q-Learning
- SARSA
- DQN
- Double DQN
- Dueling DQN
- Actor-Critic
- PPO
- PER
- Dyna-Q

### Finally

Go through:

[RL Questions — Complete Solutions](24-solutions-questions-rl.md)

and identify questions you cannot answer without looking at the solution.

---

# PDF Resources

The original instructor resources are available in:

[`pdfs/`](pdfs/)

Important RL resources include:

- `QUESTIONS_rl (2).pdf`
- `RL CSAI Sample questions (3).pdf`
- `Real (1).pdf`
- `Deep-RL-Tutorial (1).pdf`
- `L6 (3).pdf`
- `ML07_ReinforcementLearning.pdf`
- `reinforcement-learning (5) (2) (1).pdf`
- `cs231n_2017_lecture14.pdf`

The PDFs are reference material; **the Markdown notes are organized specifically around the stated Unit 4 and Unit 5 syllabus and exam preparation.**

---

# Exam Strategy

For a numerical:

1. Write the relevant formula.
2. Substitute the given values.
3. Calculate step-by-step.
4. Box the final answer.
5. State what the result means when applicable.

For a theory question:

1. Definition.
2. Core idea.
3. Working/algorithm.
4. Equation.
5. Advantages.
6. Disadvantages.
7. Short comparison/example if appropriate.

For an algorithm question:

```text
Initialize
    ↓
Observe state
    ↓
Select action
    ↓
Receive reward
    ↓
Update value/policy
    ↓
Repeat