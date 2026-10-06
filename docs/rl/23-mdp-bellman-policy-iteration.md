# MDP, Bellman Equations and Policy Iteration

## Source PDFs

- [Reinforcement Learning Lecture](pdfs/reinforcement-learning%20%285%29%20%282%29%20%281%29.pdf)
- [RL CSAI Sample Questions](pdfs/RL%20CSAI%20Sample%20questions%20%283%29.pdf)

---

# 1. Markov Decision Process

A **Markov Decision Process (MDP)** is the mathematical framework used to model sequential decision-making problems in reinforcement learning.

An MDP is represented as:

\[
\boxed{(S,A,P,R,\gamma)}
\]

where:

- \(S\) = set of states
- \(A\) = set of actions
- \(P(s'|s,a)\) = transition probability
- \(R(s,a,s')\) = reward
- \(\gamma\) = discount factor

---

# 2. State

A state represents the current situation of the agent.

Examples:

- location of a robot;
- position of a game character;
- current traffic condition;
- current condition of a machine.

Denote a state by:

\[
s\in S
\]

---

# 3. Action

An action is a decision available to the agent.

For example:

\[
A(s)=
\{\text{up, down, left, right}\}
\]

The agent chooses:

\[
a\in A(s)
\]

---

# 4. Transition Model

The transition model describes the probability of moving from one state to another after taking an action.

\[
\boxed{
P(s'|s,a)
}
\]

For a deterministic environment:

\[
P(s'|s,a)=1
\]

for the state that results from the action.

For a stochastic environment, multiple next states may be possible.

---

# 5. Reward Function

The reward tells the agent how desirable an outcome is.

\[
\boxed{
R(s,a,s')
}
\]

Examples:

- reaching a goal → positive reward;
- collision → negative reward;
- moving toward a target → positive reward;
- taking an unnecessary step → negative reward.

The objective is not necessarily to maximize immediate reward.

The agent tries to maximize **cumulative discounted reward**.

---

# 6. Discount Factor

The discount factor is:

\[
0\leq\gamma\leq1
\]

It determines how much future rewards matter.

The return from time \(t\) is:

\[
\boxed{
G_t=
R_{t+1}
+\gamma R_{t+2}
+\gamma^2R_{t+3}
+\cdots
}
\]

---

## Interpretation

### \(\gamma=0\)

Only immediate rewards matter.

### \(\gamma\approx1\)

Future rewards are important.

Therefore:

\[
\boxed{
\gamma\uparrow
\Rightarrow
\text{greater importance of future rewards}
}
\]

---

# 7. Markov Property

The Markov property states that the future depends on the current state and action, rather than the entire history.

\[
\boxed{
P(s_{t+1}|s_t,a_t,\text{history})
=
P(s_{t+1}|s_t,a_t)
}
\]

In simple terms:

> The current state contains all information required to predict the future.

This is one of the fundamental assumptions behind the MDP formulation.

---

# 8. Policy

A policy tells the agent what action to take in each state.

A deterministic policy is:

\[
\boxed{
\pi(s)=a
}
\]

A stochastic policy gives probabilities:

\[
\boxed{
\pi(a|s)
}
\]

For example:

\[
\pi(\text{up}|s)=0.7
\]

\[
\pi(\text{right}|s)=0.3
\]

---

# 9. State-Value Function

The state-value function under policy \(\pi\) is:

\[
\boxed{
V^\pi(s)
=
E_\pi[G_t|S_t=s]
}
\]

It answers:

> How good is it to be in state \(s\) if I follow policy \(\pi\)?

The supplied lecture defines \(V^\pi(s)\) as the expected return starting from state \(s\) and following policy \(\pi\). :chatgpt-content-reference{index="1"}

---

# 10. Action-Value Function

The action-value function is:

\[
\boxed{
Q^\pi(s,a)
=
E_\pi[G_t|S_t=s,A_t=a]
}
\]

It answers:

> How good is it to take action \(a\) in state \(s\) and then follow policy \(\pi\)?

This is particularly useful for choosing actions.

The lecture notes that an optimal action can be selected using:

\[
\arg\max_aQ^\pi(s,a)
\]

when the relevant Q-values are known. :chatgpt-content-reference{index="2"}

---

# 11. Relationship Between V and Q

For a deterministic policy:

\[
V^\pi(s)=Q^\pi(s,\pi(s))
\]

For a stochastic policy:

\[
\boxed{
V^\pi(s)
=
\sum_a
\pi(a|s)Q^\pi(s,a)
}
\]

Thus:

\[
\boxed{
V = \text{expected value over actions}
}
\]

---

# 12. Bellman Equation

The Bellman equation expresses a value recursively.

The return can be decomposed as:

\[
G_t
=
R_{t+1}
+\gamma G_{t+1}
\]

Taking expectations gives:

\[
\boxed{
V^\pi(s)
=
E_\pi[
R_{t+1}
+\gamma V^\pi(S_{t+1})
|S_t=s
]
}
\]

For a discrete MDP:

\[
\boxed{
V^\pi(s)
=
\sum_a\pi(a|s)
\sum_{s'}
P(s'|s,a)
[
R(s,a,s')
+\gamma V^\pi(s')
]
}
\]

This is the **Bellman expectation equation**.

---

# 13. Bellman Equation — Deterministic Case

If the policy and transition are deterministic:

\[
a=\pi(s)
\]

and:

\[
s'=T(s,a)
\]

then:

\[
\boxed{
V^\pi(s)
=
R(s,\pi(s),s')
+
\gamma V^\pi(s')
}
\]

This is much easier to calculate manually.

---

# 14. Example

Suppose:

\[
R=5
\]

\[
\gamma=0.9
\]

and:

\[
V(s')=10
\]

Then:

\[
V(s)
=
5+0.9(10)
\]

\[
\boxed{
V(s)=14
}
\]

---

# 15. Bellman Expectation Equation vs Bellman Optimality Equation

This distinction is important.

## Bellman Expectation Equation

Used when evaluating a particular policy:

\[
\boxed{
V^\pi(s)
=
E_\pi[
R+\gamma V^\pi(s')
]
}
\]

It answers:

> How good is this particular policy?

---

## Bellman Optimality Equation

Used to find the optimal value:

\[
\boxed{
V^*(s)
=
\max_a
\sum_{s'}
P(s'|s,a)
[
R(s,a,s')
+\gamma V^*(s')
]
}
\]

It answers:

> What is the best achievable value?

---

# 16. Bellman Optimality for Q

The optimal action-value function satisfies:

\[
\boxed{
Q^*(s,a)
=
\sum_{s'}
P(s'|s,a)
[
R(s,a,s')
+
\gamma\max_{a'}Q^*(s',a')
]
}
\]

This equation is fundamental to Q-Learning.

The supplied lecture notes explicitly connect Q-Learning with the Bellman optimality equation. :chatgpt-content-reference{index="3"}

---

# 17. Policy Evaluation

Policy evaluation calculates:

\[
\boxed{
\pi\rightarrow V^\pi
}
\]

That is:

> Given a policy, determine how good each state is under that policy.

The lecture describes policy evaluation as solving the Bellman equations for \(V^\pi\). :chatgpt-content-reference{index="4"}

---

# 18. Iterative Policy Evaluation

Instead of solving all Bellman equations simultaneously, we can repeatedly update the value function.

Start with:

\[
V_0(s)=0
\]

or another arbitrary initialization.

Then:

\[
\boxed{
V_{k+1}(s)
=
\sum_a\pi(a|s)
\sum_{s'}
P(s'|s,a)
[
R+\gamma V_k(s')
]
}
\]

Repeat until:

\[
|V_{k+1}(s)-V_k(s)|
\]

becomes sufficiently small.

---

# 19. Example of Policy Evaluation

Suppose a deterministic policy produces:

\[
s_1
\xrightarrow{a}
s_2
\]

with reward:

\[
R=2
\]

and:

\[
V(s_2)=5
\]

If:

\[
\gamma=0.9
\]

then:

\[
V(s_1)
=
2+0.9(5)
\]

\[
\boxed{
V(s_1)=6.5
}
\]

---

# 20. Policy Improvement

Once we have:

\[
V^\pi
\]

we can improve the policy by choosing the action with the highest expected value.

For each state:

\[
\boxed{
\pi'(s)
=
\arg\max_aQ^\pi(s,a)
}
\]

where:

\[
Q^\pi(s,a)
=
\sum_{s'}
P(s'|s,a)
[
R+\gamma V^\pi(s')
]
\]

The lecture describes policy improvement as:

\[
V^\pi\rightarrow\pi'
\]

and states that the new policy is either strictly better or already optimal. :chatgpt-content-reference{index="5"}

---

# 21. Policy Iteration

Policy iteration repeatedly performs:

\[
\boxed{
\text{Policy Evaluation}
\rightarrow
\text{Policy Improvement}
}
\]

until the policy stops changing.

The complete process is:

```text
Initialize policy π
       |
       ▼
Policy Evaluation
       |
       ▼
Calculate Vπ
       |
       ▼
Policy Improvement
       |
       ▼
New policy π'
       |
       ├── π' = π
       │      |
       │      ▼
       │    STOP
       |
       └── π' ≠ π
              |
              ▼
       Repeat evaluation
```

---

# 22. Policy Iteration Algorithm

```text
Initialize an arbitrary policy π

Repeat:

    1. Evaluate π

       Calculate Vπ

    2. Improve π

       For every state:

       π'(s) =
       argmax_a Qπ(s,a)

    3. If π' = π:

           Stop

       Else:

           π ← π'

           Repeat
```

---

# 23. Why Does Policy Iteration Work?

Policy evaluation determines:

\[
V^\pi
\]

Policy improvement then selects actions that are at least as good as the actions currently selected by \(\pi\).

Thus:

\[
V^{\pi'}(s)
\geq
V^\pi(s)
\]

for the relevant states.

Eventually:

\[
\boxed{
\pi'=\pi
}
\]

which means the policy is stable.

A stable policy under policy improvement is optimal under the usual finite MDP assumptions.

---

# 24. Policy Iteration vs Value Iteration

These are often confused.

## Policy Iteration

Alternates:

\[
\boxed{
\text{Evaluation}
\rightarrow
\text{Improvement}
}
\]

---

## Value Iteration

Uses the Bellman optimality update directly:

\[
\boxed{
V_{k+1}(s)
=
\max_a
\sum_{s'}
P(s'|s,a)
[
R+\gamma V_k(s')
]
}
\]

The supplied lecture explicitly distinguishes the two: policy iteration uses nested evaluation/improvement, while value iteration directly uses the Bellman optimality equation and converges toward \(V^*\). reinforcement-learning (5) (2) …

---

# 25. Policy Iteration vs Value Iteration

| Feature | Policy Iteration | Value Iteration |
|---|---|---|
| Starts with policy | Yes | Not necessary |
| Policy evaluation | Explicit | Implicit |
| Policy improvement | Explicit | Implicit through max |
| Main update | Bellman expectation | Bellman optimality |
| Can require nested iterations | Yes | No |
| Result | Optimal policy | Optimal value, then policy |

---

# 26. Numerical Pattern — Policy Evaluation

Suppose a state has two possible actions.

\[
\pi(a_1|s)=0.5
\]

\[
\pi(a_2|s)=0.5
\]

Suppose:

\[
Q^\pi(s,a_1)=4
\]

and:

\[
Q^\pi(s,a_2)=8
\]

Then:

\[
V^\pi(s)
=
0.5(4)+0.5(8)
\]

\[
\boxed{
V^\pi(s)=6
}
\]

---

# 27. Numerical Pattern — Policy Improvement

Suppose:

\[
Q^\pi(s,a_1)=4
\]

\[
Q^\pi(s,a_2)=8
\]

The improved policy chooses:

\[
\pi'(s)
=
\arg\max_aQ^\pi(s,a)
\]

Therefore:

\[
\boxed{
\pi'(s)=a_2
}
\]

---

# 28. Numerical Pattern — Bellman Optimality

Suppose:

\[
Q(s,a_1)=5
\]

\[
Q(s,a_2)=7
\]

and:

\[
r=2,\qquad\gamma=0.9
\]

Then the optimal target is based on:

\[
\max(5,7)=7
\]

Thus:

\[
V(s)
=
2+0.9(7)
\]

\[
\boxed{
V(s)=8.3
}
\]

---

# 29. Connection to Q-Learning

Q-Learning is essentially a model-free way of approximating the Bellman optimality equation.

Its update is:

\[
\boxed{
Q(s,a)
\leftarrow
Q(s,a)
+
\alpha
[
r+
\gamma\max_{a'}Q(s',a')
-Q(s,a)
]
}
\]

Compare this with the Bellman optimality target:

\[
r+
\gamma\max_{a'}Q(s',a')
\]

The difference is that:

### Dynamic programming

Requires a model:

\[
P(s'|s,a)
\]

### Q-Learning

Learns directly from sampled experience.

---

# 30. MDP → Dynamic Programming → Q-Learning

The progression is:

```text
MDP
 |
 +-- Known model
 |      |
 |      ▼
 |  Dynamic Programming
 |      |
 |      +-- Policy Iteration
 |      |
 |      +-- Value Iteration
 |
 +-- Unknown model
        |
        ▼
   Model-Free RL
        |
        +-- Q-Learning
        |
        +-- SARSA
```

---

# 31. Exam Question Pattern

If the question says:

> "Evaluate the current policy"

Use:

\[
\boxed{\text{Bellman expectation equation}}
\]

---

If the question says:

> "Improve the policy"

Use:

\[
\boxed{
\pi'(s)=\arg\max_aQ^\pi(s,a)
}
\]

---

If the question says:

> "Find the optimal value"

Use:

\[
\boxed{\text{Bellman optimality equation}}
\]

---

If the question says:

> "Find the optimal policy"

Use:

\[
\boxed{
\pi^*(s)=\arg\max_aQ^*(s,a)
}
\]

---

# 32. High-Priority Formulas

## Return

\[
\boxed{
G_t=
R_{t+1}
+\gamma R_{t+2}
+\gamma^2R_{t+3}
+\cdots
}
\]

## Value function

\[
\boxed{
V^\pi(s)=E_\pi[G_t|S_t=s]
}
\]

## Action-value function

\[
\boxed{
Q^\pi(s,a)=E_\pi[G_t|S_t=s,A_t=a]
}
\]

## Bellman expectation equation

\[
\boxed{
V^\pi(s)
=
\sum_a\pi(a|s)
\sum_{s'}P(s'|s,a)
[
R+\gamma V^\pi(s')
]
}
\]

## Bellman optimality equation

\[
\boxed{
V^*(s)
=
\max_a
\sum_{s'}P(s'|s,a)
[
R+\gamma V^*(s')
]
}
\]

## Policy improvement

\[
\boxed{
\pi'(s)
=
\arg\max_aQ^\pi(s,a)
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
-Q(s,a)]
}
\]

---

# 33. One-Minute Revision

### MDP

\[
\boxed{(S,A,P,R,\gamma)}
\]

### Policy

\[
\boxed{\pi(a|s)}
\]

### Value

\[
\boxed{V^\pi(s)}
\]

### Q-value

\[
\boxed{Q^\pi(s,a)}
\]

### Policy Evaluation

\[
\boxed{\pi\rightarrow V^\pi}
\]

### Policy Improvement

\[
\boxed{V^\pi\rightarrow\pi'}
\]

### Policy Iteration

\[
\boxed{
\text{Evaluate}\rightarrow\text{Improve}\rightarrow\text{Repeat}
}
\]

### Value Iteration

\[
\boxed{
\text{Bellman optimality update repeatedly}
}
\]

### Q-Learning

\[
\boxed{
\text{Sample-based Bellman optimality update}
}
