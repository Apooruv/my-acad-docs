# Bellman Equations

## 1. Why Bellman Equations?

A Bellman equation expresses the value of a state in terms of:

1. immediate reward
2. value of the next state

The key idea is:

\[
\boxed{
\text{Current value}
=
\text{Immediate reward}
+
\text{Discounted future value}
}
\]

This recursive structure is fundamental to RL.

---

# 2. Bellman Expectation Equation for V

For a policy \(\pi\):

\[
\boxed{
V^\pi(s)
=
\sum_a\pi(a|s)
\sum_{s'}P(s'|s,a)
\left[
R(s,a,s')+\gamma V^\pi(s')
\right]
}
\]

This is the **Bellman expectation equation**.

---

## 3. Deterministic Simplification

If:

- the policy chooses a fixed action \(a\)
- the transition is deterministic
- next state is \(s'\)

then:

\[
\boxed{
V^\pi(s)=R+\gamma V^\pi(s')
}
\]

This is the form most commonly used in simple numerical questions.

---

## 4. Example

Suppose:

\[
R=-1
\]

\[
\gamma=0.9
\]

\[
V(s')=5
\]

Then:

\[
V(s)=-1+0.9(5)
\]

\[
V(s)=-1+4.5
\]

\[
\boxed{V(s)=3.5}
\]

---

# 5. Bellman Expectation Equation for Q

The action-value form is:

\[
\boxed{
Q^\pi(s,a)
=
\sum_{s'}P(s'|s,a)
\left[
R(s,a,s')
+
\gamma
\sum_{a'}\pi(a'|s')Q^\pi(s',a')
\right]
}
\]

For deterministic transition and policy:

\[
\boxed{
Q^\pi(s,a)=R+\gamma Q^\pi(s',a')
}
\]

---

# 6. Bellman Optimality Equation

For the optimal value function:

\[
\boxed{
V^*(s)
=
\max_a
\sum_{s'}P(s'|s,a)
[
R(s,a,s')+\gamma V^*(s')
]
}
\]

The difference is the `max`.

### Bellman expectation

Follows a particular policy:

\[
V^\pi(s)
\]

### Bellman optimality

Chooses the best action:

\[
V^*(s)
\]

---

# 7. Bellman Optimality Equation for Q

The optimal Q-function satisfies:

\[
\boxed{
Q^*(s,a)
=
\sum_{s'}P(s'|s,a)
\left[
R(s,a,s')
+
\gamma\max_{a'}Q^*(s',a')
\right]
}
\]

For a deterministic environment:

\[
\boxed{
Q^*(s,a)
=
R+\gamma\max_{a'}Q^*(s',a')
}
\]

This equation is directly related to the Q-learning update.

---

# 8. Greedy Bellman Update

Suppose from state \(s\), four actions lead to states whose current values are:

\[
2.0,\quad1.0,\quad0.5,\quad3.0
\]

Suppose:

\[
R=-1,\qquad\gamma=0.9
\]

A greedy policy chooses the state with maximum value:

\[
\max(2.0,1.0,0.5,3.0)=3.0
\]

Therefore:

\[
V_{\text{new}}(s)
=
-1+0.9(3.0)
\]

\[
\boxed{V_{\text{new}}(s)=1.7}
\]

This exact pattern occurs in the supplied sample-question set.

---

# 9. Effect of Changing Gamma

Using the same example:

\[
R=-1
\]

\[
V(s')=3
\]

If:

\[
\gamma=0.99
\]

then:

\[
V(s)=-1+0.99(3)
\]

\[
=-1+2.97
\]

\[
\boxed{V(s)=1.97}
\]

Compared with:

\[
1.7
\]

for \(\gamma=0.9\).

### Interpretation

Increasing \(\gamma\):

- increases the importance of future rewards
- makes future state values contribute more strongly
- makes the agent more long-term oriented

---

# 10. Bellman Equation → Q-Learning

The Bellman optimality equation is:

\[
Q^*(s,a)
=
R+\gamma\max_{a'}Q^*(s',a')
\]

Q-learning does not immediately replace the current Q-value with the target.

Instead:

\[
\boxed{
Q(s,a)
\leftarrow
Q(s,a)
+
\alpha
[
\underbrace{
R+\gamma\max_{a'}Q(s',a')
}_{\text{target}}
-
Q(s,a)
]
}
\]

The difference between target and current estimate is the:

\[
\boxed{\text{TD Error}}
\]

\[
\delta=
R+\gamma\max_{a'}Q(s',a')-Q(s,a)
\]

---

# 11. Bellman Equation vs Q-Learning

| Bellman optimality | Q-learning |
|---|---|
| Uses the environment model | Model-free |
| Computes/updates values from known transitions | Learns from sampled experience |
| Uses expected transition outcomes | Uses observed transition |
| Gives the optimality target | Moves Q-values toward the target |

This distinction is important.

---

# 12. Policy Evaluation

For a fixed policy:

\[
\boxed{
V^\pi(s)
=
\sum_a\pi(a|s)
\sum_{s'}P(s'|s,a)
[R+\gamma V^\pi(s')]
}
\]

The goal is to calculate:

\[
\pi\rightarrow V^\pi
\]

This is called **policy evaluation**.

---

# 13. Policy Improvement

After obtaining \(V^\pi\), choose actions that maximize expected value:

\[
\boxed{
\pi'(s)
=
\arg\max_a
\sum_{s'}P(s'|s,a)
[R+\gamma V^\pi(s')]
}
\]

Thus:

\[
V^\pi
\rightarrow
\pi'
\]

If the new policy is better, continue.

---

# 14. Exam Checklist

When solving a Bellman numerical:

### Step 1

Identify the current state.

### Step 2

List possible next-state values.

### Step 3

Determine whether the question says:

- follow a policy → expectation
- choose greedily → maximum
- stochastic transition → weighted sum

### Step 4

Apply:

\[
R+\gamma V(s')
\]

or:

\[
R+\gamma\max_aQ(s',a)
\]

### Step 5

Substitute values carefully.

---

## Most Important Formulas

### Bellman expectation

\[
\boxed{
V^\pi(s)=
\sum_a\pi(a|s)
\sum_{s'}P(s'|s,a)
[R+\gamma V^\pi(s')]
}
\]

### Bellman optimality

\[
\boxed{
V^*(s)=
\max_a
\sum_{s'}P(s'|s,a)
[R+\gamma V^*(s')]
}
\]

### Q optimality

\[
\boxed{
Q^*(s,a)=
\sum_{s'}P(s'|s,a)
[R+\gamma\max_{a'}Q^*(s',a')]
}
\]

### Q-learning

\[
\boxed{
Q(s,a)\leftarrow
Q(s,a)+
\alpha[
R+\gamma\max_{a'}Q(s',a')-Q(s,a)
]
}
\]

