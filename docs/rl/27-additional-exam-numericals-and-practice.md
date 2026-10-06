# Additional Numericals & Exam Practice

## Purpose

This file contains:

1. Remaining worked numerical examples found in the supplied RL resources.
2. Additional numerical questions that are highly suitable for exam practice based on the syllabus.

> **Important:** Questions in the "Additional Exam Practice" section are newly constructed practice questions. They are not claimed to be questions from the supplied PDFs.

---

# Part A — Remaining Numericals from the Supplied PDFs

---

# Q1. Double DQN — Numerical from Deep RL Tutorial

> Given \(r=1\), \(\gamma=0.9\), and two actions \(a_1,a_2\) at the next state:
>
> Online network:
>
> \[
> Q_\theta(a_1)=3.0,\qquad Q_\theta(a_2)=2.0
> \]
>
> Target network:
>
> \[
> Q_{\theta^-}(a_1)=1.0,\qquad Q_{\theta^-}(a_2)=2.5
> \]
>
> Calculate the target using Vanilla DQN and Double DQN.

## Vanilla DQN

Vanilla DQN uses the target network for both selecting and evaluating the maximum action:

\[
y_{\text{DQN}}
=
r+\gamma
\max_a Q_{\theta^-}(s',a)
\]

The target-network values are:

\[
1.0,\quad2.5
\]

Therefore:

\[
\max(1.0,2.5)=2.5
\]

Hence:

\[
y_{\text{DQN}}
=
1+0.9(2.5)
\]

\[
=1+2.25
\]

\[
\boxed{y_{\text{DQN}}=3.25}
\]

---

## Double DQN

Double DQN separates action selection and evaluation.

### Step 1 — Select action using online network

Online values:

\[
Q_\theta(a_1)=3.0
\]

\[
Q_\theta(a_2)=2.0
\]

Therefore:

\[
a^*
=
\arg\max_aQ_\theta(s',a)
\]

\[
\boxed{a^*=a_1}
\]

### Step 2 — Evaluate selected action using target network

The target network gives:

\[
Q_{\theta^-}(a_1)=1.0
\]

Therefore:

\[
y_{\text{DDQN}}
=
r+\gamma Q_{\theta^-}(s',a^*)
\]

\[
=
1+0.9(1)
\]

\[
\boxed{y_{\text{DDQN}}=1.9}
\]

---

## Comparison

\[
\boxed{
y_{\text{DQN}}=3.25
}
\]

\[
\boxed{
y_{\text{DDQN}}=1.9
}
\]

### Exam takeaway

\[
\boxed{\text{DQN: target selects + evaluates}}
\]

\[
\boxed{\text{Double DQN: online selects, target evaluates}}
\]

Double DQN reduces the tendency of the maximum operation to exploit overestimated Q-values.

---

# Q2. Dueling DQN — Numerical from Deep RL Tutorial

> Given:
>
> \[
> V(s)=5
> \]
>
> and advantage values:
>
> \[
> A(s,a_1)=3,\quad
> A(s,a_2)=1,\quad
> A(s,a_3)=2
> \]
>
> Calculate the Q-value of every action.

## Formula

The Dueling DQN combination is:

\[
Q(s,a)
=
V(s)
+
\left(
A(s,a)-\frac{1}{|\mathcal A|}
\sum_{a'}A(s,a')
\right)
\]

---

## Step 1 — Calculate mean advantage

\[
\operatorname{mean}(A)
=
\frac{3+1+2}{3}
\]

\[
=
\frac63
\]

\[
\boxed{\operatorname{mean}(A)=2}
\]

---

## Step 2 — Calculate \(Q(a_1)\)

\[
Q(a_1)
=
5+(3-2)
\]

\[
\boxed{Q(a_1)=6}
\]

---

## Step 3 — Calculate \(Q(a_2)\)

\[
Q(a_2)
=
5+(1-2)
\]

\[
\boxed{Q(a_2)=4}
\]

---

## Step 4 — Calculate \(Q(a_3)\)

\[
Q(a_3)
=
5+(2-2)
\]

\[
\boxed{Q(a_3)=5}
\]

---

## Final answer

| Action | \(A(s,a)\) | \(Q(s,a)\) |
|---|---:|---:|
| \(a_1\) | 3 | **6** |
| \(a_2\) | 1 | **4** |
| \(a_3\) | 2 | **5** |

Therefore:

\[
\boxed{a_1\text{ is the best action}}
\]

because:

\[
\max Q(s,a)=6
\]

---

# Q3. Actor-Critic — Numerical from Deep RL Tutorial

> The Critic estimates:
>
> \[
> V(s)=2.0
> \]
>
> and:
>
> \[
> V(s')=3.0
> \]
>
> The received reward is:
>
> \[
> r=1.0
> \]
>
> Given:
>
> \[
> \gamma=0.9,\qquad\alpha=0.1
> \]
>
> Calculate the TD error and update the Critic.

## Step 1 — TD error

The TD error is:

\[
\delta
=
r+\gamma V(s')-V(s)
\]

Substitute:

\[
\delta
=
1+0.9(3)-2
\]

\[
=
1+2.7-2
\]

\[
\boxed{\delta=1.7}
\]

---

## Step 2 — Update Critic

The TD update is:

\[
V(s)
\leftarrow
V(s)+\alpha\delta
\]

Therefore:

\[
V(s)
=
2+0.1(1.7)
\]

\[
=
2+0.17
\]

\[
\boxed{V_{\text{new}}(s)=2.17}
\]

---

## Step 3 — Actor interpretation

Since:

\[
\delta=1.7>0
\]

the selected action performed better than expected.

Therefore the Actor should increase the probability of selecting that action.

The policy-gradient contribution is:

\[
\nabla_\theta J
\propto
\delta
\nabla_\theta\log\pi_\theta(a|s)
\]

Thus:

\[
\boxed{
\delta>0
\Rightarrow
\text{reinforce the action}
}
\]

---

# Part B — Additional Exam Practice

> The following questions are newly constructed exam-oriented problems based on the stated syllabus. They are intended to cover numerical patterns that can reasonably be asked.

---

# Q4. MDP — Calculate Discounted Return

> An agent receives rewards:
>
> \[
> 4,-2,6
> \]
>
> over three successive transitions. If:
>
> \[
> \gamma=0.8
> \]
>
> calculate the discounted return from the initial state.

## Solution

The discounted return is:

\[
G_0
=
R_1+\gamma R_2+\gamma^2R_3
\]

Substitute:

\[
G_0
=
4+0.8(-2)+0.8^2(6)
\]

\[
=
4-1.6+0.64(6)
\]

\[
=
4-1.6+3.84
\]

\[
\boxed{G_0=6.24}
\]

---

# Q5. Bellman Equation — State Value

> A state \(s\) has two possible actions. Under the current policy:
>
> \[
> \pi(a_1|s)=0.6
> \]
>
> \[
> \pi(a_2|s)=0.4
> \]
>
> For \(a_1\):
>
> \[
> r=2,\qquad V(s'_1)=5
> \]
>
> For \(a_2\):
>
> \[
> r=1,\qquad V(s'_2)=3
> \]
>
> Given:
>
> \[
> \gamma=0.9
> \]
>
> calculate \(V^\pi(s)\).

## Bellman expectation equation

\[
V^\pi(s)
=
\sum_a
\pi(a|s)
[
r+\gamma V(s')
]
\]

Therefore:

\[
V^\pi(s)
=
0.6[2+0.9(5)]
+
0.4[1+0.9(3)]
\]

First action:

\[
2+4.5=6.5
\]

Second action:

\[
1+2.7=3.7
\]

Therefore:

\[
V^\pi(s)
=
0.6(6.5)+0.4(3.7)
\]

\[
=
3.9+1.48
\]

\[
\boxed{V^\pi(s)=5.38}
\]

---

# Q6. Bellman Optimality Equation

> A state has three possible actions. Their immediate rewards and next-state values are:
>
> | Action | Reward | Next-state value |
> |---|---:|---:|
> | \(a_1\) | 2 | 4 |
> | \(a_2\) | 5 | 3 |
> | \(a_3\) | 1 | 7 |
>
> Given \(\gamma=0.9\), calculate the optimal value of the state.

## Solution

Use:

\[
V^*(s)
=
\max_a
[
r+\gamma V(s')
]
\]

### Action \(a_1\)

\[
2+0.9(4)=5.6
\]

### Action \(a_2\)

\[
5+0.9(3)=7.7
\]

### Action \(a_3\)

\[
1+0.9(7)=7.3
\]

Therefore:

\[
V^*(s)
=
\max(5.6,7.7,7.3)
\]

\[
\boxed{V^*(s)=7.7}
\]

The optimal action is:

\[
\boxed{a_2}
\]

---

# Q7. Policy Evaluation — One Iteration

> A policy always selects action \(a\). For a particular state:
>
> \[
> V_0(s)=2
> \]
>
> The action gives:
>
> \[
> r=-1
> \]
>
> and transitions to a state whose current value is:
>
> \[
> V_0(s')=6
> \]
>
> Given:
>
> \[
> \gamma=0.9
> \]
>
> perform one policy-evaluation update.

## Solution

The Bellman update is:

\[
V_{k+1}(s)
=
r+\gamma V_k(s')
\]

Therefore:

\[
V_1(s)
=
-1+0.9(6)
\]

\[
=-1+5.4
\]

\[
\boxed{V_1(s)=4.4}
\]

---

# Q8. Policy Iteration — Policy Improvement

> A state has two actions with estimated values:
>
> \[
> Q(s,a_1)=4.2
> \]
>
> \[
> Q(s,a_2)=5.7
> \]
>
> The current policy chooses \(a_1\). Perform the policy-improvement step.

## Solution

Policy improvement chooses:

\[
\pi_{\text{new}}(s)
=
\arg\max_aQ(s,a)
\]

Since:

\[
Q(s,a_2)=5.7>4.2=Q(s,a_1)
\]

the improved policy is:

\[
\boxed{\pi_{\text{new}}(s)=a_2}
\]

---

# Q9. Direct Utility Estimation

> A state \(s\) is visited in three episodes. The observed returns are:
>
> \[
> 8,\;4,\;10
> \]
>
> Estimate \(U(s)\) using Direct Utility Estimation.

## Solution

Direct Utility Estimation uses the average observed utility:

\[
U(s)
=
\frac{1}{N}
\sum_{i=1}^{N}G_i
\]

Therefore:

\[
U(s)
=
\frac{8+4+10}{3}
\]

\[
=
\frac{22}{3}
\]

\[
\boxed{U(s)\approx7.33}
\]

---

# Q10. Temporal Difference Learning

> An agent has:
>
> \[
> V(s)=4
> \]
>
> \[
> V(s')=7
> \]
>
> It receives:
>
> \[
> r=2
> \]
>
> Given:
>
> \[
> \gamma=0.9,\qquad\alpha=0.2
> \]
>
> calculate the TD error and updated value.

## Step 1 — TD error

\[
\delta
=
r+\gamma V(s')-V(s)
\]

\[
=
2+0.9(7)-4
\]

\[
=
2+6.3-4
\]

\[
\boxed{\delta=4.3}
\]

## Step 2 — Update

\[
V_{\text{new}}(s)
=
V(s)+\alpha\delta
\]

\[
=
4+0.2(4.3)
\]

\[
=
4+0.86
\]

\[
\boxed{V_{\text{new}}(s)=4.86}
\]

---

# Q11. Monte Carlo Return

> An episode produces the reward sequence:
>
> \[
> 2,3,-1,5
> \]
>
> Starting from the first state and using:
>
> \[
> \gamma=0.9
> \]
>
> calculate the Monte Carlo return.

## Solution

\[
G_0
=
2+0.9(3)+0.9^2(-1)+0.9^3(5)
\]

Calculate each term:

\[
0.9(3)=2.7
\]

\[
0.9^2(-1)=-0.81
\]

\[
0.9^3(5)=0.729(5)=3.645
\]

Therefore:

\[
G_0
=
2+2.7-0.81+3.645
\]

\[
\boxed{G_0=7.535}
\]

---

# Q12. Q-Learning Update

> An agent has:
>
> \[
> Q(s,a)=4
> \]
>
> It receives:
>
> \[
> r=-2
> \]
>
> The maximum Q-value in the next state is:
>
> \[
> \max_{a'}Q(s',a')=8
> \]
>
> Given:
>
> \[
> \alpha=0.2,\qquad\gamma=0.9
> \]
>
> calculate the updated Q-value.

## Solution

\[
Q_{\text{new}}
=
Q+
\alpha[
r+\gamma\max Q'-Q
]
\]

Substitute:

\[
Q_{\text{new}}
=
4+
0.2[
-2+0.9(8)-4
]
\]

\[
=
4+
0.2[-2+7.2-4]
\]

\[
=
4+0.2(1.2)
\]

\[
\boxed{Q_{\text{new}}=4.24}
\]

---

# Q13. SARSA Update

> An agent has:
>
> \[
> Q(s,a)=4
> \]
>
> It receives reward:
>
> \[
> r=-2
> \]
>
> The next action actually selected by the policy has:
>
> \[
> Q(s',a')=5
> \]
>
> Given:
>
> \[
> \alpha=0.2,\qquad\gamma=0.9
> \]
>
> calculate the SARSA update.

## Solution

SARSA uses the value of the **actual next action**:

\[
Q_{\text{new}}
=
Q+
\alpha[
r+\gamma Q(s',a')-Q
]
\]

Substitute:

\[
Q_{\text{new}}
=
4+
0.2[
-2+0.9(5)-4
]
\]

\[
=
4+
0.2[-2+4.5-4]
\]

\[
=
4+0.2(-1.5)
\]

\[
\boxed{Q_{\text{new}}=3.7}
\]

---

## Q-Learning vs SARSA

If instead:

\[
\max_{a'}Q(s',a')=8
\]

Q-Learning would calculate:

\[
4+
0.2[-2+0.9(8)-4]
\]

\[
\boxed{Q_{\text{Q-learning}}=4.24}
\]

whereas SARSA gives:

\[
\boxed{Q_{\text{SARSA}}=3.7}
\]

### Key difference

\[
\boxed{
\text{Q-Learning uses max next Q}
}
\]

\[
\boxed{
\text{SARSA uses actual next action Q}
}
\]

---

# Q14. DQN Target Calculation

> A DQN receives:
>
> \[
> r=3
> \]
>
> \[
> \gamma=0.95
> \]
>
> The target network predicts:
>
> \[
> Q(s',a_1)=4
> \]
>
> \[
> Q(s',a_2)=7
> \]
>
> \[
> Q(s',a_3)=5
> \]
>
> Calculate the DQN target.

## Solution

DQN target:

\[
y=
r+\gamma\max_{a'}Q_{\text{target}}(s',a')
\]

The maximum is:

\[
\max(4,7,5)=7
\]

Therefore:

\[
y=
3+0.95(7)
\]

\[
=
3+6.65
\]

\[
\boxed{y=9.65}
\]

---

# Q15. DQN Parameter Update

> Suppose:
>
> \[
> Q_{\text{current}}=5
> \]
>
> and the DQN target is:
>
> \[
> y=8
> \]
>
> with learning rate:
>
> \[
> \alpha=0.1
> \]
>
> Calculate the tabular-style Q update.

## Solution

\[
Q_{\text{new}}
=
Q_{\text{current}}
+
\alpha(y-Q_{\text{current}})
\]

Therefore:

\[
Q_{\text{new}}
=
5+0.1(8-5)
\]

\[
=
5+0.3
\]

\[
\boxed{Q_{\text{new}}=5.3}
\]

---

# Q16. Double DQN

> At the next state, the online network gives:
>
> \[
> [2,6,4]
> \]
>
> for actions \(a_1,a_2,a_3\).
>
> The target network gives:
>
> \[
> [5,3,7]
> \]
>
> The current reward is:
>
> \[
> r=2
> \]
>
> and:
>
> \[
> \gamma=0.9
> \]
>
> Calculate the Double-DQN target.

## Step 1 — Select using online network

Online:

\[
[2,6,4]
\]

Therefore:

\[
\boxed{a^*=a_2}
\]

because:

\[
6=\max(2,6,4)
\]

## Step 2 — Evaluate using target network

Target value for \(a_2\):

\[
Q_{\text{target}}(a_2)=3
\]

Therefore:

\[
y=
2+0.9(3)
\]

\[
=2+2.7
\]

\[
\boxed{y=4.7}
\]

---

# Q17. Dueling DQN

> A Dueling DQN has:
>
> \[
> V(s)=8
> \]
>
> and:
>
> \[
> A=[2,-1,3,0]
> \]
>
> Calculate the Q-value of every action.

## Step 1 — Mean advantage

\[
\bar A
=
\frac{2+(-1)+3+0}{4}
\]

\[
=
\frac44
\]

\[
\boxed{\bar A=1}
\]

## Step 2 — Calculate Q-values

### \(a_1\)

\[
Q_1=8+(2-1)
\]

\[
\boxed{Q_1=9}
\]

### \(a_2\)

\[
Q_2=8+(-1-1)
\]

\[
\boxed{Q_2=6}
\]

### \(a_3\)

\[
Q_3=8+(3-1)
\]

\[
\boxed{Q_3=10}
\]

### \(a_4\)

\[
Q_4=8+(0-1)
\]

\[
\boxed{Q_4=7}
\]

Therefore:

\[
\boxed{
Q=[9,6,10,7]
}
\]

Best action:

\[
\boxed{a_3}
\]

---

# Q18. Actor-Critic Update

> The Critic estimates:
>
> \[
> V(s)=4
> \]
>
> \[
> V(s')=6
> \]
>
> The reward is:
>
> \[
> r=-1
> \]
>
> Given:
>
> \[
> \gamma=0.9
> \]
>
> calculate the TD error. State whether the Actor should reinforce or discourage the selected action.

## Solution

\[
\delta
=
r+\gamma V(s')-V(s)
\]

\[
=
-1+0.9(6)-4
\]

\[
=
-1+5.4-4
\]

\[
\boxed{\delta=0.4}
\]

Since:

\[
\delta>0
\]

the outcome was slightly better than the Critic expected.

Therefore:

\[
\boxed{\text{Actor reinforces the selected action}}
\]

---

# Q19. Actor-Critic Critic Update

> Given:
>
> \[
> V(s)=4
> \]
>
> \[
> V(s')=6
> \]
>
> \[
> r=-2
> \]
>
> \[
> \gamma=0.9
> \]
>
> \[
> \alpha=0.1
> \]
>
> calculate the TD error and updated \(V(s)\).

## TD error

\[
\delta
=
-2+0.9(6)-4
\]

\[
=
-2+5.4-4
\]

\[
\boxed{\delta=-0.6}
\]

## Critic update

\[
V_{\text{new}}(s)
=
4+0.1(-0.6)
\]

\[
=
4-0.06
\]

\[
\boxed{V_{\text{new}}(s)=3.94}
\]

Because:

\[
\delta<0
\]

the selected action performed worse than expected.

---

# Q20. Proximal Policy Optimization — Clipped Objective

> In PPO, suppose:
>
> \[
> \frac{\pi_\theta(a|s)}
> {\pi_{\theta_{\text{old}}}(a|s)}
> =1.2
> \]
>
> and:
>
> \[
> A=2
> \]
>
> with:
>
> \[
> \epsilon=0.2
> \]
>
> Calculate the clipped PPO objective contribution.

## PPO objective

\[
L^{CLIP}
=
\min
\left(
r_tA_t,
\operatorname{clip}(r_t,1-\epsilon,1+\epsilon)A_t
\right)
\]

Given:

\[
r_t=1.2
\]

\[
A_t=2
\]

\[
\epsilon=0.2
\]

The clipping range is:

\[
[0.8,1.2]
\]

Since:

\[
r_t=1.2
\]

it lies exactly at the upper boundary.

Therefore:

\[
\operatorname{clip}(1.2,0.8,1.2)=1.2
\]

First term:

\[
1.2(2)=2.4
\]

Clipped term:

\[
1.2(2)=2.4
\]

Therefore:

\[
\boxed{L^{CLIP}=2.4}
\]

---

# Q21. PPO — Clipping an Excessive Update

> Suppose:
>
> \[
> r_t=1.5
> \]
>
> \[
> A_t=2
> \]
>
> and:
>
> \[
> \epsilon=0.2
> \]
>
> Calculate the unclipped and clipped terms and determine the PPO objective.

## Step 1 — Unclipped term

\[
r_tA_t
=
1.5(2)
\]

\[
=3
\]

## Step 2 — Clip ratio

The allowed range is:

\[
[0.8,1.2]
\]

Since:

\[
1.5>1.2
\]

the ratio is clipped to:

\[
1.2
\]

Therefore:

\[
1.2(2)=2.4
\]

## Step 3 — Take minimum

\[
L^{CLIP}
=
\min(3,2.4)
\]

\[
\boxed{L^{CLIP}=2.4}
\]

### Exam takeaway

PPO prevents a large policy update from receiving unlimited benefit.

---

# Q22. Prioritized Experience Replay

> Four experiences have TD errors:
>
> \[
> 1,\;2,\;4,\;8
> \]
>
> If:
>
> \[
> \alpha=0.5
> \]
>
> calculate their sampling probabilities.

## Step 1 — Calculate priorities

\[
p_i=|\delta_i|^{0.5}
\]

Therefore:

\[
p_1=1
\]

\[
p_2=\sqrt2\approx1.414
\]

\[
p_3=2
\]

\[
p_4=\sqrt8\approx2.828
\]

---

## Step 2 — Sum

\[
\sum p_i
=
1+1.414+2+2.828
\]

\[
\approx7.242
\]

---

## Step 3 — Probabilities

\[
P_1=
\frac1{7.242}
\approx0.138
\]

\[
P_2=
\frac{1.414}{7.242}
\approx0.195
\]

\[
P_3=
\frac2{7.242}
\approx0.276
\]

\[
P_4=
\frac{2.828}{7.242}
\approx0.390
\]

Therefore:

\[
\boxed{
P\approx
[0.138,\;0.195,\;0.276,\;0.390]
}
\]

The largest-TD-error transition is sampled most frequently.

---

# Q23. Replay Buffer

> A replay buffer has capacity 5000. The agent generates 80 experiences per episode. How many episodes are required to fill the buffer if it starts empty?

## Solution

Required experiences:

\[
5000
\]

Experiences per episode:

\[
80
\]

Therefore:

\[
\frac{5000}{80}=62.5
\]

The buffer becomes full during episode:

\[
\boxed{63}
\]

After 62 complete episodes:

\[
62(80)=4960
\]

The remaining capacity is:

\[
5000-4960=40
\]

Thus the buffer becomes full after the first 40 experiences of episode 63.

\[
\boxed{\text{Buffer becomes full during episode 63}}
\]

---

# Q24. Dyna-Q Planning Update

> A Dyna-Q agent receives a real transition:
>
> \[
> (s,a,r,s')
> \]
>
> with:
>
> \[
> Q(s,a)=2
> \]
>
> \[
> r=3
> \]
>
> \[
> \gamma=0.9
> \]
>
> \[
> \max_{a'}Q(s',a')=5
> \]
>
> and:
>
> \[
> \alpha=0.1
> \]
>
> Calculate the Q update from this experience. Then explain what happens when the learned model replays the same transition during planning.

## Real experience update

Q-learning update:

\[
Q_{\text{new}}
=
Q+
\alpha[
r+\gamma\max Q'-Q
]
\]

Substitute:

\[
Q_{\text{new}}
=
2+
0.1[
3+0.9(5)-2
]
\]

\[
=
2+
0.1[
3+4.5-2
]
\]

\[
=
2+0.1(5.5)
\]

\[
\boxed{Q_{\text{new}}=2.55}
\]

---

## Planning step

Dyna-Q stores the transition in its learned model.

Later, the agent can sample the model:

\[
(s,a)\rightarrow(r,s')
\]

and perform another Q-learning update **without interacting with the real environment again**.

Therefore Dyna-Q combines:

\[
\boxed{
\text{real experience}
+
\text{model-based planning}
}
\]

This improves sample efficiency.

---

# Q25. Dyna-Q with a Different Simulated Transition

> A learned model predicts:
>
> \[
> (s,a)\rightarrow(r=2,s')
> \]
>
> with:
>
> \[
> Q(s,a)=3
> \]
>
> \[
> \gamma=0.9
> \]
>
> \[
> \max_{a'}Q(s',a')=6
> \]
>
> \[
> \alpha=0.2
> \]
>
> Calculate the planning update.

## Solution

\[
Q_{\text{new}}
=
3+
0.2[
2+0.9(6)-3
]
\]

\[
=
3+
0.2[
2+5.4-3
]
\]

\[
=
3+0.2(4.4)
\]

\[
\boxed{Q_{\text{new}}=3.88}
\]

The important point is that this update can occur using the **learned model**, without another real environment interaction.

---

# Q26. Model-Based vs Model-Free Numerical Comparison

> An agent learns:
>
> \[
> Q(s,a)=4
> \]
>
> and receives:
>
> \[
> r=2
> \]
>
> with:
>
> \[
> \gamma=0.9
> \]
>
> and:
>
> \[
> \max Q(s',a')=5
> \]
>
> Calculate the Q-learning update. Then explain how a model-based agent could use the same transition again.

## Solution

The model-free Q-learning update is:

\[
Q_{\text{new}}
=
Q+
\alpha[
r+\gamma\max Q'-Q
]
\]

If:

\[
\alpha=0.1
\]

then:

\[
Q_{\text{new}}
=
4+
0.1[
2+0.9(5)-4
]
\]

\[
=
4+0.1(2.5)
\]

\[
\boxed{Q_{\text{new}}=4.25}
\]

A model-based agent can store:

\[
(s,a,r,s')
\]

in an environment model and later simulate the same transition.

Thus the model can provide additional planning updates without requiring the environment to be queried again.

---

# Q27. Combined Numerical — Q-Learning vs SARSA

> Consider:
>
> \[
> Q(s,a)=5
> \]
>
> \[
> r=-1
> \]
>
> \[
> \gamma=0.9
> \]
>
> \[
> \alpha=0.1
> \]
>
> At the next state:
>
> \[
> Q(s',a_1)=8
> \]
>
> \[
> Q(s',a_2)=3
> \]
>
> The policy actually chooses \(a_2\).
>
> Calculate the Q-learning and SARSA updates.

## Q-Learning

Q-learning uses:

\[
\max(8,3)=8
\]

Therefore:

\[
Q_{\text{new}}
=
5+
0.1[
-1+0.9(8)-5
]
\]

\[
=
5+0.1[-1+7.2-5]
\]

\[
=
5+0.12
\]

\[
\boxed{Q_{\text{Q-learning}}=5.12}
\]

---

## SARSA

SARSA uses the actual action:

\[
a_2
\]

Therefore:

\[
Q(s',a_2)=3
\]

\[
Q_{\text{new}}
=
5+
0.1[
-1+0.9(3)-5
]
\]

\[
=
5+0.1[-1+2.7-5]
\]

\[
=
5-0.33
\]

\[
\boxed{Q_{\text{SARSA}}=4.67}
\]

---

## Final comparison

\[
\boxed{
Q_{\text{Q-learning}}=5.12
}
\]

\[
\boxed{
Q_{\text{SARSA}}=4.67
}
\]

This numerical question is particularly important because it directly tests the distinction between:

\[
\boxed{\text{off-policy Q-Learning}}
\]

and:

\[
\boxed{\text{on-policy SARSA}}
\]

---

# Q28. Combined Numerical — Bellman + Policy Improvement

> A state has three possible actions:
>
> \[
> a_1:\;r=2,\;V(s')=5
> \]
>
> \[
> a_2:\;r=4,\;V(s')=3
> \]
>
> \[
> a_3:\;r=1,\;V(s')=7
> \]
>
> Given:
>
> \[
> \gamma=0.8
> \]
>
> calculate the value associated with every action and determine the greedy policy.

## Solution

### Action \(a_1\)

\[
2+0.8(5)
\]

\[
=2+4
\]

\[
\boxed{6}
\]

### Action \(a_2\)

\[
4+0.8(3)
\]

\[
=4+2.4
\]

\[
\boxed{6.4}
\]

### Action \(a_3\)

\[
1+0.8(7)
\]

\[
=1+5.6
\]

\[
\boxed{6.6}
\]

Therefore:

\[
V^*(s)
=
\max(6,6.4,6.6)
\]

\[
\boxed{V^*(s)=6.6}
\]

and:

\[
\boxed{\pi^*(s)=a_3}
\]

---

# Part C — Very Important Exam Patterns

## Pattern 1 — Discounted Return

Whenever a question gives:

\[
r_1,r_2,r_3,\ldots
\]

use:

\[
\boxed{
G_t=
r_{t+1}
+\gamma r_{t+2}
+\gamma^2r_{t+3}
+\cdots
}
\]

Do not forget that the first reward has:

\[
\gamma^0=1
\]

---

## Pattern 2 — Bellman Expectation

If the question gives a **policy probability**, use:

\[
\boxed{
V^\pi(s)
=
\sum_a
\pi(a|s)
[
r+\gamma V(s')
]
}
\]

Do not simply take the maximum.

---

## Pattern 3 — Bellman Optimality

If the question says:

- optimal;
- greedy;
- best action;
- maximum value;

use:

\[
\boxed{
V^*(s)
=
\max_a
[
r+\gamma V(s')
]
}
\]

---

## Pattern 4 — TD Learning

If the question gives:

\[
V(s),V(s'),r,\alpha,\gamma
\]

use:

\[
\boxed{
\delta=r+\gamma V(s')-V(s)
}
\]

then:

\[
\boxed{
V_{\text{new}}=V+\alpha\delta
}
\]

---

## Pattern 5 — Monte Carlo

If the question gives a complete episode:

\[
r_1,r_2,\ldots,r_T
\]

calculate the actual return:

\[
\boxed{
G_t=
\sum_{k=0}^{T-t-1}
\gamma^kr_{t+k+1}
}
\]

No bootstrapping.

---

## Pattern 6 — Q-Learning

Always use:

\[
\boxed{
\max_{a'}Q(s',a')
}
\]

The next action does **not** need to be the action actually selected.

---

## Pattern 7 — SARSA

Always use:

\[
\boxed{
Q(s',a')
}
\]

where \(a'\) is the **actual next action selected**.

---

## Pattern 8 — DQN

Usually calculate:

\[
\boxed{
y=
r+\gamma\max_{a'}Q_{\text{target}}(s',a')
}
\]

Then, if asked for an update:

\[
\boxed{
Q_{\text{new}}
=
Q+\alpha(y-Q)
}
\]

---

## Pattern 9 — Double DQN

Remember:

\[
\boxed{
\text{Online network → SELECT}
}
\]

\[
\boxed{
\text{Target network → EVALUATE}
}
\]

Specifically:

\[
a^*=
\arg\max_aQ_{\text{online}}(s',a)
\]

then:

\[
y=
r+\gamma Q_{\text{target}}(s',a^*)
\]

---

## Pattern 10 — Dueling DQN

Given \(V\) and \(A\):

\[
\boxed{
Q(s,a)
=
V(s)+
A(s,a)-\operatorname{mean}(A)
}
\]

Always calculate the mean advantage first.

---

## Pattern 11 — Actor-Critic

First calculate:

\[
\boxed{
\delta=
r+\gamma V(s')-V(s)
}
\]

Then interpret:

\[
\boxed{
\delta>0
\Rightarrow
\text{reinforce action}
}
\]

\[
\boxed{
\delta<0
\Rightarrow
\text{discourage action}
}
\]

Critic update:

\[
\boxed{
V(s)\leftarrow V(s)+\alpha\delta
}
\]

---

## Pattern 12 — PPO

Calculate:

\[
r_t=
\frac{\pi_\theta(a_t|s_t)}
{\pi_{\theta_{\text{old}}}(a_t|s_t)}
\]

Then:

\[
\boxed{
L^{CLIP}
=
\min
[
r_tA_t,
\operatorname{clip}(r_t,1-\epsilon,1+\epsilon)A_t
]
}
\]

Remember:

\[
\boxed{
1-\epsilon\le r_t\le1+\epsilon
}
\]

is the allowed ratio range.

---

## Pattern 13 — Prioritized Experience Replay

First:

\[
\boxed{
p_i=|\delta_i|^\alpha
}
\]

Then:

\[
\boxed{
P(i)=
\frac{p_i}{\sum_jp_j}
}
\]

Do not normalize the TD errors directly.

---

## Pattern 14 — Replay Buffer

If:

- capacity = \(C\);
- \(x\) experiences added per episode;

then:

\[
\boxed{
\text{episodes to fill}
=
\left\lceil\frac{C}{x}\right\rceil
}
\]

Once full:

\[
\boxed{\text{buffer size remains }C}
\]

---

## Pattern 15 — Dyna-Q

Dyna-Q combines:

\[
\boxed{
\text{Direct RL update}
+
\text{Model-based planning}
}
\]

The planning step uses the learned model to generate simulated transitions.

The Q-update itself can still be:

\[
\boxed{
Q(s,a)
\leftarrow
Q(s,a)+
\alpha[
r+\gamma\max Q(s',a')-Q(s,a)
]
}
\]

---

# Final Numerical Formula Sheet

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

## Bellman Expectation

\[
\boxed{
V^\pi(s)
=
\sum_a
\pi(a|s)
[
R+\gamma V^\pi(s')
]
}
\]

## Bellman Optimality

\[
\boxed{
V^*(s)
=
\max_a
[
R+\gamma V^*(s')
]
}
\]

## TD

\[
\boxed{
\delta=
r+\gamma V(s')-V(s)
}
\]

\[
\boxed{
V_{\text{new}}=V+\alpha\delta
}
\]

## Q-Learning

\[
\boxed{
Q_{\text{new}}
=
Q+
\alpha[
r+\gamma\max_{a'}Q(s',a')-Q]
}
\]

## SARSA

\[
\boxed{
Q_{\text{new}}
=
Q+
\alpha[
r+\gamma Q(s',a')-Q]
}
\]

## DQN

\[
\boxed{
y=
r+\gamma\max_{a'}Q_{\text{target}}(s',a')
}
\]

## Double DQN

\[
\boxed{
a^*=
\arg\max_{a'}Q_{\text{online}}(s',a')
}
\]

\[
\boxed{
y=
r+\gamma Q_{\text{target}}(s',a^*)
}
\]

## Dueling DQN

\[
\boxed{
Q=
V+(A-\operatorname{mean}(A))
}
\]

## Actor-Critic

\[
\boxed{
\delta=
r+\gamma V(s')-V(s)
}
\]

## PPO

\[
\boxed{
L^{CLIP}
=
\min
[
r_tA_t,
\operatorname{clip}(r_t,1-\epsilon,1+\epsilon)A_t
]
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
P(i)=
\frac{p_i}{\sum_jp_j}
}
\]

## Replay Buffer

\[
\boxed{
\text{Fill episodes}
=
\left\lceil
\frac{\text{capacity}}
{\text{experiences per episode}}
\right\rceil
}