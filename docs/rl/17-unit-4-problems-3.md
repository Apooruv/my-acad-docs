# Unit 4 — Problems 3

## Source PDFs

- [RL CSAI Sample Questions](pdfs/RL%20CSAI%20Sample%20questions%20%283%29.pdf)
- [RL Question Bank](pdfs/QUESTIONS%20_rl%20%282%29.pdf)

---

# Q15. Policy Evaluation in Grid World Scenario

> Consider a simplified 3x3 grid world where an agent can move in four directions: up, down, left, and right. The agent starts in the top left corner (0,0) and aims to reach the bottom right corner (2,2) with the least number of steps. All actions have a deterministic outcome. The agent receives a reward of -1 for each step and +10 for reaching the goal. Assume we have a policy π that chooses each action with equal probability. Calculate the expected return from each state under policy π using a discount factor (γ) of 0.9. How would the expected return change if the policy is updated to always choose the action that moves directly toward the goal?

## Assumption

The question does not explicitly specify the behavior when an action tries to leave the grid.

For the calculation below, assume:

> An action that hits a boundary leaves the agent in the same state and still gives the step reward of \(-1\).

The goal state \((2,2)\) is terminal.

---

## Bellman expectation equation

Since the policy chooses each of the four actions with probability:

\[
\frac14
\]

the value of a state is:

