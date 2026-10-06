# Direct Utility Estimation

## 1. Definition

**Direct Utility Estimation** estimates the utility of a state directly from the observed returns obtained after visiting that state.

The basic idea is:

> Visit a state, observe what happens afterward, calculate the return, and average the observed returns.

For state \(s\):

\[
\boxed{
V^\pi(s)
\approx
\frac{1}{N}
\sum_{i=1}^{N}G_i(s)
}
\]

where:

- \(N\) = number of observed visits/episodes
- \(G_i(s)\) = return observed after visiting \(s\) in episode \(i\)

---

## 2. Basic Procedure

```text
Follow fixed policy π
       ↓
Generate episode
       ↓
Visit state s
       ↓
Observe future rewards
       ↓
Calculate return G
       ↓
Store G
       ↓
Average observed returns
       ↓
Estimate Vπ(s)
```

---

## 3. Example

Suppose state \(A\) is observed in four episodes.

The returns after visiting \(A\) are:

\[
2,\quad1,\quad-5,\quad4
\]

Then:

\[
V^\pi(A)
=
\frac{2+1-5+4}{4}
\]

\[
=
\frac{2}{4}
\]

\[
\boxed{V^\pi(A)=0.5}
\]

This is the same averaging principle illustrated in the supplied RL tutorial's Monte Carlo policy-evaluation example. reinforcement-learning (5) (2) …

---

## 4. Why Does It Work?

The true value is an expected return:

\[
V^\pi(s)=E_\pi[G|s]
\]

We do not normally know the exact expectation.

Instead, we estimate it from samples:

\[
V^\pi(s)\approx\frac{1}{N}\sum_iG_i
\]

As more experience is collected, the estimate generally becomes more reliable.

---

## 5. Major Problem: Large State Spaces

Suppose an environment contains:

\[
10^6
\]

possible states.

The agent may visit only a small fraction of them.

For an unvisited state:

\[
N(s)=0
\]

so there is no direct empirical estimate.

Therefore direct estimation can become extremely inefficient in large state spaces.

---

## 6. Limited Data Problem

Suppose state \(S\) is observed only twice:

\[
G_1=10
\]

\[
G_2=-8
\]

Then:

\[
V(S)=\frac{10-8}{2}=1
\]

The estimate is based on very little evidence.

A few unusual episodes can therefore strongly affect the estimate.

---

## 7. Delayed Learning

Direct return-based methods generally need to observe the future outcome before the return can be calculated.

For example:

```text
S
↓
A
↓
B
↓
Goal
```

If the final reward occurs only at the goal, the algorithm must observe the subsequent rewards before calculating the complete return from \(S\).

This makes learning slower than methods that can update after each step.

---

## 8. Advantages

### 1. Simple

The idea is straightforward:

\[
\text{estimate}=\text{average observed returns}
\]

### 2. Model-free

The environment's transition probabilities are not required.

### 3. Directly based on experience

The estimate comes from actual observed outcomes.

---

## 9. Disadvantages

### 1. Requires sufficient observations

Rare states are difficult to estimate.

### 2. Poor scalability

Large state spaces require many state visits.

### 3. High sensitivity to limited samples

Few observations can produce noisy estimates.

### 4. Delayed updates

The complete future outcome may need to be observed before an estimate can be updated.

---

## 10. Exam Question

### Question

> Explain how Direct Utility Estimation works in Passive Learning. Why might this method be inefficient in environments with large state spaces or with limited observed data?

### Answer

Direct Utility Estimation estimates the value of a state by averaging the returns observed after visiting that state while following a fixed policy.

\[
V^\pi(s)\approx
\frac{1}{N}\sum_{i=1}^{N}G_i(s)
\]

It is inefficient for large state spaces because many states may be rarely or never visited, leaving insufficient samples to estimate their utilities reliably. With limited observed data, the estimate can also have high variance because a small number of returns may not represent the true expected return accurately.

### Key points to write

- Fixed policy
- Observe episodes
- Calculate returns
- Average returns
- No environment model required
- Large state spaces → many states rarely visited
- Limited data → unreliable estimates