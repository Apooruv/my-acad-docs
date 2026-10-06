# Temporal Difference Learning

## 1. Definition

**Temporal Difference (TD) Learning** is a model-free learning method that updates value estimates using the value of the next state.

The key idea is:

> Do not wait for the complete episode. Update the value after observing the next state.

The supplied RL tutorial describes TD as combining:

- MC's model-free learning from experience
- DP's use of successor-state values

and notes that TD can work for continuous tasks. :chatgpt-content-reference{index="5"}

---

# 2. TD vs Monte Carlo

Consider:

```text
S_t → S_{t+1} → S_{t+2} → ...
```

### Monte Carlo

Waits until the end:

```text
S_t
 ↓
...
 ↓
Terminal
 ↓
Calculate complete return
 ↓
Update
```

### TD

Updates immediately:

```text
S_t → S_{t+1}
       ↓
Reward observed
       ↓
Update V(S_t)
```

---

# 3. TD(0) Update

The basic one-step TD update is:

\[
\boxed{
V(S_t)
\leftarrow
V(S_t)
+
\alpha
[
R_{t+1}
+
\gamma V(S_{t+1})
-
V(S_t)
]
}
\]

The quantity:

\[
\boxed{
\delta_t=
R_{t+1}
+\gamma V(S_{t+1})
-
V(S_t)
}
\]

is the **TD error**.

Therefore:

\[
V(S_t)\leftarrow V(S_t)+\alpha\delta_t
\]

---

# 4. TD Target

The TD target is:

\[
\boxed{
R_{t+1}+\gamma V(S_{t+1})
}
\]

The current value is moved toward this target.

So:

\[
\boxed{
\text{New Value}
=
\text{Old Value}
+
\alpha(\text{Target}-\text{Old Value})
}
\]

---

# 5. Numerical Example

Suppose:

\[
V(S_t)=5
\]

\[
R_{t+1}=2
\]

\[
V(S_{t+1})=6
\]

\[
\gamma=0.9
\]

\[
\alpha=0.1
\]

### Step 1 — Calculate TD target

\[
Target=2+0.9(6)
\]

\[
=2+5.4
\]

\[
=7.4
\]

### Step 2 — Calculate TD error

\[
\delta=7.4-5
\]

\[
=2.4
\]

### Step 3 — Update

\[
V(S_t)=5+0.1(2.4)
\]

\[
\boxed{V(S_t)=5.24}
\]

---

# 6. TD Does Not Need Complete Episodes

This is one of its biggest advantages.

Suppose:

```text
S1 → S2 → S3 → S4 → ...
```

After observing:

\[
S_1\rightarrow S_2
\]

the agent can already update:

\[
V(S_1)
\]

It does not need to wait until termination.

---

# 7. Bootstrapping

TD is called a **bootstrapping** method because it updates one estimate using another estimate.

The target contains:

\[
V(S_{t+1})
\]

which is itself an estimate.

Therefore:

> TD learns from an estimate of future value rather than waiting for the complete actual return.

---

# 8. TD and Dynamic Programming

TD and DP have an important similarity.

DP uses:

\[
R+\gamma V(s')
\]

to calculate expected values from the environment model.

TD uses an observed transition:

\[
R_{t+1}+\gamma V(S_{t+1})
\]

Therefore:

```text
DP
Model + successor values
        ↓
Expected update

TD
Observed transition + successor value
        ↓
Sample update
```

---

# 9. TD and Monte Carlo

| Property | Monte Carlo | TD |
|---|---|---|
| Model required | No | No |
| Needs complete episode | Yes | No |
| Update timing | End of episode | After each step |
| Bootstrapping | No | Yes |
| Variance | Higher | Usually lower |
| Bias | Lower | Can have bias |
| Continuing tasks | Problematic | Suitable |

---

# 10. MC vs TD Example

Suppose:

```text
A → B
```

and:

\[
R=0
\]

Suppose:

\[
V(B)=0.75
\]

and:

\[
\gamma=1
\]

### TD

Immediately estimates:

\[
V(A)\leftarrow V(A)+
\alpha[0+0.75-V(A)]
\]

It uses the current estimate of \(B\).

### MC

It would wait until the episode terminates and use the actual return from A.

---

# 11. Why TD Can Be Faster

Consider a very long episode:

```text
S1 → S2 → S3 → ... → S10000 → Goal
```

MC may have to wait until step 10000 before updating the value of S1.

TD can update:

\[
S_1
\]

after observing:

\[
S_2
\]

Then:

\[
S_2
\]

after observing:

\[
S_3
\]

and so on.

Thus TD can propagate information backward through the state sequence incrementally.

---

# 12. Advantages

### 1. Model-free

No transition model is required.

### 2. Online learning

Can update after each transition.

### 3. Works for continuing tasks

It does not require a terminal state.

### 4. Lower variance than MC in many settings

It uses one-step targets rather than complete random returns.

---

# 13. Disadvantages

### 1. Bootstrapping bias

The target depends on another estimated value.

### 2. Learning can depend on initial estimates

Poor value estimates can influence later updates.

### 3. TD error can be noisy

Observed rewards and successor estimates can still produce unstable updates.

---

# 14. Exam Question

### Question

> Describe the key concept of Temporal Difference Learning. How does TD learning update the value of a state differently from Direct Utility Estimation and Monte Carlo Methods?

### Answer

Temporal Difference Learning updates the value of a state using the immediate reward and the estimated value of the next state:

\[
V(S_t)
\leftarrow
V(S_t)+
\alpha[
R_{t+1}+\gamma V(S_{t+1})-V(S_t)
]
\]

Unlike Direct Utility Estimation and Monte Carlo methods, TD does not need to wait for the complete episode to calculate the return. It updates after each observed transition and uses the successor state's estimated value. Therefore, TD is a bootstrapping method.

### Core difference

```text
Direct Utility:
Observed complete returns → average

Monte Carlo:
Complete episode → actual return → update

TD:
One transition → estimated successor value → update
```