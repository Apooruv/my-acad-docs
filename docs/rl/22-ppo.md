# Unit 5 — Proximal Policy Optimization (PPO)

## Source PDFs

- [Deep RL Tutorial](pdfs/Deep-RL-Tutorial%20%281%29.pdf)
- [L6 — Reinforcement Learning](pdfs/L6%20%283%29.pdf)
- [RL Question Bank](pdfs/QUESTIONS%20_rl%20%282%29.pdf)

> **Syllabus note:** PPO is explicitly included in Unit 5 of the syllabus.
> The supplied lecture PDFs do not provide a dedicated PPO treatment, so this
> section covers the syllabus-required PPO concepts directly.

---

# 1. What is PPO?

PPO stands for:

\[
\boxed{\text{Proximal Policy Optimization}}
\]

PPO is a **policy-gradient / actor-critic reinforcement learning algorithm**.

Its main objective is:

\[
\boxed{
\text{Improve the policy without allowing each update to change it too much}
}
\]

The word **proximal** means:

\[
\boxed{\text{close to the old policy}}
\]

PPO prevents the new policy from moving too far away from the old policy during an update.

---

# 2. Why is PPO Needed?

Policy-gradient methods directly optimize the policy.

A basic policy-gradient update is:

\[
\nabla_\theta J(\theta)
=
E[
A_t\nabla_\theta\log\pi_\theta(a_t|s_t)
]
\]

where:

- \(\theta\) = policy parameters;
- \(\pi_\theta(a|s)\) = policy;
- \(A_t\) = advantage;
- \(s_t\) = current state;
- \(a_t\) = selected action.

The problem is that a large gradient update can change the policy drastically.

For example:

```text
Old Policy
    |
    | large update
    ▼
New Policy
```

The new policy may become very different from the policy that generated the collected data.

This can result in:

- unstable learning;
- poor performance;
- destructive policy updates;
- large fluctuations in training.

PPO addresses this by restricting how much the policy can change.

---

# 3. Main Idea of PPO

PPO compares:

\[
\boxed{
\text{New policy}
}
\]

with:

\[
\boxed{
\text{Old policy}
}
\]

and discourages excessively large changes.

The central quantity is the probability ratio:

\[
\boxed{
r_t(\theta)
=
\frac{\pi_\theta(a_t|s_t)}
{\pi_{\theta_{\text{old}}}(a_t|s_t)}
}
\]

where:

- numerator = probability under the new policy;
- denominator = probability under the old policy.

---

# 4. Interpreting the Probability Ratio

Consider:

\[
r_t(\theta)=1
\]

Then:

\[
\pi_\theta(a_t|s_t)
=
\pi_{\theta_{\text{old}}}(a_t|s_t)
\]

So the policy has not changed for that action.

---

If:

\[
r_t>1
\]

the new policy gives the action a higher probability.

---

If:

\[
r_t<1
\]

the new policy gives the action a lower probability.

Therefore:

\[
\boxed{
r_t
\text{ measures how much the action probability changed}
}
\]

---

# 5. Advantage Function

PPO uses the advantage function to determine whether an action was better or worse than expected.

\[
\boxed{
A(s,a)=Q(s,a)-V(s)
}
\]

where:

- \(Q(s,a)\) = value of taking action \(a\);
- \(V(s)\) = value of the state.

Interpretation:

### If:

\[
A(s,a)>0
\]

the action was better than expected.

Therefore:

\[
\boxed{\text{increase its probability}}
\]

### If:

\[
A(s,a)<0
\]

the action was worse than expected.

Therefore:

\[
\boxed{\text{decrease its probability}}
\]

---

# 6. PPO Clipping

The main innovation of PPO is the **clipped objective**.

The objective is:

\[
\boxed{
L^{CLIP}(\theta)
=
E_t
\left[
\min
\left(
r_t(\theta)A_t,
\operatorname{clip}(r_t(\theta),1-\epsilon,1+\epsilon)A_t
\right)
\right]
}
\]

where:

\[
\epsilon
\]

is the clipping parameter.

A common conceptual choice is:

\[
\epsilon\approx0.1\text{ to }0.2
\]

---

# 7. What Does Clipping Do?

Suppose:

\[
\epsilon=0.2
\]

Then the permitted ratio range is:

\[
[1-\epsilon,1+\epsilon]
\]