\[
V^\pi(s)
=
\sum_a\pi(a|s)
\left[
R(s,a)+\gamma V^\pi(s')
\right]
\]

Therefore:

\[
V^\pi(s)
=
\frac14
\sum_a
[-1+0.9V^\pi(s')]
\]

for non-terminal states.

---

## State notation

Represent the grid as:

\[
\begin{matrix}
A&B&C\\
D&E&F\\
G&H&T
\end{matrix}
\]

where:

\[
T=(2,2)
\]

is the terminal goal.

---

## Bellman equations

For \(A=(0,0)\):

\[
A=
\frac14[
-1+0.9A
-1+0.9D
-1+0.9A
-1+0.9B
]
\]

For \(B=(0,1)\):

\[
B=
\frac14[
-1+0.9B
-1+0.9E
-1+0.9A
-1+0.9C
]
\]

For \(C=(0,2)\):

\[
C=
\frac14[
-1+0.9C
-1+0.9F
-1+0.9B
-1+0.9C
]
\]

For \(D=(1,0)\):

\[
D=
\frac14[
-1+0.9A
-1+0.9G
-1+0.9D
-1+0.9E
]
\]

For \(E=(1,1)\):

\[
E=
\frac14[
-1+0.9B
-1+0.9H
-1+0.9D
-1+0.9F
]
\]

For \(F=(1,2)\):

\[
F=
\frac14[
-1+0.9C
-1+0.9T
-1+0.9E
-1+0.9F
]
\]

For \(G=(2,0)\):

\[
G=
\frac14[
-1+0.9D
-1+0.9G
-1+0.9G
-1+0.9H
]
\]

For \(H=(2,1)\):

\[
H=
\frac14[
-1+0.9E
-1+0.9H
-1+0.9G
-1+0.9T
]
\]

and:

\[
T=0
\]

for the terminal state.

Solving these simultaneous Bellman equations gives approximately:

| State | Expected value |
|---|---:|
| \((0,0)\) | **2.039** |
| \((0,1)\) | **2.492** |
| \((0,2)\) | **3.116** |
| \((1,0)\) | **2.492** |
| \((1,1)\) | **3.428** |
| \((1,2)\) | **5.126** |
| \((2,0)\) | **3.116** |
| \((2,1)\) | **5.126** |
| \((2,2)\) | **0** |

Therefore, from the starting state:

\[
\boxed{V^\pi(0,0)\approx2.039}
\]

---

## Improved policy

Now suppose the policy always chooses an action that moves toward the goal.

The value can be calculated backward from the goal.

### One step from goal

The final transition receives:

\[
+10
\]

so:

\[
V_1=10
\]

### Two steps from goal

\[
V_2=-1+0.9(10)
\]

\[
\boxed{V_2=8}
\]

### Three steps

\[
V_3=-1+0.9(8)
\]

\[
\boxed{V_3=6.2}
\]

### Four steps

\[
V_4=-1+0.9(6.2)
\]

\[
\boxed{V_4=4.58}
\]

The start state is four steps from the goal, so:

\[
\boxed{V(0,0)=4.58}
\]

Thus the expected return improves from approximately:

\[
2.039
\]

to:

\[
4.58
\]

because the improved policy reaches the goal more directly.

---

# Q16. Bellman Equation for Value Estimation

> In the same 3x3 grid world, consider a state (1,1) with possible actions leading to states (1,0), (1,2), (0,1), and (2,1). The immediate rewards for moving to these states are -1, and the discount factor γ is 0.9. Assume the current estimated values of these states are 2.0, 1.0, 0.5, and 3.0, respectively. Use the Bellman equation to calculate the updated value of state (1,1) if the agent follows a greedy policy that always chooses the action leading to the state with the highest value. Discuss the impact of changing the discount factor to 0.99 on the value of state (1,1).

## Step 1 — Identify the maximum next-state value

The values are:

\[
2.0,\quad1.0,\quad0.5,\quad3.0
\]

Therefore:

\[
\max V(s')=3.0
\]

The greedy policy selects the action leading to this state.

---

## Step 2 — Bellman equation

For a deterministic greedy transition:

\[
V(s)=R+\gamma V(s')
\]

Therefore:

\[
V(1,1)
=
-1+0.9(3.0)
\]

\[
=-1+2.7
\]

\[
\boxed{V(1,1)=1.7}
\]

---

## Step 3 — Change γ to 0.99

\[
V(1,1)
=
-1+0.99(3.0)
\]

\[
=-1+2.97
\]

\[
\boxed{V(1,1)=1.97}
\]

---

## Interpretation

Increasing:

\[
\gamma:0.9\rightarrow0.99
\]

increases the value because the future value of the next state receives more weight.

\[
\boxed{1.7\rightarrow1.97}
\]

Therefore:

> A larger discount factor makes the agent more concerned with future rewards.

---

# Q17. Q-Learning Update Scenario

> An agent is learning to play a simple game using Q-learning. The agent is in state S and chooses action A, leading to state S'. The reward received is R = 2. The learning rate α is 0.1, and the discount factor γ is 0.95. The highest Q-value for the next state S' is 5. If the current Q-value Q(S,A) is 3, calculate the updated Q-value after taking action A and receiving the reward. Explain how the Q-value would change if the reward for taking action A was increased to R = 5.

## Q-learning equation

\[
Q(S,A)
\leftarrow
Q(S,A)+
\alpha
[
R+\gamma\max_{a'}Q(S',a')
-Q(S,A)
]
\]

Given:

\[
Q(S,A)=3
\]

\[
R=2
\]

\[
\alpha=0.1
\]

\[
\gamma=0.95
\]

\[
\max Q(S',a')=5
\]

---

## Case 1 — Reward = 2

Substitute:

\[
Q_{\text{new}}
=
3+
0.1[
2+0.95(5)-3
]
\]

Calculate:

\[
0.95(5)=4.75
\]

Therefore:

\[
Q_{\text{new}}
=
3+
0.1[2+4.75-3]
\]

\[
=
3+0.1(3.75)
\]

\[
=
3+0.375
\]

\[
\boxed{Q_{\text{new}}=3.375}
\]

---

## Case 2 — Reward = 5

Now:

\[
R=5
\]

Therefore:

\[
Q_{\text{new}}
=
3+
0.1[
5+0.95(5)-3
]
\]

\[
=
3+
0.1[
5+4.75-3
]
\]

\[
=
3+0.1(6.75)
\]

\[
\boxed{Q_{\text{new}}=3.675}
\]

---

## Comparison

| Reward | Updated Q-value |
|---:|---:|
| \(R=2\) | **3.375** |
| \(R=5\) | **3.675** |

Increasing the immediate reward increases the Q-value because the target becomes larger.

---

# Quick Formula Sheet

## Discounted Return

\[
\boxed{
G_t=
R_{t+1}
+\gamma R_{t+2}
+\gamma^2R_{t+3}
+\cdots
}
\]

## Bellman Value Equation

\[
\boxed{
V(s)=R+\gamma V(s')
}
\]

## Greedy Bellman Equation

\[
\boxed{
V(s)=R+\gamma\max_aV(s')
}
\]

## Bellman Expectation Equation

\[
\boxed{
V^\pi(s)
=
\sum_a
\pi(a|s)
\left[
R(s,a)+\gamma V^\pi(s')
\right]
}
\]

## Q-Learning

\[
\boxed{
Q(s,a)\leftarrow
Q(s,a)+
\alpha[
R+\gamma\max_{a'}Q(s',a')
-Q(s,a)]
}
\]

## SARSA

\[
\boxed{
Q(s,a)\leftarrow
Q(s,a)+
\alpha[
R+\gamma Q(s',a')
-Q(s,a)]
}
\]

## Optimal Action

\[
\boxed{
a^*=\arg\max_aQ(s,a)
}
\]

