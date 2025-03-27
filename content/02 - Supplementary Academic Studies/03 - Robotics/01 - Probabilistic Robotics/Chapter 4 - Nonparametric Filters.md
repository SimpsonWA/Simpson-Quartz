# Chapter 4: Nonparametric Filters

Nonparametric filters don't rely on a fixed functional form of the posterior; instead, they approximate posteriors with a finite number of values.

## 4.1: The Histogram Filter

- **Discrete spaces:** Discrete Bayes Filter  
- **Continuous spaces:** Histogram Filters

### 4.1.1: The Discrete Bayes Filter

Commonly used in cases of occupancy grid spaces as it's discrete.

#### Algorithm: Discrete Bayes Filter
```pseudo
\begin{algorithm}
\caption{Algo\_Discrete\_Bayes\_Filter($\{P_{k,t-1}\}, u_t, z_t$)}
\begin{algorithmic}
\ForAll{$k$}
    \STATE $\bar{P}_{k,t} = \sum_i p(X_{k} = x_{k} \mid u_t, X_{t-1} = x_i) P_{i,t-1}$
    \STATE $P_{k,t} = \eta p(z_t \mid X_{t} = x_{k}) \bar{P}_{k,t}$
\EndFor
\RETURN{$\{P_{k,t}\}$}
\end{algorithmic}
\end{algorithm}
```

- $x_i, x_t$: individual states    
- $P_{k,t}$: probability or belief of $X_k$ at time $t$
- Input $\{P_{k,t-1}\}$: discrete probability distribution

- Line 3 calculates the prediction (the belief for the new state based on the control $u_t$ only).
- Line 4 updates the prediction with the inclusion of the measurement $z_t$.
- Bayes filter algorithm is commonly used in areas of signal processing such as speech recognition.

## 4.1.2 Continuous State

- **Histogram filters:** Bayes filter in continuous state space.
- Histogram filters decompose a continuous space into finitely many regions:
  $$
  \text{range}(X_{t}) = x_{1,t} \cup x_{2,t} \cup \ldots \cup x_{k,t}
  $$
  where:
  - $X_{t}$: state of robot at time $t$
  - $\text{range}(X_{t})$: state space (universe of possible values $X_{t}$ may take)
  - $X_{k,t}$: convex region
- Probability is calculated as:
  $$
  P(x_{t}) = \frac{P_{k,t}}{|x_{k,t}|}
  $$
- $|x_{k,t}|$ Volume of the Region $x_{k,t}$

In continuous space, we are typically given the densities $p(x_{k,t} \mid x_{k,t-1})$ and $p(z_t \mid x_t)$, which are defined for individual states (and not for regions in the state space). For cases where each region $x_{k,t}$ is small and of the same size, these regions are approximated by substituting $x_{k,t}$ with a representative of this region. For example, we may begin by using the mean state in $x_{k,t}$:

$$
\hat{x}_{k,t} = \frac{1}{|x_{k,t}|} \int_{x_{k,t}} x_t \, dx
$$

Then we would replace:

$$
p(z_t \mid x_{k,t}) \approx p(z_t \mid \hat{x}_{k,t})
$$

$$
p(x_{k,t} \mid u_t, x_{k,t-1}) = \frac{h}{|x_{k,t}|} p(\hat{x}_{k,t} \mid u_t, x_{k,t-1})
$$
# 4.1.3 Decomposition Techniques

- Commonly two different techniques for decomposition of continuous spaces:
  - **Static**: where we have a fixed decomposition that is chosen in advance.
  - **Dynamic**: adapt the decomposition to a specific shape of the posterior distribution.

## 4.1.4 Binary Bayes's Filters with Static State

- Since the state is static, the belief is a function of the measurements:
  $$
  \text{bel}_t(x) = p(X_t \mid Z_{1:t}, U_{1:t}) = p(X_t \mid Z_{1:t})
  $$
- Where the state has two possible values $x$ and $\neg x$:
  $$
  \text{bel}_t(\neg x) = 1 - \text{bel}_t(x)
  $$
- The belief is commonly represented as the log-odds ratio:
  $$
  l(x) := \log \left( \frac{p(x)}{1 - p(x)} \right)
  $$

# Binary Bayes Filter Algorithm:

```pseudo
\begin{algorithm}
\caption{Binary Bayes Filter Algorithm}
\begin{algorithmic}
\State Update log-odds: 
$l_{t} = l_{t-1} + \log \frac{p(x \mid z_t)}{1 - p(x \mid z_t)} - \log \frac{p(x)}{1 - p(x)}$
\RETURN $l_t$
\end{algorithmic}
\end{algorithm}
```


### Belief Representation
The belief can be computed using the log-odds ratio as follows:

$$
\text{bel}_t(x) = 1 - \frac{1}{1 + \exp(2l_t)}
$$

### Measurement Probability Update
The probability for the measurement $z_t$ given $x$ is expressed as:

$$
p(z_t \mid x) = \frac{p(x \mid z_t) p(z_t)}{p(x)}
$$

---

## 4.2 The Particle Filter

### Basic Algorithm

- Particle filters serve as a nonparametric alternative to Bayes filters.
- The key idea of particle filters is to approximate the posterior distribution $\text{bel}(x_t)$ using random state samples.
- Particles represent the posterior distribution, denoted as:

$$
X_t := \{x_t^{[1]}, x_t^{[2]}, \dots, x_t^{[M]}\}
$$

- Here $M$ is the number of particles.

Each particle $x_t^{[m]}$ is a concrete instantiation of the state at time $t$.  

The likelihood for a state hypothesis $x_t$ to be included in the particle set $X_t$ is proportional to its Bayes filter posterior $\text{bel}(x_t)$:

$$
x_t^{[m]} \sim p(x_t \mid z_{1:t}, u_{1:t})
$$

```pseudo
\begin{algorithm}
\caption{Resampling for Particle Filter}
\begin{algorithmic}
\STATE \textbf{Inputs:} Particle weights $\{w_t^{[1]}, \dots, w_t^{[M]}\}$, particle set $\{x_t^{[1]}, \dots, x_t^{[M]}\}$
\STATE \textbf{Output:} Resampled particle set $\{x_t^{[1]}, x_t^{[2]}, \dots, x_t^{[M]}\}$
\STATE Initialize new particle set $X_t = \emptyset$
\FOR{$m = 1$ to $M$}
    \STATE Draw $i$ with probability proportional to $w_t^{[i]}$
    \STATE Add $x_t^{[i]}$ to $X_t$
\ENDFOR
\RETURN $X_t$
\end{algorithmic}
\end{algorithm}
```



The importance factor for particle $m$, denoted as $w_t^{[m]}$, is calculated as:

$$
w_t^{[m]} = p(z_t \mid x_t^{[m]})
$$

---

## Resampling

The steps for implementing resampling (importance resampling) are as follows:
- For $m = 1$ to $M$, draw $i$ with probability proportional to $w_t^{[i]}$.
- Add $x_t^{[i]}$ to the new particle set $X_t$.

# 4.2.2 Importance Sampling

- $f$: Target distribution.

- The goal is to sample from $f$, but this may not be feasible. Instead, we generate particles from a related density ($g$). Assuming that the particles in $X_{t-1}$ are distributed according to $bel(X_{t-1})$, the density $g$ corresponds to:

$$
P(X_t \mid u_t, X_{t-1}) bel(X_{t-1})
$$

- This is referred to as the proposal distribution.