\[
=[0.8,1.2]
\]

Therefore:

```text
             PPO ratio
                 |
       +---------+---------+
       |                   |
     0.8                   1.2
       |                   |
   lower bound         upper bound
```

The objective does not allow the policy update to benefit indefinitely from moving outside this range.

---

# 8. Positive Advantage Case

Suppose:

\[
A_t>0
\]

The action was good.

PPO wants to increase:

\[
\pi(a_t|s_t)
\]

Therefore it wants:

\[
r_t>1
\]

But if:

\[
r_t>1+\epsilon
\]

the improvement is clipped.

For:

\[
\epsilon=0.2
\]

the ratio is clipped at:

\[
1.2
\]

Therefore:

\[
\boxed{
\text{Good action → increase probability, but not excessively}
}
\]

---

# 9. Negative Advantage Case

Suppose:

\[
A_t<0
\]

The action was bad.

PPO wants to decrease its probability.

Therefore:

\[
r_t<1
\]

But PPO prevents the update from pushing the probability down excessively.

With:

\[
\epsilon=0.2
\]

the lower boundary is:

\[
0.8
\]

Therefore:

\[
\boxed{
\text{Bad action → decrease probability, but not excessively}
}
\]

---

# 10. Why Does the min() Matter?

PPO uses:

\[
\min
\left(
r_tA_t,
\operatorname{clip}(r_t,1-\epsilon,1+\epsilon)A_t
\right)
\]

The `min` selects the more conservative objective.

Thus the algorithm does not receive additional benefit from making the policy change too large.

This is the core reason PPO is more stable than an unconstrained policy-gradient update.

---

# 11. PPO Example

Suppose:

\[
\pi_{\text{old}}(a|s)=0.5
\]

and the new policy gives:

\[
\pi_{\text{new}}(a|s)=0.6
\]

Then:

\[
r_t
=
\frac{0.6}{0.5}
=
1.2
\]

Suppose:

\[
A_t=2
\]

and:

\[
\epsilon=0.2
\]

Then:

\[
r_tA_t
=
1.2(2)
=
2.4
\]

The clipped ratio is:

\[
\operatorname{clip}(1.2,0.8,1.2)=1.2
\]

Therefore:

\[
1.2(2)=2.4
\]

So:

\[
\boxed{L^{CLIP}=2.4}
\]

The policy change is exactly at the permitted upper boundary.

---

# 12. Example of Excessive Policy Change

Suppose:

\[
\pi_{\text{old}}(a|s)=0.5
\]

and:

\[
\pi_{\text{new}}(a|s)=0.8
\]

Then:

\[
r_t=
\frac{0.8}{0.5}
=
1.6
\]

Suppose:

\[
A_t=2
\]

and:

\[
\epsilon=0.2
\]

Then:

\[
1+\epsilon=1.2
\]

so:

\[
\operatorname{clip}(1.6,0.8,1.2)=1.2
\]

The unclipped objective is:

\[
1.6(2)=3.2
\]

The clipped objective is:

\[
1.2(2)=2.4
\]

PPO chooses:

\[
\min(3.2,2.4)=2.4
\]

Therefore:

\[
\boxed{
\text{The excessive policy improvement is ignored}
}
\]

This is the key mechanism of PPO.

---

# 13. PPO Algorithm

The basic PPO procedure is:

### Step 1 — Collect experience

Use the current policy:

\[
\pi_{\theta_{\text{old}}}
\]

to interact with the environment.

Collect:

\[
(s_t,a_t,r_t,s_{t+1})
\]

---

### Step 2 — Estimate value

The Critic estimates:

\[
V(s_t)
\]

---

### Step 3 — Calculate advantage

Estimate:

\[
A_t
\]

A simple form is:

\[
A_t=Q(s_t,a_t)-V(s_t)
\]

---

### Step 4 — Calculate probability ratio

\[
r_t(\theta)
=
\frac{\pi_\theta(a_t|s_t)}
{\pi_{\theta_{\text{old}}}(a_t|s_t)}
\]

---

### Step 5 — Apply clipping

Calculate:

\[
L^{CLIP}
\]

using:

\[
\operatorname{clip}(r_t,1-\epsilon,1+\epsilon)
\]

---

### Step 6 — Update policy

Optimize the PPO objective.

---

### Step 7 — Update Critic

