# Solutions — Class Assignment on DRL

## Source PDF

[Open Real (1).pdf](pdfs/Real%20%281%29.pdf)

---

# Q1. Real-World Case of Prioritized Experience Replay in DRL

> Imagine training a robot to navigate a maze. The robot has to learn the correct policy by interacting with the environment. Most of the experiences might be unimportant, such as the robot moving around without getting closer to the goal, but occasionally it may take a crucial action that brings it close to the goal.
>
> Explain how Prioritized Experience Replay can improve learning in this situation.

## Solution

In ordinary experience replay, experiences are sampled approximately uniformly.

This means that an important transition and an unimportant transition can have similar probabilities of being selected.

For maze navigation, this is inefficient because most experiences may contain little new information.

---

## Prioritized Experience Replay

PER assigns a priority to each experience according to its TD error.

A common priority is:

\[
p_i=|\delta_i|^\alpha
\]

where:

- \(\delta_i\) = TD error;
- \(\alpha\) = priority exponent.

The sampling probability is:

\[
\boxed{
P(i)=
\frac{p_i}{\sum_jp_j}
}
\]

---

## Application to the maze

Suppose the robot normally moves around without making meaningful progress.

These transitions generally have relatively small TD errors.

A transition that suddenly brings the robot close to the goal may have a large TD error.

Therefore:

\[
|\delta_{\text{important}}|
>
|\delta_{\text{ordinary}}|
\]

and consequently:

\[
P(\text{important experience})
>
P(\text{ordinary experience})
\]

---

## Learning process

```text
Robot interacts with maze
          ↓
Store experiences
          ↓
Calculate TD errors
          ↓
Assign priorities
          ↓
Sample high-priority experiences more often
          ↓
Update neural network
          ↓
Improved navigation policy
```

---

## Why PER helps

### 1. Faster learning

Important experiences are replayed more frequently.

### 2. Better sample efficiency

The agent extracts more information from informative transitions.

### 3. Rare events receive attention

A rare successful or highly surprising transition is less likely to be ignored.

---

## Drawback

Prioritized sampling introduces bias because the replay distribution is no longer uniform.

Importance-sampling weights can be used to compensate for this bias.

### Exam conclusion

> PER improves learning by replaying experiences with large TD errors more frequently. In maze navigation, crucial transitions that move the robot toward the goal can therefore influence learning much more strongly than routine movements.

---

# Q2. DQN — Autonomous Traffic Light Control System

> In a smart city, traffic lights need to adapt dynamically to real-time traffic conditions to minimize congestion and travel time. Design a DQN solution.

## Solution

DQN can learn a traffic-light control policy by observing traffic conditions and selecting the traffic-light phase that maximizes long-term reward.

---

## State

The state should represent the current traffic situation.

For example:

\[
s=
(\text{vehicles per lane},
\text{waiting times},
\text{traffic density})
\]

Possible state information:

- number of vehicles in each lane;
- average waiting time;
- queue length;
- current traffic-light phase;
- traffic density.

---

## Actions

The actions represent possible traffic-light states.

For example:

\[
A=
\{
\text{North-South green},
\text{East-West green},
\text{yellow},
\text{etc.}
\}
\]

The exact action set depends on the intersection.

---

## Reward

The objective is to reduce congestion and waiting time.

A suitable reward could be:

\[
\boxed{
R=
-\lambda_1(\text{waiting time})
-\lambda_2(\text{queue length})
}
\]

A reduction in congestion therefore produces a less negative or positive reward.

---

## DQN learning

The agent interacts with a traffic simulation.

At each step:

1. observe traffic state \(s\);
2. choose traffic-light action \(a\);
3. execute action;
4. receive reward \(r\);
5. observe \(s'\);
6. store transition;
7. train DQN.

The Q-learning target is:

\[
y=
r+\gamma
\max_{a'}
Q_{\text{target}}(s',a')
\]

The online network is trained toward this target.

---

## Why DQN?

Traffic conditions are dynamic.

A fixed rule such as:

> "Change the light every 60 seconds"

cannot adapt well to unusual traffic conditions.

DQN can learn different decisions for different traffic states.

---

## Limitation

The source specifically identifies overestimation bias as a limitation of DQN in complex traffic patterns.

A noisy Q-value estimate can cause the agent to select a non-optimal traffic-light policy.

Double DQN can be used to reduce this overestimation.

### Exam conclusion

> DQN can dynamically control traffic lights by mapping traffic states to traffic-light actions and learning from congestion-related rewards.

---

# Q3. Double DQN — Stock Trading Bot

> Design a Double DQN solution for algorithmic stock trading in a volatile market.

## Solution

Stock markets are noisy and uncertain.

Standard DQN can overestimate Q-values because of the maximum operation.

Double DQN reduces this problem by separating action selection from action evaluation.

---

## State

The state can contain:

- current stock price;
- moving averages;
- trading volume;
- other market indicators.

For example:

\[
s=
(\text{price},
\text{moving average},
\text{volume},
\ldots)
\]

---

## Actions

The source specifies:

\[
A=
\{
\text{Buy},
\text{Sell},
\text{Hold}
\}
\]

---

## Reward

The reward can represent profit or loss:

\[
\boxed{
R=\text{profit/loss from action}
}
\]

A profitable trade gives positive reward.

A loss gives negative reward.

---

## Why Double DQN?

Standard DQN uses:

\[
y=
r+
\gamma
\max_{a'}
Q_{\text{target}}(s',a')
\]

The maximum can select an overestimated Q-value.

Double DQN performs:

### Step 1 — action selection

Use the online network:

\[
\boxed{
a^*=
\arg\max_{a'}
Q_{\text{online}}(s',a')
}
\]

### Step 2 — action evaluation

Use the target network:

\[
\boxed{
y=
r+
\gamma
Q_{\text{target}}(s',a^*)
}
\]

Thus:

\[
\boxed{\text{Online selects, target evaluates}}
\]

---

## Benefit

The trading system is less likely to treat a noisy overestimated Q-value as reliable.

This can prevent overly optimistic trading decisions.

---

## Exam conclusion

> Double DQN is suitable for volatile trading environments because it reduces Q-value overestimation by decoupling action selection from action evaluation.

---

# Q4. Dueling DQN — Autonomous Drone Navigation

> Design a Dueling DQN solution for an autonomous drone navigating an unknown environment while avoiding obstacles and reaching a target.

## Solution

A drone needs to determine both:

1. how good the current state is;
2. which action is better in that state.

Dueling DQN separates these two concepts.

---

## State

The source specifies:

- current location;
- distance to obstacles;
- distance to goal.

Therefore:

\[
s=
(\text{location},
\text{obstacle distances},
\text{goal distance})
\]

---

## Actions

Possible actions:

\[
A=
\{
\text{forward},
\text{left},
\text{right},
\text{hover}
\}
\]

---

## Reward

The source specifies:

- positive reward for moving closer to the target;
- penalty for collisions.

A possible reward is:

\[
R=
w_1(\text{progress})
-w_2(\text{collision})
\]

where:

\[
w_2\gg w_1
\]

for strong safety enforcement.

---

## Dueling architecture

Instead of directly learning only \(Q(s,a)\), the network estimates:

\[
V(s)
\]

and:

\[
A(s,a)
\]

Then:

\[
\boxed{
Q(s,a)
=
V(s)+
A(s,a)
-
\frac{1}{|\mathcal A|}
\sum_{a'}A(s,a')
}
\]

---

## Why useful for the drone?

Consider a state where the drone is far away from obstacles.

Several actions may have nearly identical immediate consequences.

The important information is:

\[
\boxed{\text{This is a safe/good state}}
\]

rather than tiny differences between actions.

The value stream can learn:

\[
V(s)
\]

while the advantage stream learns which action is better.

---

## Architecture

```text
                  State
                    |
                    v
              Shared network
                    |
             +------+------+
             |             |
             v             v
           V(s)          A(s,a)
             |             |
             +------+------+
                    |
                    v
                  Q(s,a)
```

### Exam conclusion

> Dueling DQN improves learning by separately estimating state value and action advantage. This is particularly useful when several actions have similar effects in a given state.

---

# Q5. DQN — Robot Path Planning in Warehouses

> Autonomous robots in warehouses need to find short and safe paths to shelves while avoiding collisions with other robots and obstacles. Design a DQN solution.

## Solution

---

## State

The state contains:

- robot position;
- nearby obstacles;
- target location.

Therefore:

\[
s=
(\text{robot position},
\text{obstacles},
\text{target})
\]

---

## Actions

The source specifies:

\[
A=
\{
\text{move forward},
\text{turn left},
\text{turn right},
\text{stop}
\}
\]

---

## Reward

The source specifies:

- positive reward for reaching the target quickly;
- penalty for collisions;
- penalty for taking too long.

A suitable reward can be:

\[
\boxed{
R=
R_{\text{goal}}
-R_{\text{collision}}
-R_{\text{time}}
}
\]

with:

\[
R_{\text{collision}}
\]

large enough to discourage dangerous paths.

---

## DQN process

```text
Observe warehouse
       ↓
Construct state
       ↓
DQN chooses movement
       ↓
Robot moves
       ↓
Receive reward
       ↓
Store experience
       ↓
Replay and train
       ↓
Improved path planning
```

---

## Objective

The learned policy should maximize:

\[
\mathbb E
\left[
\sum_t\gamma^tr_t
\right]
\]

Therefore it should learn paths that are:

- short;
- safe;
- collision-free.

### Exam conclusion

> DQN can learn warehouse navigation by mapping robot/obstacle/target states to movement actions and rewarding fast, collision-free movement toward the target.

---

# Q6. Double DQN — Autonomous Taxi Dispatch System

> Design a Double DQN solution for assigning taxis to customer requests while minimizing waiting time and maximizing profit.

## Solution

---

## State

The state contains:

- locations of available taxis;
- locations of customers;
- time of day;
- potentially current demand.

\[
s=
(\text{taxi locations},
\text{customer locations},
\text{time})
\]

---

## Actions

The agent can:

- assign a particular taxi;
- delay dispatch.

Thus:

\[
A=
\{\text{taxi assignment actions},\text{delay}\}
\]

---

## Reward

The source specifies positive reward for:

- minimizing waiting time;
- maximizing profit.

A suitable objective is:

\[
\boxed{
R=
w_p(\text{profit})
-w_w(\text{waiting time})
}
\]

---

## Why Double DQN?

Taxi demand is dynamic and noisy.

Standard DQN can overestimate Q-values.

Double DQN separates:

\[
\text{action selection}
\]

from:

\[
\text{action evaluation}
\]

using online and target networks.

\[
a^*=
\arg\max_aQ_{\text{online}}(s',a)
\]

\[
y=
r+\gamma Q_{\text{target}}(s',a^*)
\]

---

## Result

The system can learn assignments that balance:

\[
\boxed{
\text{customer waiting time}
\leftrightarrow
\text{driver utilization}
\leftrightarrow
\text{profit}
}
\]

### Exam conclusion

> Double DQN is useful because dispatch decisions are made in a dynamic and uncertain environment where inaccurate Q-value estimates can produce poor assignments.

---

# Q7. Dueling DQN — Online Video Streaming Quality Optimization

> Design a Dueling DQN system that dynamically adjusts video quality according to changing network conditions while avoiding buffering.

## Solution

---

## State

The source specifies:

- current bandwidth;
- buffer size;
- current video bitrate.

Therefore:

\[
s=
(\text{bandwidth},
\text{buffer},
\text{bitrate})
\]

---

## Actions

\[
A=
\{
\text{increase quality},
\text{decrease quality},
\text{maintain quality}
\}
\]

---

## Reward

The system should reward high quality without buffering.

A possible reward is:

\[
\boxed{
R=
w_q(\text{video quality})
-w_b(\text{buffering})
}
\]

A large penalty should be assigned to buffering events.

---

## Why Dueling DQN?

There are states where the exact quality action is less important than the overall condition of the connection.

For example, if bandwidth is extremely low, the state itself is poor.

The network can learn:

\[
V(s)
\]

while separately learning:

\[
A(s,a)
\]

Then:

\[
Q(s,a)=
V(s)+
A(s,a)-\operatorname{mean}(A)
\]

---

## Benefit

The network can learn the general quality of a network state while determining which quality action is best.

### Exam conclusion

> Dueling DQN is appropriate because it separately learns the value of the current network state and the relative advantage of changing video quality.

---

# Q8. DQN — Energy Management in Smart Grids

> Design a DQN system that decides whether to store, release or purchase energy according to demand, supply, storage and market prices.

## Solution

---

## State

The state includes:

- energy demand;
- energy supply;
- storage level;
- market price.

\[
s=
(\text{demand},
\text{supply},
\text{storage},
\text{price})
\]

---

## Actions

\[
A=
\{
\text{store},
\text{release},
\text{buy}
\}
\]

---

## Reward

The objective is to satisfy demand at minimum cost.

Therefore:

\[
\boxed{
R=
-\text{energy cost}
-\text{unmet demand penalty}
}
\]

Meeting demand efficiently should produce a better reward.

---

## DQN learning

The agent observes:

\[
s_t
\]

and chooses:

\[
a_t
\]

The environment produces:

\[
r_t,s_{t+1}
\]

The transition:

\[
(s_t,a_t,r_t,s_{t+1})
\]

is stored in the replay buffer.

The DQN learns:

\[
Q(s,a)
\]

and ultimately selects:

\[
\boxed{
a^*=\arg\max_aQ(s,a)
}
\]

---

## Exam conclusion

> DQN can learn an adaptive energy-management policy that reacts to changing demand, supply, storage and market prices instead of relying on fixed rules.

---

# Q9. Double DQN — Self-Driving Car Lane Changing

> Design a Double DQN solution for safe and efficient lane-changing decisions considering traffic patterns, vehicle speeds and road conditions.

## Solution

---

## State

The source specifies:

- vehicle speed;
- distance to other vehicles;
- available lanes.

Therefore:

\[
s=
(\text{speed},
\text{vehicle distances},
\text{available lanes})
\]

Road conditions and surrounding traffic can also be represented in the state when available.

---

## Actions

\[
A=
\{
\text{change left},
\text{change right},
\text{stay}
\}
\]

---

## Reward

The source specifies:

- positive reward for smooth and safe lane changes;
- penalties for collisions;
- penalties for abrupt stops.

A suitable formulation is:

\[
\boxed{
R=
w_s(\text{safe smooth change})
-w_c(\text{collision})
-w_a(\text{abrupt stop})
}
\]

---

## Double DQN

The online network selects:

\[
\boxed{
a^*=
\arg\max_aQ_{\text{online}}(s',a)
}
\]

The target network evaluates it:

\[
\boxed{
y=
r+\gamma Q_{\text{target}}(s',a^*)
}
\]

This reduces the Q-value overestimation associated with standard DQN.

---

## Safety

Safety should be encoded strongly in the reward and, where possible, enforced using action constraints.

A collision should have a much larger negative reward than the small positive benefit from completing a faster lane change.

### Exam conclusion

> Double DQN can improve lane-change decisions by reducing Q-value overestimation, while a safety-focused reward discourages collisions and abrupt maneuvers.

---

# Q10. Dueling DQN — Personalized Advertising Recommendation

> Design a Dueling DQN system for personalized advertising that maximizes click-through rate and conversions while avoiding irrelevant advertisements.

## Solution

---

## State

The state contains:

- browsing history;
- user demographics;
- previous interactions.

Thus:

\[
s=
(\text{browsing history},
\text{demographics},
\text{past interactions})
\]

---

## Actions

The actions are:

\[
A=
\{
\text{recommend advertisement 1},
\text{recommend advertisement 2},
\ldots,
\text{no advertisement}
\}
\]

---

## Reward

The source specifies:

- positive reward for clicks;
- positive reward for conversions;
- penalty for irrelevant advertisements.

A suitable reward is:

\[
\boxed{
R=
w_c(\text{click})
+w_v(\text{conversion})
-w_i(\text{irrelevance})
}
\]

where:

\[
w_v>w_c
\]

if conversions are considered more valuable than clicks.

---

## Why Dueling DQN?

The network separates:

\[
V(s)
\]

from:

\[
A(s,a)
\]

The value stream estimates:

> How valuable is this user's current state?

The advantage stream estimates:

> Which advertisement is better for this user?

Then:

\[
\boxed{
Q(s,a)
=
V(s)+
A(s,a)-\operatorname{mean}_aA(s,a)
}
\]

---

## Example

If a user's current state indicates very high purchasing intent, the state itself may have high value.

The advantage stream can then distinguish between:

- advertisement A;
- advertisement B;
- no advertisement.

This allows the model to learn state quality separately from action preference.

---

## Exam conclusion

> Dueling DQN is useful for personalized recommendation because it separates the general value of the user's state from the relative advantage of individual advertising actions.

---

# Quick Revision Table

| Q | Application | Algorithm | Main reason |
|---|---|---|---|
| Q1 | Robot maze | PER | Replay important experiences |
| Q2 | Traffic lights | DQN | Adaptive traffic control |
| Q3 | Stock trading | Double DQN | Reduce overestimation |
| Q4 | Drone navigation | Dueling DQN | Separate \(V\) and \(A\) |
| Q5 | Warehouse robots | DQN | Path planning |
| Q6 | Taxi dispatch | Double DQN | Reliable Q estimates |
| Q7 | Video streaming | Dueling DQN | State value + action advantage |
| Q8 | Smart grid | DQN | Dynamic energy management |
| Q9 | Lane changing | Double DQN | Reduce Q overestimation |
| Q10 | Advertising | Dueling DQN | User-state value + ad advantage |

---

# Important Formulas

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
Q(s,a)
=
V(s)+
A(s,a)
-
\frac{1}{|\mathcal A|}
\sum_{a'}A(s,a')
}
\]

## Prioritized Experience Replay

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
