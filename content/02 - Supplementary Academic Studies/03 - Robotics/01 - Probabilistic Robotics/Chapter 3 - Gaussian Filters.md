## 3.1 Introduction

- Gaussian techniques all share the idea that beliefs can be represented by multivariate normal distributions.
- These distributions are defined as:

$$
P(x) = \text{det}(2\pi \Sigma)^{-\frac{1}{2}} \exp \left\{ -\frac{1}{2} (x - \mu)^T \Sigma^{-1} (x - \mu) \right\}
$$

- Mean: $\mu \in \mathbb{R}^n$
- Covariance: $\Sigma$ (quadratic matrix must be symmetric and positive-semidefinite) $\in \mathbb{R}^{n \times n}$

## 3.2 Kalman Filter

### 3.2.1 Linear Gaussian Systems

- The Kalman filter explains **belief** computation for continuous states.
- Kalman filter represents beliefs by the moment representation. At time $t$ the belief is represented by the mean $\mu_t$ and the covariance $\Sigma_t$.
- Posteriors are Gaussian if the 3 properties hold.


### 1.) State Transition Probability

The next state probability $P(x_t \mid u_t, x_{t-1})$ must be a linear function:

$$
x_t = A_t x_{t-1} + B_t u_t + \epsilon_t
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
- $x_{t-1}$: Previous state vector
- $u_t$: Control vector at time $t$
  $$
  u_t = \begin{pmatrix}
  u_{1,t} \\
  \vdots \\
  u_{m,t}
  \end{pmatrix}
  $$
- $A_t$: $n \times n$ matrix where $n$ is the size of $x_t$
- $B_t$: $n \times m$ matrix where $m$ is the size of $u_t$
- $\epsilon_t$: Random variable with mean $0$ and covariance $R_t$

The full probability distribution is expressed as:

$$
P(x_t \mid u_t, x_{t-1}) = \delta_t (2\pi R_t)^{-\frac{1}{2}} \exp \left\{ -\frac{1}{2} (x_t - A_t x_{t-1} - B_t u_t)^T R_t^{-1} (x_t - A_t x_{t-1} - B_t u_t) \right\}
$$

### 2.) Measurement Probability

The measurement probability $P(z_t \mid x_t)$ must also be linear with added Gaussian noise:

$$
z_t = C_t x_t + \delta_t
$$

Where:
- $C_t$: $k \times n$ matrix where $n$ is the size of $x_t$
- $\delta_t$: Gaussian noise with zero mean and covariance $Q_t$

We can re-write the measurement probability:

$$
P(z_t | x_t) = \text{det}(2\pi Q_t)^{-\frac{1}{2}} \exp \left\{ -\frac{1}{2} (z_t - C_t x_t)^T Q_t^{-1} (z_t - C_t x_t) \right\}
$$

### 3) Finally, the initial belief $bel(x_0)$ must be normally distributed. The mean of this belief is $\mu_0$ and covariance $\Sigma_0$:

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

## 3.3 The Extended Kalman Filter

For the extended Kalman filter, we remove the linearity assumptions and have the next state and measurement probabilities governed by nonlinear functions $g$ and $h$, respectively:

$$
x_t = g(u_t, x_{t-1}) + \epsilon_t
$$

$$
z_t = h(x_t) + \delta_t
$$

The EKF calculates an approximation to the true belief. This belief $bel(x_t)$ at time $t$ is represented by a mean $\mu_t$ and a covariance $\Sigma_t$. Thus, EKF is an approximation by a Gaussian.

### 3.3.1 Linearization via Taylor Expansion

Linearization approximates $g$ by a linear function that is tangent to $g$ at the mean of the Gaussian. The same can be said for $h$.

Using Taylor's expansion on $g$:

$$
g'(u_t, x_{t-1}) := \frac{\partial g(u_t, x_{t-1})}{\partial x_{t-1}}
$$

$$
g(u_t, x_{t-1}) \approx g(u_t, \mu_{t-1}) + g'(u_t, \mu_{t-1})(x_{t-1} - \mu_{t-1})
$$
## 3.3 The Extended Kalman Filter (EKF)

The EKF modifies nonlinear state and measurement equations into linear approximations for simplicity in computation.

### Linearization of $g$ and $h$

The nonlinear functions $g$ and $h$ are linearized using a first-order Taylor expansion:

$$
g(u_t, \bar{M}_{t-1}) \approx g(u_t, M_{t-1}) + G_t (x_{t-1} - M_{t-1})
$$

Similarly, $h(x_t)$ becomes:

$$
h(x_t) \approx h(\bar{M}_t) + H_t (x_t - \bar{M}_t)
$$

### Approximations for Probabilities

Using linearization, the state transition probability becomes:

$$
P(x_t \mid u_t, x_{t-1}) \approx \text{det}((2\pi R_t)^{1/2}) \exp \left\{ -\frac{1}{2} (x_t - g(u_t, M_{t-1}) - G_t (x_{t-1} - M_{t-1}))^T R_t^{-1} (x_t - g(u_t, M_{t-1}) - G_t (x_{t-1} - M_{t-1})) \right\}
$$

For the measurement probability:

$$
P(z_t \mid x_t) \approx \text{det}((2\pi Q_t)^{1/2}) \exp \left\{ -\frac{1}{2} (z_t - h(\bar{M}_t) - H_t (x_t - \bar{M}_t))^T Q_t^{-1} (z_t - h(\bar{M}_t) - H_t (x_t - \bar{M}_t)) \right\}
$$

