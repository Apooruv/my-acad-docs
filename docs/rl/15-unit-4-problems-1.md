# RL Application Problems

## Source PDF

[RL CSAI Sample Questions](pdfs/RL%20CSAI%20Sample%20questions%20%283%29.pdf)

---

# Q1. Autonomous Vehicle Navigation

> **Problem Statement:** Design an RL agent that can safely navigate an autonomous vehicle through a simulated urban environment. The agent must learn to follow traffic rules, avoid collisions, and reach its destination in the shortest time possible.

## Solution

This problem can be formulated as an RL problem using:

\[
MDP=(S,A,P,R,\gamma)
\]

### State Space

The state should contain information relevant to driving decisions, such as:

- vehicle position
- vehicle speed
- vehicle direction
- distance from destination
- nearby vehicles
- nearby obstacles
- traffic-light state
- lane information
- traffic-sign information

Therefore:

\[
s_t=
(\text{position},
\text{speed},
\text{direction},
\text{obstacles},
\text{traffic state},
\ldots)
\]

### Action Space

Possible actions include:

- accelerate
- decelerate
- maintain speed
- turn left
- turn right
- change lane
- brake

Thus:

\[
A=
\{
accelerate,
decelerate,
left,
right,
brake,
\ldots
\}
\]

### Reward Function

The reward should encourage:

1. reaching the destination;
2. reducing travel time;
3. obeying traffic rules;
4. avoiding collisions.

A suitable reward formulation is:

\[
R=
w_pR_p
-w_tR_t
-w_cR_c
-w_vR_v
\]

where:

- \(R_p\): progress toward destination
- \(R_t\): time/step penalty
- \(R_c\): collision penalty
- \(R_v\): traffic violation penalty

For example:

\[
R=
5(\text{progress})
-1(\text{time step})
-100(\text{collision})
-20(\text{traffic violation})
\]

The exact weights are not given in the question, so these values are illustrative.

### Learning

The agent repeatedly interacts with a simulated environment:

```text
State
  ↓
Choose action
  ↓
Environment
  ↓
Reward + next state
  ↓
Update policy/value
  ↓
Repeat
```

A model-free method such as Q-learning can learn:

\[
Q(s,a)
\]

and eventually select:

\[
a^*=\arg\max_aQ(s,a)
\]

For a large continuous state space, a neural-network-based method such as DQN or an actor-critic method would be more appropriate than a tabular Q-table.

### Safe Exploration

Unrestricted random exploration is inappropriate for autonomous driving.

A safer strategy is:

- train initially in simulation;
- restrict exploration to legal actions;
- use safety constraints;
- apply a safety controller;
- penalize collisions heavily;
- gradually increase environment complexity.

### Final Answer

The autonomous-driving problem can be formulated as an MDP where the state describes the vehicle and surrounding environment, actions represent driving decisions, and rewards encourage progress while strongly penalizing collisions and traffic violations. The agent can learn an optimal policy through Q-learning or deep RL, with exploration constrained by safety mechanisms.

---

# Q2. Smart Grid Energy Management

> **Problem Statement:** Develop an RL agent that optimizes energy consumption in a smart grid, balancing the supply and demand by dynamically pricing energy based on usage patterns, weather conditions, and renewable energy availability.

## Solution

This can also be formulated as an MDP.

### State Space

The state should represent the current condition of the grid.

Possible state variables include:

- current energy demand;
- energy supply;
- electricity price;
- weather conditions;
- solar generation;
- wind generation;
- battery/storage level;
- time of day;
- historical usage patterns.

For example:

\[
s_t=
(D_t,S_t,P_t,W_t,B_t,\ldots)
\]

where:

- \(D_t\): demand
- \(S_t\): supply
- \(P_t\): current price
- \(W_t\): weather
- \(B_t\): battery level

### Action Space

The RL agent could:

- increase electricity price;
- decrease electricity price;
- keep price unchanged;
- charge storage;
- discharge storage;
- adjust demand-response incentives.