Train the value function to estimate state values accurately.

---

### Step 8 — Repeat

Collect fresh trajectories using the updated policy and repeat.

---

# 14. PPO Actor-Critic Structure

PPO is commonly implemented using an Actor-Critic architecture.

```text
                 State s
                    |
                    ▼
              Shared Network
                /       \
               /         \
              ▼           ▼
           Actor        Critic
             |             |
             ▼             ▼
       π(a | s)           V(s)
             |
             ▼
           Action
```

---

# 15. Role of Actor

The Actor represents:

\[
\boxed{
\pi_\theta(a|s)
}
\]

It determines the probability of selecting each action.

PPO updates the Actor while controlling how far its policy moves from the previous policy.

---

# 16. Role of Critic

The Critic estimates:

\[
\boxed{
V(s)
}
\]

It helps calculate the advantage:

\[
A(s,a)=Q(s,a)-V(s)
\]

Thus:

\[
\boxed{
\text{Actor decides; Critic evaluates}
}
\]

This is consistent with the supplied lecture's treatment of Advantage Actor-Critic, where the policy network and value network are updated using an advantage/TD-based learning signal. [Source: L6 — Reinforcement Learning]

---

# 17. PPO vs Vanilla Policy Gradient

| Feature | Vanilla Policy Gradient | PPO |
|---|---|---|
| Policy gradient | Yes | Yes |
| Direct policy optimization | Yes | Yes |
| Controls policy update size | Weakly | Yes |
| Probability ratio | Usually not central | Central |
| Clipped objective | No | Yes |
| Stability | Can be unstable | More stable |
| Large policy changes | Possible | Restricted |

---

# 18. PPO vs Actor-Critic

These are not exactly competing concepts.

Actor-Critic is a general architecture:

\[
\boxed{
\text{Actor}+\text{Critic}
}
\]

PPO is a policy-optimization algorithm that is commonly implemented using Actor-Critic.

Therefore:

\[
\boxed{
\text{PPO can use an Actor-Critic structure}
}
\]

The Critic estimates values, while PPO's clipped objective controls Actor updates.

---

# 19. PPO vs DQN

| PPO | DQN |
|---|---|
| Policy-based / actor-critic | Value-based |
| Learns policy directly | Learns Q-values |
| Naturally supports stochastic policies | Usually selects max-Q action |
| Uses policy ratio | Uses Bellman target |
| Uses advantage/value estimate | Uses Q-value |
| Can naturally handle continuous actions | Standard DQN is designed for discrete actions |
| Uses policy updates | Uses Q-function updates |

---

# 20. Advantages of PPO

## 1. Stable policy updates

Clipping prevents excessively large policy changes.

## 2. Relatively simple

PPO avoids the more complicated constrained optimization associated with strict trust-region methods.

## 3. Good practical performance

It is widely useful for policy optimization.

## 4. Works naturally with stochastic policies

The policy can output action probabilities/distributions.

## 5. Actor-Critic compatible

The Critic provides advantage estimates that guide policy updates.

---

# 21. Disadvantages of PPO

## 1. Multiple samples may be required

PPO is generally an on-policy method, so old experience cannot be reused indefinitely after the policy changes.

## 2. Hyperparameter sensitivity

Performance depends on parameters such as:

- learning rate;
- clipping parameter \(\epsilon\);
- batch size;
- number of epochs;
- discount factor.

## 3. Computational cost

New trajectories generally need to be collected as the policy changes.

## 4. Clipping can limit useful updates

If updates are too aggressively clipped, learning may become slow.

---

# 22. PPO Clipping — Exam Explanation

If asked:

> **Why does PPO use clipping?**

Write:

> PPO clips the probability ratio between the new and old policies so that the policy cannot change excessively in a single update. This prevents destructive policy updates and improves training stability.

Formula:

\[
\boxed{
L^{CLIP}
=
E[
\min(
r_tA_t,
\operatorname{clip}(r_t,1-\epsilon,1+\epsilon)A_t
)
]
}
\]

---

# 23. PPO — Most Important Formula

Memorize:

\[
\boxed{
r_t(\theta)
=
\frac{\pi_\theta(a_t|s_t)}
{\pi_{\theta_{\text{old}}}(a_t|s_t)}
}
\]

and:

\[
\boxed{
L^{CLIP}(\theta)
=
E_t
[
\min(
r_tA_t,
\operatorname{clip}(r_t,1-\epsilon,1+\epsilon)A_t
)
]
}
\]

These are the two most important PPO equations.

---

# 24. Quick Numerical Pattern

If given:

\[
\pi_{\text{old}}=0.4
\]

\[
\pi_{\text{new}}=0.5
\]

then:

\[
r=\frac{0.5}{0.4}=1.25
\]

If:

\[
\epsilon=0.2
\]

then:

\[
1-\epsilon=0.8
\]

\[
1+\epsilon=1.2
\]

Therefore:

\[
\operatorname{clip}(1.25,0.8,1.2)=1.2
\]

If:

\[
A=3
\]

then:

\[
rA=1.25(3)=3.75
\]

while:

\[
\operatorname{clip}(r)A=1.2(3)=3.6
\]

Hence:

\[
L^{CLIP}
=
\min(3.75,3.6)
\]

\[
\boxed{L^{CLIP}=3.6}
\]

---

# 25. What Happens When Advantage Is Negative?

Suppose:

\[
A=-2
\]

and:

\[
r=1.5
\]

with:

\[
\epsilon=0.2
\]

Then:

\[
\operatorname{clip}(1.5,0.8,1.2)=1.2
\]

Unclipped:

\[
rA=1.5(-2)=-3
\]

Clipped:

\[
1.2(-2)=-2.4
\]

Therefore:

\[
\min(-3,-2.4)=-3
\]

The objective therefore prevents the update from receiving an artificially favorable objective when the policy moves too far in the wrong direction.

---

# 26. PPO — Important Terms

| Term | Meaning |
|---|---|
| Policy | \(\pi(a|s)\) |
| Old policy | Policy used to collect data |
| New policy | Policy currently being optimized |
| Ratio | New probability / old probability |
| Advantage | How much better an action was than expected |
| Clipping | Limits policy change |
| Actor | Policy network |
| Critic | Value network |
| \(\epsilon\) | Clipping range |

---

# 27. PPO — One-Minute Revision

Remember:

```text
PPO
 |
 +-- Policy-gradient algorithm
 |
 +-- Usually Actor-Critic
 |
 +-- Collect trajectories
 |
 +-- Calculate advantage
 |
 +-- Compare new policy with old policy
 |
 +-- Probability ratio
 |
 +-- Clip ratio
 |
 +-- Prevent excessively large updates
 |
 +-- Update Actor + Critic
```

---

# 28. Exam Answer: "Explain PPO"

> Proximal Policy Optimization is a policy-gradient reinforcement learning algorithm that improves a policy while preventing excessively large policy updates. It compares the new and old policies using the probability ratio
>
> \[
> r_t(\theta)=
> \frac{\pi_\theta(a_t|s_t)}
> {\pi_{\theta_{old}}(a_t|s_t)}
> \]
>
> and uses a clipped surrogate objective:
>
> \[
> L^{CLIP}
> =
> E[
> \min(
> r_tA_t,
> \operatorname{clip}(r_t,1-\epsilon,1+\epsilon)A_t
> )
> ].
> \]
>
> The clipping limits how much the new policy can differ from the old policy in one update. PPO commonly uses an Actor-Critic structure where the Actor represents the policy and the Critic estimates the value function and helps calculate the advantage. The main advantage of PPO is stable policy optimization with a relatively simple implementation.

---

# 29. High-Priority Exam Points

### Must know

\[
\boxed{
r_t=
\frac{\pi_{\text{new}}}
{\pi_{\text{old}}}
}
\]

\[
\boxed{
A(s,a)=Q(s,a)-V(s)
}
\]

\[
\boxed{
L^{CLIP}
=
E[
\min(rA,\operatorname{clip}(r,1-\epsilon,1+\epsilon)A)
]
}
\]

### Must understand

1. Why policy updates can become unstable.
2. Why PPO compares old and new policies.
3. Meaning of probability ratio.
4. Purpose of clipping.
5. Role of advantage.
6. Actor vs Critic.
7. PPO vs DQN.
8. PPO vs vanilla policy gradient.

---

# 30. Memory Trick

\[
\boxed{
\text{PPO = Policy + Ratio + Clip}
}
\]

Think:

> **"Improve the policy, but don't move it too far."**

That is the central idea of PPO.