Here, $G_t$ and $H_t$ are Jacobian matrices of $g$ and $h$, respectively.

### 3.3.2 The EKF Algorithm

The EKF algorithm is as follows:

```pseudo
\begin{algorithm}
\caption{Extended Kalman Filter Algorithm}
\begin{algorithmic}
\REQUIRE $\mu_{t-1}$, $\Sigma_{t-1}$, $u_t$, $z_t$
\STATE \textbf{1. Prediction Step:}
\STATE $\bar{M}_t = g(u_t, \mu_{t-1})$
\STATE $\bar{\Sigma}_t = G_t \Sigma_{t-1} G_t^T + R_t$

\STATE \textbf{2. Update Step:}
\STATE $K_t = \bar{\Sigma}_t H_t^T \left( H_t \bar{\Sigma}_t H_t^T + Q_t \right)^{-1}$
\STATE $\mu_t = \bar{\mu}_t + K_t \left( z_t - h(\bar{\mu}_t) \right)$
\STATE $\Sigma_t = \left( I - K_t H_t \right) \bar{\Sigma}_t$

\RETURN $\mu_t$, $\Sigma_t$
\end{algorithmic}
\end{algorithm}

```
This algorithm outputs the updated mean $\mu_t$ and covariance $\Sigma_t$.

- Each update requires $O(n^{2.3} + n^2)$.

## 3.4 Information Filter

- Information Filters (IF) are similar to Kalman Filters (KF) but differ in how Gaussian beliefs are represented. In Information Filters, the Gaussian beliefs are in the canonical representation.

### 3.4.1 Canonical Representation

- **Information Matrix ($\Omega$):**
  $$
  \Omega = \Sigma^{-1}
  $$

- **Information Vector ($\xi$):**
  $$
  \xi = \Sigma^{-1} \mu = \Omega \mu
  $$

- Relationships between canonical and standard representations:
  $$
  \Sigma = \Omega^{-1}
  $$
  $$
  \mu = \Omega^{-1} \xi
  $$
  $$
  x = \Omega^{-1} \xi
  $$

### 3.4.2 The Information Filter Algorithm

```pseudo
\begin{algorithm}
\caption{Information Filter Algorithm}
\begin{algorithmic}
\REQUIRE $\bar{\xi}_{t-1}$, $\bar{\Omega}_{t-1}$, $u_t$, $z_t$

\STATE \textbf{1. Prediction Step:}
\STATE $\Omega_t = \left( A_t \bar{\Omega}_{t-1}^{-1} A_t^T + R_t \right)^{-1}$
\STATE $\bar{\xi}_t = \Omega_t \left( A_t \bar{\Omega}_{t-1}^{-1} \bar{\xi}_{t-1} + B_t u_t \right)$

\STATE \textbf{2. Update Step:}
\STATE $\bar{\Omega}_t = C_t^T Q_t^{-1} C_t + \Omega_t$
\STATE $\bar{\xi}_t = C_t^T Q_t^{-1} z_t + \bar{\xi}_t$

\RETURN $\bar{\xi}_t, \bar{\Omega}_t$
\end{algorithmic}
\end{algorithm}

```
- $A_t, B_t, C_t, R_t, \text{and } Q_t$ are the same as defined in Section 3.2.
- Lines 2 and 3 are the prediction steps where the parameters $\bar{\xi}_t$ and $\bar{\Omega}_t$ describe the Gaussian belief over $x_t$ after incorporating the action $u_t$, but before taking the measurement $z_t$.
- Lines 4 and 5 are updating the belief after taking the measurement $z_t$.
- **Worst case complexity**: $O(n^{2.8})$

## 3.4.4 The Extended Information Filter Algorithm

### Nonlinear Functions:
- Same nonlinear function models as EKF:
  $$
  x_t = g(u_t, x_{t-1}) + \epsilon_t
  $$
  $$
  z_t = h(x_t) + \delta_t
  $$

### Algorithm Steps:

```pseudo
\begin{algorithm}
\caption{Extended Information Filter (EIF) Algorithm}
\begin{algorithmic}
\REQUIRE $\hat{\xi}_{t-1}$, $\Omega_{t-1}$, $u_t$, $z_t$

\STATE \textbf{1. Compute the Mean:}
\STATE $M_{t-1} = \Omega_{t-1}^{-1} \hat{\xi}_{t-1}$

\STATE \textbf{2. Prediction Step:}
\STATE $\bar{\Omega}_t = \left( G_t \Omega_{t-1}^{-1} G_t^T + R_t \right)^{-1}$
\STATE $\bar{\xi}_t = \bar{\Omega}_t g(u_t, M_{t-1})$

\STATE \textbf{3. Predicted Mean:}
\STATE $\bar{M}_t = g(u_t, M_{t-1})$

\STATE \textbf{4. Update Step:}
\STATE $\Omega_t = \bar{\Omega}_t + H_t^T Q_t^{-1} H_t$
\STATE $\hat{\xi}_t = \bar{\xi}_t + H_t^T Q_t^{-1} \left[ z_t - h(\bar{M}_t) - H_t \bar{M}_t \right]$

\RETURN $\hat{\xi}_t, \Omega_t$
\end{algorithmic}
\end{algorithm}

```
### Jacobians:
- $G_t$ and $H_t$ are Jacobians of the functions $g$ and $h$, respectively.
