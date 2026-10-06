# Unit 4 — Problems 2

## Source PDFs

- [RL CSAI Sample Questions](pdfs/RL%20CSAI%20Sample%20questions%20%283%29.pdf)
- [RL Question Bank](pdfs/QUESTIONS%20_rl%20%282%29.pdf)

---

# Q11. Q-Learning Basic Calculation

> An agent is learning to navigate the grid world using Q-learning, a popular RL algorithm. The Q-value Q(s,a) represents the quality of taking action a in state s. Assume the agent is in state (2,2), and the Q-values for moving left and right are 0.5 and -0.2, respectively. After taking the action to move left, the agent receives a reward of -1 and ends up in state (2,1) with the highest Q-value for the next actions being 0.7. The learning rate (α) is 0.1, and the discount factor (γ) is 0.9. Calculate the updated Q-value for the action taken (moving left from state (2,2)). Explain the significance of the learning rate and discount factor in the Q-learning update formula.

## Solution

The Q-learning equation is:

\[
Q(s,a)\leftarrow Q(s,a)+
\alpha
[
r+\gamma\max_{a'}Q(s',a')-Q(s,a)
]
\]

Given:

\[
Q(s,a)=0.5
\]

\[
r=-1
\]

\[
\max Q(s',a')=0.7
\]

\[
\alpha=0.1
\]

\[
\gamma=0.9
\]

Substitute:

\[
Q_{\text{new}}
=
0.5+
0.1[
-1+0.9(0.7)-0.5
]
\]

\[
=0.5+0.1[-1+0.63-0.5]
\]

\[
=0.5+0.1(-0.87)
\]

\[
=0.5-0.087
\]

\[
\boxed{Q_{\text{new}}=0.413}
\]

### Learning rate α

\[
\alpha=0.1
\]

controls how strongly the new experience changes the current Q-value.

Higher \(\alpha\):

- faster learning;
- greater effect of new experiences.

Lower \(\alpha\):

- slower learning;
- more gradual updates.

### Discount factor γ

\[
\gamma=0.9
\]

controls the importance of future rewards.

Higher \(\gamma\):

> greater importance to future rewards.

Lower \(\gamma\):

> greater emphasis on immediate rewards.

---

# Q12. Policy Improvement

> An RL agent uses a policy π to choose actions in a simplified environment with three states (A, B, C) and two actions (X, Y). The transition rewards are as follows: A-X leads to B with a reward of +2, A-Y leads to C with a reward of +1, B-X leads to C with a reward of +2, B-Y leads to A with a reward of -1, C-X leads to A with a reward of +0, and C-Y leads to B with a reward of +3. Assuming the agent starts with a policy to always choose action X, calculate the total reward for two transitions starting from each state. Discuss how the agent could improve its policy based on the rewards received from the transitions.

## Given transitions

| State | Action | Next State | Reward |
|---|---|---|---:|
| A | X | B | +2 |
| A | Y | C | +1 |
| B | X | C | +2 |
| B | Y | A | -1 |
| C | X | A | 0 |
| C | Y | B | +3 |

Initial policy:

\[
\boxed{\pi(A)=\pi(B)=\pi(C)=X}
\]

---

## Starting from A

First transition:

\[
A\xrightarrow{X,+2}B
\]

Second transition:

\[
B\xrightarrow{X,+2}C
\]

Therefore:

\[
G=2+2
\]

\[
\boxed{G_A=4}
\]

---

## Starting from B

\[
B\xrightarrow{X,+2}C
\]

Then:

\[
C\xrightarrow{X,0}A
\]

Therefore:

\[
G=2+0
\]

\[
\boxed{G_B=2}
\]

---

## Starting from C

\[
C\xrightarrow{X,0}A
\]

Then:

\[
A\xrightarrow{X,+2}B
\]

Therefore:

\[
G=0+2
\]

\[
\boxed{G_C=2}
\]

---

## Summary

| Starting state | First action | Second action | Total reward |
|---|---|---|---:|
| A | X | X | **4** |
| B | X | X | **2** |
| C | X | X | **2** |

---

## Policy improvement

Compare immediate rewards.

### A

\[
X=2,\quad Y=1
\]

Therefore:

\[
\boxed{X\text{ is preferred}}
\]

### B

\[
X=2,\quad Y=-1
\]

Therefore:

\[
\boxed{X\text{ is preferred}}
\]

### C

\[
X=0,\quad Y=3
\]

Therefore:

\[
\boxed{Y\text{ is preferred}}
\]

A simple reward-based policy improvement gives:

\[
\boxed{
\pi(A)=X,\quad
\pi(B)=X,\quad
\pi(C)=Y
}
\]

### Important note

The question does not specify a discount factor.

Therefore, this comparison is based on the immediate transition rewards.

For a complete Bellman policy-improvement calculation, we would compare:

\[
R(s,a)+\gamma V^\pi(s')
\]

for every action.

---

# Q13. Autonomous Driving

> An autonomous vehicle is trained using RL to navigate through a city environment. The vehicle must learn to reach a destination as quickly as possible while avoiding obstacles and obeying traffic laws. The state space includes the vehicle's speed, direction, location, and the proximity of obstacles. Actions include accelerating, decelerating, and turning. The reward function gives positive points for moving closer to the destination, negative points for collisions, and penalties for traffic law violations. Design a reward function that encourages the vehicle to reach its destination efficiently while ensuring safety and law compliance. Discuss how you would implement an exploration strategy that allows the vehicle to learn about its environment without compromising safety.

## Solution

A suitable reward function is:

\[
\boxed{
R=
w_dR_d
-w_tR_t
-w_cR_c
-w_vR_v
}
\]

where:

- \(R_d\): progress toward destination;
- \(R_t\): time/step cost;
- \(R_c\): collision indicator/severity;
- \(R_v\): traffic-law violation penalty.

For example:

\[
R=
5(\text{progress})
-1(\text{step})
-100(\text{collision})
-20(\text{violation})
\]

The exact weights are design parameters.

### Desired behavior

Moving closer:

\[
\Rightarrow +R
\]

Taking unnecessary steps:

\[
\Rightarrow -R
\]

Traffic violation:

\[
\Rightarrow \text{large penalty}
\]

Collision:

\[
\Rightarrow \text{very large penalty}
\]

### Safe exploration

Random exploration is unsafe for a real autonomous vehicle.

A safer approach is:

1. Train extensively in simulation.
2. Restrict exploration to legal actions.
3. Apply hard safety constraints.
4. Use a safety controller to override dangerous actions.
5. Penalize collisions strongly.
6. Gradually transfer the learned policy to increasingly realistic environments.

An epsilon-greedy policy can still be used, but exploration should be restricted to actions that satisfy safety constraints.

---

# Q14. Healthcare Treatment Optimization

> An RL agent is used to recommend personalized treatment plans for patients with chronic diseases, considering the patient's health state, medical history, and treatment response. The state space includes various health indicators, treatment history, and patient-reported outcomes. Actions include adjusting medication dosages, changing medications, or recommending lifestyle changes. The reward function aims to improve patient health outcomes while minimizing side effects and costs. Propose a reward function that accurately reflects the goal of optimizing patient health outcomes. Discuss the ethical considerations and the importance of safety in exploring new treatment plans with RL.

## Solution

A suitable reward can be expressed as:

\[
\boxed{
R=
w_hH-w_sS-w_cC
}
\]

where:

- \(H\): health improvement;
- \(S\): side-effect severity;
- \(C\): treatment cost.

For example:

\[
R=
10H-8S-2C
\]

The numerical weights are illustrative; the question does not specify them.

### Why this formulation?

The objective is not simply:

\[
\max H
\]

because a treatment that produces large health improvements but severe side effects may not be desirable.

The objective should balance:

\[
\text{health improvement}
\]

against:

\[
\text{side effects + cost}
\]

### Safety

Healthcare is a high-risk environment, so unrestricted exploration is inappropriate.

The system should use:

- safety constraints;
- medically acceptable action ranges;
- historical/simulated data;
- clinician supervision;
- human approval for high-risk actions.

### Ethical considerations

Important considerations include:

- patient safety;
- privacy;
- informed consent;
- bias in training data;
- fairness;
- accountability.

### Exam conclusion

> In healthcare RL, safety constraints and clinical oversight must take priority over unrestricted exploration because incorrect exploration can directly harm patients.