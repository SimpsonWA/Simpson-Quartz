## Recursive Bayesian updating

$$P(x \mid z_{1:n}) = \frac{P(z_n \mid x, z_{1:n-1}) P(x \mid z_{1:n-1})}{P(z_n \mid z_{1:n-1})}$$

### Markov assumption:
$z_n$ is independent of previous measurements ($z_{1:n-1}$) if we know $x$. This can be equivalently stated as the Markov property.

### Markov property:
The future is independent of the past if the present is known. A stochastic process that has this property is called a Markov process.

### Markov assumption equation:
$$P(x \mid z_{1:n}) = \frac{P(z_n \mid x) P(x \mid z_{1:n-1})}{P(z_n \mid z_{1:n-1})} = \eta_n P(z_n \mid x) P(x \mid z_{1:n-1}) = \eta_{1:n} \prod_{z=1}^n P(z_i \mid x) P(x)$$

...where $\eta_{1:n} \triangleq \eta_1 \eta_2 ... \eta_n$

## State estimation

Estimate the state $x$ of a system given observations $z$ and controls $u$.

$$P(x|z,u)$$

## Recursive Bayes filter

1. $bel(x_t) = p(x_t|z_{1:t}, u_{1:t})$ (Def of Belief)
2. $= \eta p(z_t|x_t, x_t, z_{1:t-1}, u_{1:t-1}) p(x_t|z_{1:t-1}, u_{1:t})$ (Bayes Rule)
3. $= \eta p(z_t|x_t) p(x_t|z_{1:t-1}, u_{1:t})$ (Markov assumption)
4. $= \eta p(z_t|x_t) \int p(x_t|x_{t-1}, u_t) p(x_{t-1}|z_{1:t-1}, u_{1:t-1}) dx_{t-1}$ (Law of total probability)
5. $= \eta p(z_t|x_t) \int p(x_t|x_{t-1}, u_t) p(x_{t-1}|z_{1:t-1}, u_{1:t-1}) dx_{t-1}$ (Markov assumption)
6. $= \eta p(z_t|x_t) \int p(x_t|x_{t-1}, u_t) p(x_{t-1}|z_{1:t-1}, u_{1:t-1}) dx_{t-1}$ (Markov assumption)
7. $= \eta p(z_t|x_t) \int p(x_t|x_{t-1}, u_t) bel(x_{t-1}) dx_{t-1}$ (Recursive term)

Bayes filter can be written into a 2-step prediction and correction process.

1. Prediction Step:
$$ \overline{bel(x_t)} = \int p(x_t | u_t, x_{t-1}) \, bel(x_{t-1}) \, dx_{t-1} $$

2.  Correction Step:
$$ bel(x_t) = \eta \, p(z_t | x_t) \, \overline{bel(x_t)} $$

- **Motion model**: $p(x_t | u_t, x_{t-1})$
- **Sensor/observation model**: $\eta \, p(z_t | x_t)$

### Bayes Filter Framework:
- **Given**:
  - Stream of observations $z_{1:t}$ and control actions $u_{1:t}$
  - Sensor/measurement model: $p(z_t | x_t)$
  - Action/motion/transition model: $p(x_t | x_{t-1}, u_{t})$

- **Want**:
  - The state $x_t$ of dynamic system
  - The posterior of state as called belief:
    $$ bel(x_t) = p(x_t | z_{1:t}, u_{1:t}) $$

**Copy Pseudocode Slide 20**

### Bayes Filters Examples

#### Linear:
- Kalman Filter
- Information Filter
#### Nonlinear:
- Extended Kalman Filter
- Extended Information Filter
- Particle Filter

### Discrete-Time White Noise

- A discrete-time random process $w_k$ is called White Noise if:
$$E[w_k w_j^T] = Q_k \delta_{kj};$$

- Where the Kronecker $\delta_{kj}$ is:
$$\delta_{kj} = \begin{cases} 
1 & \text{if } k = j; \\
0 & \text{if } k \neq j;
\end{cases}$$

### Gauss-Markov Process

- The state of a dynamic system excited by white noise $(x_{k+1} = f(x_k, w_k))$ is a discrete-time Markov process or Markov sequence.

The state of a linear dynamic system excited by white Gaussian noise $(x_{k+1} = F_k x_k + w_k)$ is called a Gauss-Markov process.

## Kalman Filter (KF) Assumptions

- The state $x_k$ evolves according to some known linear dynamic equation with:
  - Known inputs $u_k$
  - Additive process noise $(w_k)$ that has a known covariance $Q_k$:
  $$
  \bar{x}_k = F_k x_{k-1} + G_k u_k + w_k
  $$

- Measurement model is known linear function of the state with:
  - Additive measurement noise, $v_k$, with known covariance $R_k$:
  $$
  z_k = H_k \bar{x}_k + v_k
  $$

## Kalman Filter Estimation Cycle:
- State and measurement prediction
- State update (correction)

**Copy KF ALGO**