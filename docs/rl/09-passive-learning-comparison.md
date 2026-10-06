# Direct Utility Estimation vs Monte Carlo vs TD

## 1. Why Compare Them?

All three methods can be used for **passive policy evaluation**.

The goal is:

\[
\boxed{\text{Estimate }V^\pi(s)}
\]

But they use experience differently.

---

# 2. Core Difference

### Direct Utility Estimation

\[
\boxed{
V(s)\approx\text{average observed returns}
}
\]

### Monte Carlo

\[
\boxed{
V(s)\leftarrow V(s)+
\alpha[G_t-V(s)]
}
\]

### TD

\[
\boxed{
V(s)\leftarrow V(s)+
\alpha[
R+\gamma V(s')-V(s)
]
}
\]

---

# 3. Comparison Table

| Feature | Direct Utility Estimation | Monte Carlo | TD |
|---|---|---|---|
| Policy | Fixed | Fixed | Fixed in passive setting |
| Model required | No | No | No |
| Uses experience | Yes | Yes | Yes |
| Complete episode required | Generally | Yes | No |
| Bootstrapping | No | No | Yes |
| Update | Average returns | Sample return | Successor estimate |
| Continuing tasks | Poor | Poor | Good |
| Variance | Can be high | High | Usually lower |
| Main weakness | Needs many observations | Must wait for episode | Bootstrapping bias |

---

# 4. Direct Utility Estimation

### Best suited for

- Small state spaces
- Sufficient repeated observations
- Simple episodic environments

### Main problem

Large state spaces:

\[
|S|\gg1
\]

Many states may not have enough observations.

---

# 5. Monte Carlo

### Best suited for

- Episodic tasks
- Environments where complete episodes are available
- Situations where model-free learning is required

### Main problem

Must wait until the end of an episode.

---

# 6. Temporal Difference

### Best suited for

- Continuing environments
- Online learning
- Long episodes
- Situations where frequent updates are useful

### Main problem

Uses bootstrapping and therefore introduces bias.

---

# 7. Bias-Variance Intuition

This is useful for conceptual questions.

### Monte Carlo

Uses the actual sampled return.

Therefore:

- less bias from bootstrapping
- potentially high variance

### TD

Uses:

\[
R+\gamma V(S')
\]

Therefore:

- lower variance in many situations
- introduces bootstrapping bias

A useful exam statement:

> MC waits for accurate sampled returns but can have high variance; TD updates earlier using estimated successor values, which reduces variance but introduces bootstrapping bias.

---

# 8. Question: Compare the Three Methods

### Answer

Direct Utility Estimation, Monte Carlo and Temporal Difference learning are methods for estimating the value function under a fixed policy.

Direct Utility Estimation estimates the value of a state by averaging observed returns. It is simple but inefficient for large state spaces or states with limited observations.

Monte Carlo methods also estimate values using complete sampled episodes and observed returns. They are model-free and simple but must wait until the episode terminates and can have high variance.

TD learning updates values after each transition using the immediate reward and estimated value of the next state. It does not require complete episodes and can therefore operate online and in continuing environments. Its main disadvantage is bootstrapping bias because the target contains an estimated value.

---

# 9. Most Important Exam Comparison

Remember this:

```text
                 PASSIVE LEARNING

                     Vπ(s)
                       │
          ┌────────────┼────────────┐
          │            │            │
          ▼            ▼            ▼
       Direct         MC           TD
       Utility
          │            │            │
          ▼            ▼            ▼
     Average       Complete     One-step
     returns        return       target
                       │            │
                       │            ▼
                       │       V(s')
                       │       estimate
                       │
                       ▼
                  Wait until
                  episode ends
```

---

# 10. One-Line Definitions

### Direct Utility Estimation

> Estimates state utility by averaging observed returns following visits to the state.

### Monte Carlo

> Estimates value from complete sampled episodes without using a model or bootstrapping.

### Temporal Difference

> Estimates value from observed transitions by bootstrapping from the estimated value of the successor state.

---

# 11. Exam Decision Rule

If the question says:

### "Average observed returns"

Think:

\[
\boxed{\text{Direct Utility / MC}}
\]

### "Complete episode"

Think:

\[
\boxed{\text{Monte Carlo}}
\]

### "Update after every step"

Think:

\[
\boxed{\text{TD}}
\]

### "Uses value of next state"

Think:

\[
\boxed{\text{TD}}
\]

### "No model"

Think:

\[
\boxed{\text{MC or TD}}
\]

### "Continuing task"

Think:

\[
\boxed{\text{TD}}
\]

---

# 12. Final Revision Table

| If the question emphasizes... | Answer |
|---|---|
| Average observed utility | Direct Utility Estimation |
| Complete episodes | Monte Carlo |
| First visit to state | First-visit MC |
| Actual complete return | Monte Carlo |
| Update after one step | TD |
| Successor state value | TD |
| Bootstrapping | TD |
| Continuing environments | TD |
| High variance of complete returns | MC |
| Large state space / sparse visits | Direct Utility Estimation limitation |