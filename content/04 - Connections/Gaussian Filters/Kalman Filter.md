**Idea**:  The kalman filter is a specific implementation of the [[Bayes' Filter]] with assumptions for a linear system and Gaussian noise. 

---


### 1.) State Transition Probability

The next state probability $P(x_t \mid u_t, x_{t-1})$ must be a linear function:

$$
x_t = A_t x_{t-1} + B_t u_t + \epsilon_t, \quad \epsilon_t \sim \mathcal{N}(0, R_t)
$$

Where:
- $x_t$: State vector
  $$
  x_t = \begin{pmatrix}
  x_{1,t} \\
  \vdots \\
  x_{n,t}
  \end{pmatrix}
  $$
- $x_{t-1}$: **Previous state** vector
- $u_t$: **Control** vector at time $t$
  $$
  u_t = \begin{pmatrix}
  u_{1,t} \\
  \vdots \\
  u_{m,t}
  \end{pmatrix}
  $$
- $A_t$: **State Transition** $n \times n$ matrix where $n$ is the size of $x_t$
- $B_t$ : **Control Matrix** $n \times m$ where $m$ is the size of $u_t$
- $R_t$: **Covariance of Process Noise** $\epsilon_t$
- $\epsilon_t$: Random variable with mean $0$ and covariance $R_t$

The full probability distribution is expressed as:

$$
P(x_t \mid u_t, x_{t-1}) = \delta_t (2\pi R_t)^{-\frac{1}{2}} \exp \left\{ -\frac{1}{2} (x_t - A_t x_{t-1} - B_t u_t)^T R_t^{-1} (x_t - A_t x_{t-1} - B_t u_t) \right\}
$$

### 2.) Measurement Probability

The measurement probability $P(z_t \mid x_t)$ must also be linear with added Gaussian noise:

$$
z_t = C_t x_t + \delta_t \quad \delta_t  \sim \mathcal{N}(0, Q_t)
$$

Where:
- $C_t$: $k \times n$ matrix where $n$ is the size of $x_t$
- $\delta_t$: Gaussian noise with zero mean and covariance $Q_t$

We can re-write the measurement probability:

$$
P(z_t | x_t) = \text{det}(2\pi Q_t)^{-\frac{1}{2}} \exp \left\{ -\frac{1}{2} (z_t - C_t x_t)^T Q_t^{-1} (z_t - C_t x_t) \right\}
$$

### 3)  Initial Belief

$bel(x_0)$ must be normally distributed. The mean of this belief is $\mu_0$ and covariance $\Sigma_0$:

$$
bel(x_0) = P(x_0) = \text{det}(2\pi \Sigma_0)^{-\frac{1}{2}} \exp \left\{ -\frac{1}{2} (x_0 - \mu_0)^T \Sigma_0^{-1} (x_0 - \mu_0) \right\}
$$

These 3 assumptions are sufficient to ensure the posterior $bel(x_t)$ is always Gaussian.

## 3.2.2 The Kalman Filter Algorithm

**Algorithm:**

```pseudo
\begin{algorithm}
\caption{Kalman Filter Algorithm}
\begin{algorithmic}
\REQUIRE $\mu_{t-1}$, $\Sigma_{t-1}$, $u_t$, $z_t$

\STATE \textbf{1. Predict step:}
\STATE $\bar{\mu}_t = A_t \mu_{t-1} + B_t u_t$
\STATE $\bar{\Sigma}_t = A_t \Sigma_{t-1} A_t^T + R_t$

\STATE \textbf{2. Update step:}
\STATE $K_t = \bar{\Sigma}_t C_t^T \left( C_t \bar{\Sigma}_t C_t^T + Q_t \right)^{-1}$
\STATE $\mu_t = \bar{\mu}_t + K_t \left( z_t - C_t \bar{\mu}_t \right)$
\STATE $\Sigma_t = \left( I - K_t C_t \right) \bar{\Sigma}_t$

\RETURN $\mu_t, \Sigma_t$
\end{algorithmic}
\end{algorithm}

```
