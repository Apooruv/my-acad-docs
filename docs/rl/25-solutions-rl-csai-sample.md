# Solutions — RL CSAI Sample Questions

## Source PDF

[Open RL CSAI Sample questions (3).pdf](pdfs/RL%20CSAI%20Sample%20questions%20%283%29.pdf)

---

# Q1. Autonomous Vehicle Navigation

> Design an RL agent that can safely navigate an autonomous vehicle through a simulated urban environment. The agent must learn to follow traffic rules, avoid collisions, and reach its destination in the shortest time possible.

## Solution

This can be formulated as an MDP:

\[
MDP=(S,A,P,R,\gamma)
\]

### State

The state should contain information such as:

- vehicle position;
- vehicle speed;
- direction;
- distance from nearby vehicles;
- distance from obstacles;
- traffic-light status;
- lane information;
- destination location.

\[
s=(position,speed,direction,traffic,obstacles,\ldots)
\]

### Actions

Possible actions:

- accelerate;
- decelerate;
- maintain speed;
- turn left;
- turn right;
- change lane.

### Reward

A suitable reward should:

- reward progress toward destination;
- reward reaching destination;
- penalize collisions heavily;
- penalize traffic violations;
- penalize unnecessary delay.

For example:

\[
R=
w_p(\text{progress})
-w_t(\text{time})
-w_c(\text{collision})
-w_v(\text{violation})
+w_g(\text{goal})
\]

with:

\[
w_c,w_v,w_g \gg w_t
\]

for safety-critical penalties.

### Learning

A DQN can be used if the action space is discrete.

The agent repeatedly:

