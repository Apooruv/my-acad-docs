# Markov Decision Process (MDP)

## 1. What is Reinforcement Learning?

Reinforcement Learning (RL) is a learning framework in which an **agent interacts with an environment** and learns how to choose actions to maximize cumulative reward.

The interaction is:

```text
        Action
Agent ───────────> Environment
  ↑                    │
  │                    │
  └── Reward + State ──┘
```

At time step `t`:

1. The agent observes the current state `s_t`.
2. The agent selects an action `a_t`.
3. The environment produces a reward `r_{t+1}`.
4. The environment transitions to `s_{t+1}`.
5. The process repeats.

---

## 2. Markov Decision Process

An **MDP** is the mathematical framework used to represent a sequential decision-making problem.

An MDP is generally represented by:

\[
(S,A,P,R,\gamma)
\]

where:

| Symbol | Meaning |
|---|---|
| \(S\) | Set of states |
| \(A\) | Set of actions |
| \(P(s'|s,a)\) | Transition probability |
| \(R(s,a,s')\) | Reward |
| \(\gamma\) | Discount factor |

Some formulations also explicitly specify the initial-state distribution.

---

## 3. State

A **state** represents the information about the environment required for making a decision.

Example: Grid World

```text
+---+---+---+
|   |   |   |
+---+---+---+
|   | A |   |
+---+---+---+
|   |   | G |
+---+---+---+
```

If the agent is at row 2, column 2:

\[
s=(2,2)
\]

The set of all possible positions forms the state space \(S\).

---

## 4. Action

An action is a decision available to the agent in a state.

For a grid-world problem:

\[
A=\{Up,Down,Left,Right\}
\]

The available actions may depend on the state.

---

## 5. Transition Model

The transition model specifies the probability of reaching a new state after taking an action.

\[
P(s'|s,a)
\]

For example:

\[
P((1,2)|(1,1),Up)=0.8
\]

means that if the agent is in state `(1,1)` and chooses `Up`, there is an 80% probability of reaching `(1,2)`.

### Deterministic Environment

If an action always produces the same next state:

\[
P(s'|s,a)=1
\]

for that particular transition.

### Stochastic Environment

If an action can result in multiple next states:

\[
\sum_{s'}P(s'|s,a)=1
\]

---

## 6. Reward

A reward tells the agent how desirable the immediate outcome is.

Examples:

- Reaching the goal: `+10`
- Collision: `-10`
- Normal movement: `-1`
- Winning a game: `+1`
- Losing a game: `-1`

The reward should represent **what the agent should achieve**, rather than prescribing exactly how it should achieve it.

---

## 7. Policy

A policy specifies how the agent chooses actions.

### Deterministic Policy

A deterministic policy maps each state to exactly one action:

\[
\pi:S\rightarrow A
\]

Example:

\[
\pi(s)=Right
\]

### Stochastic Policy

A stochastic policy gives a probability distribution over actions:

\[
\pi(a|s)
\]

Example:

\[
\pi(Up|s)=0.5
\]

\[
\pi(Right|s)=0.5
\]

The probabilities must satisfy:

\[
\sum_a\pi(a|s)=1
\]

---

## 8. Markov Property

The Markov property means that the future depends only on the **current state and action**, not on the complete history.

Formally:

\[
P(s_{t+1}|s_t,a_t,s_{t-1},a_{t-1},\ldots)
=
P(s_{t+1}|s_t,a_t)
\]

In simple terms:

> The current state contains all the information required to predict the future.

This assumption is fundamental to MDPs.

---

## 9. Complete MDP Example

Consider a grid world.

### States

\[
S=\{A,B,C,G\}
\]

where `G` is the terminal goal.

### Actions

\[
A=\{Left,Right\}
\]

Suppose:

- From `A`, `Right` leads to `B`
- From `B`, `Right` leads to `C`
- From `C`, `Right` leads to `G`
- Every movement gives `-1`
- Reaching `G` gives `+10`

The agent must learn a policy that maximizes cumulative reward.

---

## 10. Objective of RL

The objective is to find an optimal policy:

\[
\pi^*
\]

that maximizes expected cumulative discounted reward.

The cumulative discounted reward is:

\[
G_t =
R_{t+1}
+\gamma R_{t+2}
+\gamma^2R_{t+3}
+\cdots
\]

where:

\[
0\leq\gamma\leq1
\]

The meaning of \(\gamma\) is covered in the next section.

---

## 11. MDP vs Reinforcement Learning

An important distinction:

### MDP

An MDP describes the environment mathematically.

It assumes that the transition and reward model can be specified.

### Reinforcement Learning

RL is the learning problem where the agent generally does **not know the environment model in advance**.

The agent learns from interaction.

```text
MDP
 │
 ├── States
 ├── Actions
 ├── Transitions
 └── Rewards
       ↓
RL agent learns how to act
       ↓
Optimal policy
```

---

## 12. Exam Points

Remember:

1. MDP models sequential decision making.
2. The main components are states, actions, transition probabilities and rewards.
3. A policy determines how actions are selected.
4. The Markov property means the current state summarizes relevant history.
5. RL attempts to learn a policy that maximizes cumulative reward.
6. The transition model describes how the environment changes.
7. The reward function describes the immediate desirability of an outcome.

### One-line definition

> An MDP is a mathematical framework for sequential decision-making consisting of states, actions, transition dynamics and rewards, satisfying the Markov property.



