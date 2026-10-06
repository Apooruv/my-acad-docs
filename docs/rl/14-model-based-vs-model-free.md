# Model-Based vs Model-Free Reinforcement Learning

## 1. Model-Based Reinforcement Learning

A model-based RL method uses or learns a model of the environment.

The model describes:

\[
P(s'|s,a)
\]

and potentially:

\[
R(s,a,s')
\]

The agent can then use the model to predict future outcomes.

```text
State + Action
      ↓
Environment Model
      ↓
Predicted next state + reward
      ↓
Planning
      ↓
Action
```

---

## 2. Model-Free Reinforcement Learning

A model-free method does not explicitly learn the transition dynamics of the environment.

Instead, it directly learns:

- value functions
- Q-values
- policies

Examples in this syllabus:

- Q-learning
- SARSA
- DQN

```text
Experience
    ↓
Value / Policy
    ↓
Action
```

---

# 3. Main Difference

### Model-Based

Learns:

\[
\text{How does the environment behave?}
\]

Then uses that model for planning.

### Model-Free

Learns:

\[
\text{Which actions are good?}
\]

without explicitly modelling the environment.

---

# 4. Comparison

| Feature | Model-Based | Model-Free |
|---|---|---|
| Environment model | Required/learned | Not explicitly required |
| Planning | Yes | Usually no explicit planning |
| Sample efficiency | Often better | Can require more experience |
| Model error | Important issue | Avoids explicit model error |
| Complexity | Higher | Usually simpler |
| Examples | Dyna-Q | Q-learning, SARSA, DQN |

---

# 5. Dyna-Q

Dyna-Q combines:

1. Real interaction
2. Model learning
3. Q-learning
4. Planning using simulated experience

Conceptually:

```text
                 Real Environment
                       │
                       ▼
                  Experience
                  /         \
                 /           \
                ▼             ▼
          Update Q        Learn Model
                              │
                              ▼
                         Simulated
                         Experience
                              │
                              ▼
                          Update Q
```

The supplied material explicitly describes Dyna-Q as combining model-based planning with model-free value learning. L6 (3)

---

# 6. Dyna-Q Process

During real interaction:

\[
(s,a,r,s')
\]

is observed.

This experience is used for:

### Q update

Update the Q-function from the real transition.

### Model update

Store/learn:

\[
(s,a)\rightarrow(r,s')
\]

Then planning steps sample previously observed state-action pairs from the learned model.

The model generates simulated experience:

\[
(s,a,\hat r,\hat s')
\]

and Q-learning is applied to that simulated experience.

---

# 7. Why Use Planning?

Suppose the agent has only experienced one real transition:

\[
A\rightarrow B
\]

Without planning:

```text
1 real experience
→ 1 direct learning update
```

With Dyna-Q:

```text
1 real experience
      ↓
learn model
      ↓
simulate it multiple times
      ↓
multiple Q updates
```

Thus, a small amount of real experience can be reused.

---

# 8. Advantages of Dyna-Q

### 1. Better sample efficiency

Real experiences can be reused through simulated planning.

### 2. Combines learning and planning

It obtains benefits from both approaches.

### 3. Faster propagation of information

A reward discovered through real interaction can affect several simulated updates.

---

# 9. Disadvantages

The supplied deep-RL material highlights a major issue:

> **Compounding model errors.** L6 (3)

Suppose the learned model predicts:

\[
A\rightarrow B
\]

but the real environment is:

\[
A\rightarrow C
\]

Planning using an incorrect model can reinforce incorrect Q-values.

The problem becomes worse when many simulated transitions are chained together.

```text
Model error
    ↓
Incorrect next state
    ↓
Another prediction based on wrong state
    ↓
More error
    ↓
Compounding error
```

---

# 10. Model-Based vs Dyna-Q

Dyna-Q is particularly useful for understanding the distinction.

It contains both:

### Model-free component

\[
Q(s,a)
\]

### Model-based component

\[
\hat P(s'|s,a),\hat R(s,a)
\]

Therefore:

> Dyna-Q is a hybrid architecture combining model-free learning with model-based planning.

---

# 11. Question: Dyna-Q

### Question

> Explain how the Dyna-Q framework utilizes simulated experiences to improve learning efficiency. What are the benefits of adding simulated planning steps, and how does it differ conceptually from pure model-free approaches?

### Answer

Dyna-Q learns a model of the environment from real experience and uses that model to generate simulated transitions. These simulated experiences are then used to update the Q-function in additional planning steps.

This allows each real interaction to produce multiple learning updates, improving sample efficiency and speeding up value propagation.

In a pure model-free approach such as Q-learning, the agent directly updates its Q-values from real experience without explicitly learning a transition model for planning. Dyna-Q adds a model-based planning component.

Its main limitation is that errors in the learned model can produce incorrect simulated experiences, and these errors can compound over long planning trajectories. L6 (3)

---

# 12. Exam Comparison

| Method | Learns model? | Uses planning? | Learns Q/policy? |
|---|---:|---:|---:|
| Q-learning | No | No | Yes |
| SARSA | No | No | Yes |
| Model-based RL | Yes | Yes | Usually |
| Dyna-Q | Yes | Yes | Yes |
| DQN | No explicit environment model | No | Yes |

---

# 13. Important Distinction

Do not confuse:

### Model-free

> "I don't need to know how the world works. I learn which actions work."

with:

### Model-based

> "I learn/predict how the world changes, then use that prediction for planning."

---

# 14. Exam Definition

> **Model-free RL learns values or policies directly from experience without explicitly modelling environment dynamics, whereas model-based RL uses a known or learned environment model to predict outcomes and perform planning.**

---

# 15. Unit 4 Connection

The complete progression is:

```text
MDP
 ↓
Bellman Equation
 ↓
Policy Evaluation
 ↓
Policy Iteration
 ↓
Passive Learning
 ├── Direct Utility Estimation
 ├── Monte Carlo
 └── TD
       ↓
Active Learning
 ├── Q-Learning
 └── SARSA
       ↓
Model-Based / Model-Free
       ↓
Dyna-Q
```

This progression is useful for remembering how the algorithms relate to each other.