1. observes state \(s\);
2. chooses action \(a\);
3. receives reward \(r\);
4. observes \(s'\);
5. stores \((s,a,r,s',done)\);
6. samples experiences from the replay buffer;
7. updates the DQN.

### Exam conclusion

The important point is that the reward function must not encourage the vehicle to reach the destination quickly at the cost of collisions or traffic violations.

---

# Q2. Smart Grid Energy Management

> Develop an RL agent that optimizes energy consumption in a smart grid, balancing supply and demand by dynamically pricing energy based on usage patterns, weather conditions, and renewable energy availability.

## Solution

### State

The state may contain:

- current energy demand;
- available energy supply;
- renewable energy generation;
- battery/storage level;
- weather conditions;
- current electricity price;
- predicted demand.

\[
s=(demand,supply,renewable,storage,weather,price)
\]

### Actions

The agent can:

- increase/decrease price;
- maintain price;
- store energy;
- release stored energy;
- purchase energy externally.

### Reward

The objective is to maximize efficient energy usage while maintaining supply-demand balance.

A possible reward is:

\[
R=
-\lambda_1(\text{energy cost})
-\lambda_2|\text{supply}-\text{demand}|
+\lambda_3(\text{renewable utilization})
\]

A shortage can receive a large negative penalty.

### RL process

```text
Observe grid state
       ↓
Choose pricing/energy action
       ↓
Observe demand and supply
       ↓
Receive reward
       ↓
Update policy/value
```

### Exam point

RL is useful because demand, renewable generation and weather conditions are dynamic, so a fixed rule-based strategy may not adapt effectively.

---

# Q3. Personalized Education

> Create an RL-based system that personalizes learning experiences for students by adapting the difficulty level and topics based on student performance and engagement.

## Solution

### State

The state can contain:

- current topic;
- test scores;
- number of mistakes;
- response time;
- engagement level;
- previous difficulty;
- learning progress.

### Actions

The agent can:

- increase difficulty;
- decrease difficulty;
- maintain difficulty;
- change topic;
- provide revision material;
- provide a harder problem.

### Reward

A suitable reward should encourage learning and engagement.

For example:

\[
R=
w_1(\text{learning improvement})
+w_2(\text{engagement})
-w_3(\text{excessive difficulty})
\]

A large positive reward can be given when the student's performance improves.

### Goal

The learned policy should select educational content that maximizes long-term learning rather than simply maximizing immediate quiz scores.

---

# Q4. Healthcare Treatment Optimization

> Design an RL agent that suggests personalized treatment plans for patients with chronic conditions such as diabetes by continuously learning from patient data, treatment outcomes and evolving medical research.

## Solution

### State

The state may include:

- blood glucose;
- blood pressure;
- medical history;
- current medication;
- previous treatment response;
- patient-reported symptoms;
- other relevant health indicators.

### Actions

Possible actions include:

- adjust medication dosage;
- change medication;
- recommend lifestyle modification;
- maintain the current treatment.

### Reward

The reward should prioritize patient health and strongly penalize harmful outcomes.

\[
R=
w_h(\text{health improvement})
-w_s(\text{side effects})
-w_c(\text{treatment cost})
-w_r(\text{risk})
\]

### Important safety consideration

Unlike an ordinary game environment, unsafe exploration can directly harm a patient.

Therefore, unrestricted exploration should not be used.

Possible safeguards include:

- restricting actions to medically approved treatments;
- human/doctor approval;
- safety constraints;
- offline training using historical data;
- simulation before deployment;
- conservative policy updates.

### Exam conclusion

Healthcare RL should prioritize safety and clinical constraints over unrestricted exploration.

---

# Q5. Frozen Lake Navigation

> The agent must navigate across a frozen lake from a starting point to a goal while avoiding holes. Use Q-learning to find the best action in each state. The environment provides a reward of 1 if the agent reaches the goal and 0 otherwise.

## Solution

Frozen Lake can be represented using:

\[
Q(s,a)
\]

for every state-action pair.

Initially:

\[
Q(s,a)=0
\]

for all state-action pairs.

The Q-learning update is:

\[
Q(s,a)
\leftarrow
Q(s,a)+
\alpha
[
r+\gamma\max_{a'}Q(s',a')
-Q(s,a)
]
\]

---

## Learning process

Suppose the agent reaches the goal after taking action \(a\).

Then:

\[
r=1
\]

For a terminal state:

\[
Q(s,a)
\leftarrow
Q(s,a)+\alpha[1-Q(s,a)]
\]

Repeated successful episodes increase the Q-value of actions that eventually lead to the goal.

Actions leading toward holes receive no positive terminal reward.

Eventually:

\[
\boxed{
\pi(s)=\arg\max_aQ(s,a)
}
\]

gives the learned policy.

### Exam conclusion

The best action in every state is the action having the largest learned Q-value.

---

# Q6. Understanding Rewards and Actions

> A 4×4 grid world starts at (0,0) and the goal is (3,3). The agent receives -1 for each action and +10 for reaching the goal. The path is right, right, down, down, down, right. Calculate the total cumulative reward. What happens if the goal reward becomes +20?

## Solution

The path contains:

\[
6
\]

actions.

The final action reaches the goal.

Using the interpretation that each ordinary step has reward \(-1\) and the goal transition gives \(+10\):

- first 5 actions: \(-1\) each;
- goal-reaching action: \(+10\).

Therefore:

\[
G=-1-1-1-1-1+10
\]

\[
\boxed{G=5}
\]

### If goal reward becomes +20

\[
G=-5+20
\]

\[
\boxed{G=15}
\]

Therefore reaching the goal becomes significantly more valuable.

### Effect on learning

A larger terminal reward increases the Q-values of actions leading toward the goal.

Thus the agent receives a stronger signal to reach the goal.

---

# Q7. Discount Factor in Future Rewards

> Consider the same grid world. The discount factor is 0.9. The agent takes right, right, down, down, right, and then reaches the goal. Calculate the cumulative discounted reward. Explain the effect of changing γ to 0.99.

## Solution

The sequence contains five ordinary actions followed by the goal-reaching transition.

Rewards:

\[
-1,-1,-1,-1,-1,+10
\]

The discounted return is:

\[
G=
-1
+\gamma(-1)
+\gamma^2(-1)
+\gamma^3(-1)
+\gamma^4(-1)
+\gamma^5(10)
\]

For:

\[
\gamma=0.9
\]

\[
G=
-1-0.9-0.81-0.729-0.6561+10(0.59049)
\]

\[
G=
-4.0951+5.9049
\]

\[
\boxed{G=1.8098}
\]

### If γ = 0.99

Future rewards are discounted much less.

Therefore the future goal reward retains more of its value.

\[
\boxed{
\gamma\uparrow
\Rightarrow
\text{future rewards become more important}
}
\]

Thus the agent becomes more willing to take actions whose benefits occur later.

---

# Q8. Exploration vs Exploitation

> Lever A returns a reward of 1 with probability 0.5. Lever B returns 2 with probability 0.2. The agent explores randomly 20% of the time and exploits 80% of the time. For 100 pulls, estimate the expected total reward. What happens with 50% exploration and 50% exploitation?

## Solution

### Expected reward of Lever A

\[
E[A]=1(0.5)=0.5
\]

### Expected reward of Lever B

\[
E[B]=2(0.2)=0.4
\]

Therefore:

\[
\boxed{A\text{ is the better lever}}
\]

---

## 20% exploration, 80% exploitation

During exploitation:

\[
E[R_{\text{exploit}}]=0.5
\]

During random exploration, assuming both levers are selected with equal probability:

\[
E[R_{\text{explore}}]
=
\frac{0.5+0.4}{2}
=
0.45
\]

Therefore:

\[
E[R]
=
0.8(0.5)+0.2(0.45)
\]

\[
=0.4+0.09
\]

\[
=0.49
\]

For 100 pulls:

\[
\boxed{49}
\]

expected reward.

---

## 50% exploration, 50% exploitation

\[
E[R]
=
0.5(0.5)+0.5(0.45)
\]

\[
=0.25+0.225
\]

\[
=0.475
\]

For 100 pulls:

\[
\boxed{47.5}
\]

expected reward.

### Conclusion

Increasing exploration from 20% to 50% reduces immediate expected reward here because Lever A is already known to be better.

However, exploration may help discover better actions in a less-known environment.

---

# Q9. Discount Factor in Future Rewards

> Consider the same grid world with γ = 0.9. The agent takes right, right, down, down, right, and then reaches the goal. Calculate the discounted cumulative reward and explain the effect of γ = 0.99.

## Solution

This question repeats Q7.

The reward sequence is:

\[
-1,-1,-1,-1,-1,+10
\]

Therefore:

\[
G=
-1
-0.9
-0.9^2
-0.9^3
-0.9^4
+10(0.9)^5
\]

\[
\boxed{G=1.8098}
\]

With:

\[
\gamma=0.99
\]

the future goal reward is discounted less.

Hence:

\[
\boxed{
\gamma=0.99
\Rightarrow
\text{greater importance to future rewards}
}
\]

---

# Q10. Exploration vs Exploitation

> Lever A gives reward 1 with probability 0.5 and Lever B gives reward 2 with probability 0.2. The agent explores 20% and exploits 80% of the time. Calculate the expected total reward for 100 pulls. Discuss the 50%-50% case.

## Solution

Expected values:

\[
E[A]=0.5
\]

\[
E[B]=0.4
\]

Therefore Lever A is optimal.

For 20% exploration:

\[
E[R]=0.8(0.5)+0.2(0.45)
\]

\[
=0.49
\]

Hence:

\[
\boxed{E[R_{100}]=49}
\]

For 50% exploration:

\[
E[R]=0.5(0.5)+0.5(0.45)
\]

\[
=0.475
\]

Hence:

\[
\boxed{E[R_{100}]=47.5}
\]

The higher exploration rate lowers immediate expected reward because exploration sometimes chooses the inferior lever.

---

# Q11. Q-Learning Basic Calculation

> The agent is in state (2,2). The Q-value for moving left is 0.5. After moving left, it receives reward -1 and reaches (2,1), whose highest next Q-value is 0.7. α = 0.1 and γ = 0.9. Calculate the updated Q-value.

## Given

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

Q-learning:

\[
Q_{\text{new}}
=
Q+\alpha[r+\gamma\max Q'-Q]
\]

Substitute:

\[
Q_{\text{new}}
=
0.5+
0.1[-1+0.9(0.7)-0.5]
\]

\[
=
0.5+
0.1[-1+0.63-0.5]
\]

\[
=
0.5+0.1(-0.87)
\]

\[
\boxed{Q_{\text{new}}=0.413}
\]

### Learning rate

\[
\alpha
\]

controls how strongly the new experience changes the old Q-value.

Small \(\alpha\):

\[
\rightarrow
\text{slow updates}
\]

Large \(\alpha\):

\[
\rightarrow
\text{faster but potentially less stable updates}
\]

### Discount factor

\[
\gamma
\]

controls the importance of future rewards.

High \(\gamma\):

\[
\rightarrow
\text{future rewards matter more}
\]

Low \(\gamma\):

\[
\rightarrow
\text{immediate rewards matter more}
\]

---

# Q12. Policy Improvement

> States A, B, C and actions X, Y have the following transitions:
>
> A-X → B, reward +2  
> A-Y → C, reward +1  
> B-X → C, reward +2  
> B-Y → A, reward -1  
> C-X → A, reward 0  
> C-Y → B, reward +3
>
> The initial policy always chooses X. Calculate the total reward for two transitions starting from each state. Discuss policy improvement.

## Solution

Initial policy:

\[
\boxed{\pi(s)=X}
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
\boxed{G_A=2+2=4}
\]

---

## Starting from B

First:

\[
B\xrightarrow{X,+2}C
\]

Second:

\[
C\xrightarrow{X,0}A
\]

Therefore:

\[
\boxed{G_B=2+0=2}
\]

---

## Starting from C

First:

\[
C\xrightarrow{X,0}A
\]

Second:

\[
A\xrightarrow{X,+2}B
\]

Therefore:

\[
\boxed{G_C=0+2=2}
\]

---

## Policy improvement

Compare X and Y.

### At A

\[
X:+2
\]

\[
Y:+1
\]

Choose:

\[
\boxed{X}
\]

### At B

\[
X:+2
\]

\[
Y:-1
\]

Choose:

\[
\boxed{X}
\]

### At C

\[
X:0
\]

\[
Y:+3
\]

Choose:

\[
\boxed{Y}
\]

Therefore an improved one-step policy is:

\[
\boxed{
\pi'(A)=X,\quad
\pi'(B)=X,\quad
\pi'(C)=Y
}
\]

The important policy-improvement idea is:

\[
\boxed{
\text{choose the action with higher expected value}
}
\]

---

# Q13. Autonomous Driving

> Design a reward function that encourages an autonomous vehicle to reach its destination efficiently while ensuring safety and law compliance. Discuss an exploration strategy that allows learning without compromising safety.

## Solution

A suitable reward can combine:

### Positive terms

- progress toward destination;
- successful goal completion.

### Negative terms

- collision;
- traffic violation;
- excessive delay;
- unsafe speed;
- unnecessary lane changes.

A general form is:

\[
\boxed{
R=
w_pP
+w_gG
-w_cC
-w_vV
-w_tT
}
\]

where:

- \(P\) = progress;
- \(G\) = goal achievement;
- \(C\) = collision indicator;
- \(V\) = traffic violation;
- \(T\) = time/delay.

Safety penalties should have very large magnitude.

---

## Safe exploration

Unrestricted random exploration is unsuitable.

A safer strategy is:

1. train initially in simulation;
2. use constrained action spaces;
3. reject unsafe actions;
4. use safety rules during exploration;
5. gradually reduce exploration;
6. validate the learned policy before deployment.

For example:

\[
\epsilon\text{-greedy}
\]

can be combined with a safety filter:

```text
Choose exploratory action
        ↓
Safety check
        ↓
Safe? ── No ──→ choose safe action
  |
 Yes
  ↓
Execute
```

### Exam conclusion

The reward should make collisions and violations much more costly than small improvements in speed.

---

# Q14. Healthcare Treatment Optimization

> Propose a reward function for personalized treatment that improves patient health while minimizing side effects and costs. Discuss ethical considerations and safety during exploration.

## Solution

A possible reward function is:

\[
\boxed{
R=
w_hH
-w_sS
-w_cC
-w_rR
}
\]

where:

- \(H\) = improvement in health outcome;
- \(S\) = side-effect severity;
- \(C\) = treatment cost;
- \(R\) = medical risk.

The weights should prioritize patient safety.

---

## Example

A treatment that improves health slightly but creates serious side effects should receive a low or negative reward.

Therefore:

\[
\boxed{
\text{Health improvement alone is not sufficient}
}
\]

---

## Ethical considerations

Important issues include:

### Patient safety

Unsafe exploratory treatments must not be freely tested.

### Human oversight

Clinicians should remain involved in high-risk decisions.

### Bias

Training data may contain demographic or treatment biases.

### Privacy

Patient medical data must be protected.

### Explainability

Healthcare decisions should be sufficiently understandable to clinicians.

### Safe exploration

Possible approaches include:

- offline RL;
- historical patient data;
- simulated environments;
- constrained policies;
- approved-treatment action spaces;
- human approval.

---

# Q15. Policy Evaluation in Grid World

> Consider a 3×3 grid world. The agent starts at (0,0), aims for (2,2), receives -1 for each step and +10 for reaching the goal. The policy chooses each action with equal probability. Calculate the expected return from each state using γ = 0.9. How does the return change if the policy always moves toward the goal?

## Solution

The Bellman expectation equation is:

\[
\boxed{
V^\pi(s)
=
\sum_a\pi(a|s)
\left[
R(s,a,s')
+\gamma V^\pi(s')
\right]
}
\]

Here:

\[
\pi(a|s)=\frac14
\]

for each action.

The goal is terminal:

\[
V(2,2)=0
\]

For wall movements, the agent remains in the same state, as specified by the grid-world convention.

For a normal transition:

\[
R=-1
\]

For a transition into the goal:

\[
R=10
\]

Solving the resulting Bellman equations gives approximately:

| State | \(V^\pi(s)\) |
|---|---:|
| (0,0) | -5.9225 |
| (0,1) | -5.0164 |
| (0,2) | -3.7675 |
| (1,0) | -5.0164 |
| (1,1) | -3.1442 |
| (1,2) | 0.2514 |
| (2,0) | -3.7675 |
| (2,1) | 0.2514 |
| (2,2) | 0 |

Therefore:

\[
\boxed{V^\pi(0,0)\approx-5.9225}
\]

under the uniformly random policy.

---

## If the policy always moves toward the goal

Now the agent follows the shortest path.

Let the distance from the current state to the goal be \(d\).

For a state one step away:

\[
V_1=10
\]

For two steps away:

\[
V_2=-1+0.9(10)
\]

\[
\boxed{V_2=8}
\]

For three steps:

\[
V_3=-1+0.9(8)
\]

\[
\boxed{V_3=6.2}
\]

For four steps:

\[
V_4=-1+0.9(6.2)
\]

\[
\boxed{V_4=4.58}
\]

The start state (0,0) is four steps from (2,2), so:

\[
\boxed{V(0,0)=4.58}
\]

Thus the goal-directed policy produces a much higher expected return than the random policy.

### Important exam point

\[
\boxed{
\text{Better policy}
\Rightarrow
\text{higher expected return}
}
\]

---

# Q16. Bellman Equation for Value Estimation

> State (1,1) can move to (1,0), (1,2), (0,1), and (2,1). Their estimated values are 2.0, 1.0, 0.5 and 3.0. The immediate rewards are -1 and γ = 0.9. Use the Bellman equation under a greedy policy.

## Solution

The next-state values are:

\[
2.0,\;1.0,\;0.5,\;3.0
\]

The greedy policy chooses the maximum:

\[
\max(2.0,1.0,0.5,3.0)=3.0
\]

Therefore the selected next state is:

\[
\boxed{(2,1)}
\]

Bellman greedy update:

\[
V(1,1)
=
R+\gamma\max_{s'}V(s')
\]

Substitute:

\[
V(1,1)
=
-1+0.9(3)
\]

\[
=-1+2.7
\]

\[
\boxed{V(1,1)=1.7}
\]

---

## If γ = 0.99

\[
V(1,1)
=
-1+0.99(3)
\]

\[
=-1+2.97
\]

\[
\boxed{V(1,1)=1.97}
\]

Therefore increasing γ increases the contribution of the future value.

---

# Q17. Q-Learning Update Scenario

> An agent is in state S and chooses action A, reaching S'. The reward is R = 2. α = 0.1, γ = 0.95. The highest Q-value for S' is 5. The current Q(S,A) is 3. Calculate the updated Q-value. What happens if the reward increases to 5?

## Given

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

## Q-learning equation

\[
Q_{\text{new}}
=
Q+\alpha
[
R+\gamma\max Q(S',a')
-Q
]
\]

Substitute:

\[
Q_{\text{new}}
=
3+
0.1[
2+0.95(5)-3]
\]

\[
=
3+
0.1[
2+4.75-3
]
\]

\[
=
3+0.1(3.75)
\]

\[
\boxed{Q_{\text{new}}=3.375}
\]

---

## If reward increases to 5

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
5+0.95(5)-3]
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

Therefore increasing the immediate reward increases the updated Q-value.

---

# Important Numerical Answers

| Question | Answer |
|---|---:|
| Q6 | \(5\) |
| Q7 | \(1.8098\) |
| Q8 | \(49\) expected reward |
| Q10 | \(49\) expected reward |
| Q11 | \(0.413\) |
| Q12 | A: 4, B: 2, C: 2 |
| Q15, \(V(0,0)\), random policy | \(\approx-5.9225\) |
| Q15, \(V(0,0)\), goal-directed policy | \(4.58\) |
| Q16 | \(1.7\) |
| Q16, γ = 0.99 | \(1.97\) |
| Q17 | \(3.375\) |
| Q17, R = 5 | \(3.675\) |

---

# Formulas to Remember

## Q-Learning

\[
\boxed{
Q(s,a)\leftarrow
Q(s,a)+
\alpha[
r+\gamma\max_{a'}Q(s',a')
-Q(s,a)]
}
\]

## Bellman Expectation Equation

\[
\boxed{
V^\pi(s)
=
\sum_a\pi(a|s)
[
R(s,a,s')+\gamma V^\pi(s')
]
}
\]

## Bellman Optimality Equation

\[
\boxed{
V^*(s)
=
\max_a
[
R(s,a,s')+\gamma V^*(s')
]
}
\]

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

## Policy

\[
\boxed{
\pi(s)=\arg\max_aQ(s,a)
}
\]