For a pricing-only formulation:

\[
A=
\{
increase,
decrease,
maintain
\}
\]

### Reward Function

The objective is to balance:

- energy demand and supply;
- operating cost;
- renewable utilization;
- grid stability.

A possible reward is:

\[
R=
w_1(\text{renewable utilization})
-w_2(\text{supply-demand imbalance})
-w_3(\text{operating cost})
-w_4(\text{peak demand})
\]

The agent should receive a penalty when:

\[
|Supply-Demand|
\]

becomes large.

### Learning Process

```text
Observe grid state
       ↓
Choose price/control action
       ↓
Grid responds
       ↓
Observe demand/supply
       ↓
Receive reward
       ↓
Update policy
```

Over time, the agent learns pricing/control actions that maintain a stable grid while efficiently using renewable energy.

### Example

Suppose renewable generation suddenly increases.

A good policy could:

\[
\text{increase renewable consumption}
\]

by lowering the effective energy price or increasing demand-response incentives.

If demand is very high and supply is limited:

\[
\text{increase price}
\]

can discourage unnecessary consumption.

### Final Answer

The state should represent supply, demand, renewable generation, weather, storage and current pricing. Actions modify energy prices or grid controls, while the reward should encourage supply-demand balance, renewable utilization and low operating cost. The RL agent learns the pricing/control policy through repeated interaction with the grid environment.

---

# Q3. Personalized Education

> **Problem Statement:** Create an RL-based system that personalizes learning experiences for students by adapting the difficulty level and topics of educational content based on the student's performance and engagement.

## Solution

The student-learning process can be modelled as an MDP.

### State Space

The state should represent the student's current learning condition.

Possible variables:

- current knowledge level;
- recent test scores;
- accuracy;
- response time;
- completed topics;
- difficulty currently being attempted;
- engagement;
- number of consecutive incorrect answers.

For example:

\[
s_t=
(\text{knowledge},
\text{score},
\text{engagement},
\text{difficulty},
\ldots)
\]

### Action Space

The agent can choose:

- easier question;
- same difficulty;
- harder question;
- new topic;
- revision;
- additional practice.

For example:

\[
A=
\{
easy,
medium,
hard,
revision,
new\ topic
\}
\]

### Reward Function

The system should maximize learning rather than simply maximize immediate correctness.

A possible reward is:

\[
R=
w_1(\text{learning gain})
+w_2(\text{engagement})
-w_3(\text{excessive difficulty})
-w_4(\text{repeated failure})
\]

For example:

- successful learning improvement → positive reward;
- appropriate challenge → positive reward;
- repeated failure → negative reward;
- disengagement → negative reward.

### Learning Process

```text
Student state
     ↓
Select content
     ↓
Student attempts content
     ↓
Observe performance
     ↓
Reward
     ↓
Update policy
     ↓
Select next content
```

### Example

Suppose a student repeatedly answers medium-level questions correctly.

The system can gradually increase difficulty:

\[
Medium\rightarrowHard
\]

If the student repeatedly fails hard questions:

\[
Hard\rightarrowMedium
\]

This creates an adaptive learning process.

### Exploration vs Exploitation

The system should also explore new topics occasionally.

For example:

- exploitation → provide topics known to help the student;
- exploration → test whether another topic or difficulty level produces better learning.

However, excessive exploration could frustrate the student.

### Final Answer

The student's knowledge and engagement form the state, educational content/difficulty forms the action, and learning improvement and engagement form the reward. The RL agent learns a policy that dynamically selects appropriate educational content based on the student's changing state.

---

# Q4. Healthcare Treatment Optimization

> **Problem Statement:** Design an RL agent that suggests personalized treatment plans for patients with chronic conditions, such as diabetes, by continuously learning from patient data, treatment outcomes, and evolving medical research.

## Solution

This can be formulated as a sequential decision-making problem.

### State Space

The state can include:

