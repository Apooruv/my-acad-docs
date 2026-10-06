# Monte Carlo Methods

## 1. Definition

Monte Carlo (MC) methods estimate value functions using **sampled complete episodes**.

The key idea is:

> Generate an episode, observe the complete return, and use that return to estimate the value of visited states.

For state \(s\):

\[
\boxed{
V^\pi(s)
\approx
\text{average of observed returns after }s
}
\]

The supplied RL tutorial explicitly describes MC as requiring experience or simulated experience and averaging sample returns. :chatgpt-content-reference{index="3"}

---

## 2. Important Property

Monte Carlo methods do **not require a model** of the environment.

They only need experience:

```text
Environment
     ↓
Episode
     ↓
Observed rewards
     ↓
Return
     ↓
Value estimate
```

---

## 3. Monte Carlo Policy Evaluation

The objective is:

\[
V^\pi(s)
=
E_\pi[G_t|S_t=s]
\]

We estimate this using observed returns.

Suppose the returns observed after state \(s\) are:

\[
G_1,G_2,\ldots,G_N
\]

Then:

\[
\boxed{
V^\pi(s)
=
\frac{1}{N}\sum_{i=1}^{N}G_i
}
\]

---

# 4. First-Visit Monte Carlo

In **first-visit MC**, only the first occurrence of a state in an episode is used.

Suppose:

```text
Episode:

A → B → A → C → Goal
```

State A occurs twice.

First-visit MC uses only the first `A`.

```text
A → B → A → C → Goal
↑
Use this A
```

The supplied tutorial specifically describes first-visit MC as averaging returns following the first visit to a state. reinforcement-learning (5) (2) …

---

# 5. Numerical Example

Suppose four episodes produce returns after state \(S\):

\[
2,\quad1,\quad-5,\quad4
\]

Then:

\[
V^\pi(S)
=
\frac{2+1-5+4}{4}
\]

\[
\boxed{V^\pi(S)=0.5}
\]

---

# 6. Why Complete Episodes?

The return is:

\[
G_t=
R_{t+1}
+\gamma R_{t+2}
+\gamma^2R_{t+3}
+\cdots
\]

To know the complete return, MC waits until the episode terminates.

Example:

```text
S
↓
A
↓
B
↓
Goal
```

Only after reaching the terminal state do we know the complete return.

---

# 7. Monte Carlo Update

For a state \(s\), if the observed return is \(G_t\):

\[
\boxed{
V(s)\leftarrow
V(s)+
\alpha[G_t-V(s)]
}
\]

Here:

\[
G_t-V(s)
\]

is the prediction error.

This is an incremental implementation of averaging.

---

# 8. Advantages of Monte Carlo

## 1. Model-free

No transition model is needed.

## 2. Simple

It directly uses observed returns.

## 3. No bootstrapping

MC uses the actual sampled return rather than another estimated value.

## 4. Can learn from complete episodes

The agent does not need to know transition probabilities.

---

# 9. Disadvantages

## 1. Must wait until episode termination

This makes MC unsuitable for direct learning in continuing tasks.

## 2. High variance

Returns can vary significantly between episodes.

## 3. Slow learning

A long episode may need to finish before the value is updated.

## 4. Poor for very long/continuous tasks

If episodes are extremely long or do not naturally terminate, waiting for complete returns becomes impractical.

---

# 10. MC vs Dynamic Programming

| MC | Dynamic Programming |
|---|---|
| Model-free | Model-based |
| Uses sampled episodes | Uses known transition model |
| Estimates from experience | Computes expected values |
| No transition probabilities needed | Requires transition probabilities |

---

# 11. MC vs TD

This distinction is extremely important.

### Monte Carlo

Waits until the end:

\[
V(s)\leftarrow V(s)+\alpha[G_t-V(s)]
\]

### TD

Updates after the next step:

\[
V(s_t)
\leftarrow
V(s_t)
+
\alpha[
R_{t+1}
+\gamma V(s_{t+1})
-
V(s_t)
]
\]

Therefore:

> **MC learns from complete returns.**

> **TD learns from one-step estimates.**

---

# 12. Exam Question

### Question

> Explain the advantages and disadvantages of Monte Carlo methods in Passive Learning. Why might it be impractical to use Monte Carlo methods in continuous or highly variable environments?

### Answer

Monte Carlo methods estimate state values by averaging returns obtained from complete episodes. They are model-free and conceptually simple, because they learn directly from observed experience without requiring transition probabilities.

Their major disadvantage is that they generally require an episode to terminate before the complete return is known. They can also have high variance because returns can differ significantly between episodes. Therefore, they become impractical when episodes are extremely long, do not naturally terminate, or the environment is highly variable.

### Exam keywords

- Complete episode
- Sample return
- Average
- Model-free
- No bootstrapping
- High variance
- Delayed update
- Episodic tasks