- blood glucose levels;
- previous treatment;
- treatment response;
- patient history;
- symptoms;
- lifestyle information;
- relevant clinical measurements.

For example:

\[
s_t=
(\text{glucose},
\text{treatment history},
\text{response},
\text{clinical state},
\ldots)
\]

### Action Space

Possible actions might include:

- maintain current treatment;
- adjust treatment;
- recommend an approved lifestyle intervention;
- schedule additional monitoring.

In a real medical system, the action space must be restricted to clinically approved possibilities.

### Reward Function

The reward should balance health improvement with side effects and treatment cost.

A generic formulation is:

\[
R=
w_h(\text{health improvement})
-w_s(\text{side effects})
-w_c(\text{cost})
\]

The reward should strongly penalize unsafe outcomes.

### Learning Process

```text
Patient state
     ↓
Candidate treatment
     ↓
Observed response
     ↓
Health outcome
     ↓
Reward
     ↓
Policy/value update
```

### Why RL is Suitable

Treatment is sequential.

A decision made today can affect:

- future health;
- future treatment response;
- future side effects.

Therefore, the objective is not merely to maximize immediate improvement.

The RL objective is:

\[
\max_\pi E_\pi
\left[
\sum_t\gamma^tR_{t+1}
\right]
\]

which considers long-term outcomes.

### Safety

Healthcare is a high-risk environment.

The agent should **not** be allowed unrestricted exploration.

Appropriate safeguards include:

- hard medical constraints;
- clinician approval;
- offline training using historical data;
- simulation before deployment;
- restricted action space;
- monitoring and intervention mechanisms.

### Ethical Considerations

Important issues include:

#### Patient safety

Incorrect exploration can cause harm.

#### Bias

If historical data contains demographic or treatment bias, the learned policy may reproduce it.

#### Privacy

Patient data must be protected.

#### Explainability

Healthcare professionals may need to understand why a recommendation was produced.

#### Accountability

There must be clear responsibility for decisions made with AI assistance.

### Final Answer

The patient's clinical state forms the state, treatment decisions form the action, and long-term health outcomes form the reward. The RL agent can learn from treatment-response data to improve sequential decision-making, but healthcare requires strict safety constraints, restricted exploration and human/clinical oversight.

# Unit 4 — Problems 1

## Source PDFs

- [RL CSAI Sample Questions](pdfs/RL%20CSAI%20Sample%20questions%20%283%29.pdf)
- [RL Question Bank](pdfs/QUESTIONS%20_rl%20%282%29.pdf)

---

# Q5. Frozen Lake Navigation

> The agent must learn to navigate across a frozen lake from a starting point to a goal, avoiding falling into holes. This problem is a classic example of a discrete state and action space, ideal for introducing Q-learning. Use the Q-learning algorithm to find the best action in each state. The environment provides a reward of 1 if the agent reaches the goal and 0 otherwise.

## Solution

Q-learning updates the action-value function using:

\[
Q(s,a)\leftarrow Q(s,a)+
\alpha
\left[
r+\gamma\max_{a'}Q(s',a')-Q(s,a)
\right]
\]

The procedure is:

1. Initialize all \(Q(s,a)\) values.
2. Observe the current state \(s\).
3. Select an action \(a\), normally using an \(\epsilon\)-greedy policy.
4. Execute the action.
5. Observe reward \(r\) and next state \(s'\).
6. Update \(Q(s,a)\).
7. Repeat until the episode terminates.
8. After sufficient training, select:

\[
a^*=\arg\max_a Q(s,a)
\]

for every state.

### Reward structure

For reaching the goal:

\[
r=1
\]

For other transitions:

\[
r=0
\]

Therefore, the positive Q-value originating at the goal gradually propagates backward through states that lead toward it.

### Important limitation of the question

The question does **not** provide:

- the Frozen Lake map,
- the locations of holes,
- transition probabilities,
- \(\alpha\),
- \(\gamma\),
- or a trained Q-table.

Therefore, a specific action for every state cannot be numerically calculated from the supplied information.

The correct answer is to describe the Q-learning procedure and state that the optimal action is:

\[
\boxed{a^*=\arg\max_a Q(s,a)}
\]

---

# Q6. Understanding Rewards and Actions

> An RL agent is navigating a grid world, a simple environment used for demonstration purposes. The grid is 4x4, and the agent starts in the top left corner (0,0) and must reach the bottom right corner (3,3) to maximize its cumulative reward. The actions it can take at any state are to move up, down, left, or right. Moving into a wall keeps the agent in the same place. The agent receives a reward of -1 for each action taken and +10 for reaching the goal. If the agent takes a path right, right, down, down, down, right, calculate the total cumulative reward. Discuss how changing the reward for reaching the goal to +20 would affect the agent's learning.

## Solution

The path is:

\[
Right,Right,Down,Down,Down,Right
\]

Starting from:

\[
(0,0)
\]

the states are:

\[
(0,0)
\rightarrow
(0,1)
\rightarrow
(0,2)
\rightarrow
(1,2)
\rightarrow
(2,2)
\rightarrow
(3,2)
\rightarrow
(3,3)
\]

The agent takes six actions.

The first five transitions have reward:

\[
-1
\]

The final transition reaches the goal and gives:

\[
+10
\]

Therefore:

\[
G=(-1)+(-1)+(-1)+(-1)+(-1)+10
\]

\[
G=-5+10
\]

\[
\boxed{G=5}
\]

### If the goal reward becomes +20

The first five penalties remain:

\[
-5
\]

The goal reward becomes:

\[
+20
\]

Therefore:

\[
G=-5+20
\]

\[
\boxed{G=15}
\]

### Effect on learning

Increasing the goal reward makes reaching the goal more valuable.

Therefore, Q-values associated with actions that eventually lead to the goal will receive stronger positive updates.

The agent gets a stronger incentive to reach the goal.

\[
\boxed{\text{Higher goal reward} \Rightarrow \text{stronger incentive to reach the goal}}
\]

---

# Q7. Discount Factor in Future Rewards

> Consider the same grid world. Now, introduce a discount factor (γ) that determines the importance of future rewards. A common value for γ is 0.9. Assume the agent takes the following actions: right, right, down, down, right, and then reaches the goal. Calculate the total cumulative reward for the agent using a discount factor of 0.9. Explain the effect of changing the discount factor to 0.99 on the agent's strategy.

## Solution

The supplied question states that the agent takes:

\[
Right,Right,Down,Down,Right
\]

and then reaches the goal.

There is an ambiguity here: from \((0,0)\), these five movements reach \((2,3)\), not \((3,3)\).

Therefore, to actually reach the stated goal \((3,3)\), one additional `Down` action is required.

Using the stated grid-world reward structure, the rewards are:

\[
-1,-1,-1,-1,-1,+10
\]

The discounted return is:

\[
G=
-1
+0.9(-1)
+0.9^2(-1)
+0.9^3(-1)
+0.9^4(-1)
+0.9^5(10)
\]

Calculate:

\[
G=-1-0.9-0.81-0.729-0.6561+5.9049
\]

Therefore:

\[
\boxed{G=1.8098}
\]

### If γ = 0.99

\[
G=
-1
-0.99
-0.99^2
-0.99^3
-0.99^4
+10(0.99)^5
\]

\[
\boxed{G\approx3.8049}
\]

### Effect of increasing γ

Increasing:

\[
\gamma:0.9\rightarrow0.99
\]

makes future rewards less heavily discounted.

Therefore, the agent gives greater importance to future rewards and becomes more long-term oriented.

---

# Q8. Exploration vs Exploitation Trade-off

> An RL agent is playing a slot machine with two levers. Lever A returns a reward of 1 with a probability of 0.5, and Lever B returns a reward of 2 with a probability of 0.2. The agent has a policy to explore (choose randomly) 20% of the time and exploit (choose the best lever based on past experience) 80% of the time. If the agent pulls a lever 100 times, estimate the expected total reward. Discuss how the agent's total expected reward might change if it explores 50% of the time and exploits 50% of the time.

## Solution

### Step 1 — Expected reward of Lever A

\[
E[A]=1(0.5)
\]

\[
\boxed{E[A]=0.5}
\]

### Step 2 — Expected reward of Lever B

\[
E[B]=2(0.2)
\]

\[
\boxed{E[B]=0.4}
\]

Therefore:

\[
A>B
\]

in expected reward.

---

## Case 1: 20% exploration, 80% exploitation

Out of 100 pulls:

\[
20
\]

are exploration pulls.

Assuming exploration means choosing randomly between the two levers:

\[
E[R_{\text{explore}}]
=
\frac{0.5+0.4}{2}
=0.45
\]

Therefore:

\[
20(0.45)=9
\]

The remaining:

\[
80
\]

pulls are exploitation pulls.

Since A is better:

\[
80(0.5)=40
\]

Total:

\[
9+40
\]

\[
\boxed{49}
\]

---

## Case 2: 50% exploration, 50% exploitation

Exploration:

\[
50(0.45)=22.5
\]

Exploitation:

\[
50(0.5)=25
\]

Total:

\[
22.5+25
\]

\[
\boxed{47.5}
\]

### Comparison

| Strategy | Expected total reward |
|---|---:|
| 20% explore / 80% exploit | **49** |
| 50% explore / 50% exploit | **47.5** |

Increasing exploration reduces the immediate expected reward under the assumptions given.

However, exploration is useful because the agent may initially not know which lever is better.

### Exam point

> Exploration sacrifices some short-term reward to obtain information that may improve future decisions.

---

# Q9. Discount Factor in Future Rewards

> Consider the same grid world. Now, introduce a discount factor (γ) that determines the importance of future rewards. A common value for γ is 0.9. Assume the agent takes the following actions: right, right, down, down, right, and then reaches the goal.  
> 1. Calculate the total cumulative reward for the agent using a discount factor of 0.9.  
> 2. Explain the effect of changing the discount factor to 0.99 on the agent's strategy.

## Solution

This is the same problem as Q7 in the supplied PDF.

Again, the stated five movements do not reach \((3,3)\) from \((0,0)\). One additional Down movement is required.

Using:

\[
-1,-1,-1,-1,-1,+10
\]

we obtain:

\[
G=
-1
-0.9
-0.81
-0.729
-0.6561
+10(0.9)^5
\]

\[
\boxed{G=1.8098}
\]

For:

\[
\gamma=0.99
\]

\[
G=
-1
-0.99
-0.9801
-0.970299
-0.96059601
+10(0.99)^5
\]

\[
\boxed{G\approx3.8049}
\]

Increasing \(\gamma\) makes future rewards more important and therefore encourages more long-term decision-making.

---

# Q10. Exploration vs Exploitation Trade-off

> An RL agent is playing a slot machine with two levers. Lever A returns a reward of 1 with a probability of 0.5, and Lever B returns a reward of 2 with a probability of 0.2. The agent has a policy to explore (choose randomly) 20% of the time and exploit (choose the best lever based on past experience) 80% of the time. If the agent pulls a lever 100 times, estimate the expected total reward. Discuss how the agent's total expected reward might change if it explores 50% of the time and exploits 50% of the time.

## Solution

This is a duplicate of Q8 in the supplied PDF.

\[
E[A]=0.5
\]

\[
E[B]=0.4
\]

Therefore A is the better lever.

### 20% exploration

\[
20(0.45)+80(0.5)
\]

\[
=9+40
\]

\[
\boxed{49}
\]

### 50% exploration

\[
50(0.45)+50(0.5)
\]

\[
=22.5+25
\]

\[
\boxed{47.5}
\]

Thus, under the assumptions of the question:

\[
\boxed{49>47.5}
\]

Higher exploration lowers immediate expected reward, but may provide useful information about the environment.


