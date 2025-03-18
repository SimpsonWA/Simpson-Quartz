## 2.2 Basic Concepts in Probabilities

- Let $X$ denote a random variable and $x$ denote a specific event $X$ might take on.

- If all values that $X$ can be are discrete, we can write:
  $$
  P(X = x)
  $$
  to denote the probability that random variable $X$ has value $x$.

- Discrete probabilities must sum to one, which is to say:
  $$
  \sum_x P(X = x) = 1
  $$

- Commonly, we will exclude the random variable and abbreviate as $P(x)$ instead of $P(X = x)$.

- Normal distribution (Gaussian function) (PDF):
  $$
  P(x) = (2 \pi \sigma^2)^{-1/2} \exp \left\{ -\frac{1}{2} \left( \frac{x - \mu}{\sigma} \right)^2 \right\}
  $$

  - $\sigma^2$: variance
  - $\mu$: mean

- This normal distribution is commonly abbreviated as:
  $$
  \mathcal{N}(x_j, \mu, \sigma^2)
  $$

- Commonly $X$ is dependent on multiple variables so $X \in \mathbb{R}^n$

- Normal distributions over vectors are called **Multivariate**:

- Multivariate normal distribution density function:
  $$
  P(X) = \text{Det}(2\pi\Sigma)^{-\frac{1}{2}} \exp \left\{ -\frac{1}{2} (x - \mu)^T \Sigma^{-1} (x - \mu) \right\}
  $$

  - $\mu$: mean vector
  - $\Sigma$ (positive semidefinite symmetric matrix): covariance matrix

- Discrete probability density functions integrate to 1:
  $$
  \int P(x) dx = 1
  $$

- **Joint distribution** given by:
$$
  P(X = x, Y = y) = P(\bar{X} = x \text{ and } \bar{Y} = y)
  $$
- **Joint probability**: describes the probability that the random variable $X$ takes on the value $x$ and that $Y$ takes on value $y$.

- If $x$ and $y$ are **independent**:
  $$
  P(x,y) = P(x)P(y)
  $$

- **Conditional**: probability of $x$ occurring given $y$
  $$
  P(X|Y) = P(X = x | Y = y)
  $$
  If $P(y) > 0$
  $$
  P(X|Y) = \frac{P(x,y)}{P(y)}
  $$

- If $x$ and $y$ are independent, then:
  $$
  P(X|Y) = \frac{P(x)P(y)}{P(y)} = P(x)
  $$

- **Theorem of total probability**:
  $$
  P(x) = \sum_y P(x|y)P(y) \quad \text{(discrete)}
  $$
  $$
  P(x) = \int P(x|y)P(y) \, dy \quad \text{(continuous)}
  $$
- **Bayes' Rule**: relates conditional $p(x|y)$ to its inverse $p(y|x)$ with $p(y) > 0$:
  $$
  p(x|y) = \frac{p(y|x) p(x)}{p(y)} = \frac{p(y|x) p(x)}{\sum_{x'} p(y|x') p(x')} \quad \text{(discrete)}
  $$

  $$
  p(x|y) = \frac{p(y|x) p(x)}{p(y)} = \frac{p(y|x) p(x)}{\int p(y|x') p(x') dx} \quad \text{(continuous)}
  $$

- $x$: the variable we want to infer from $y$.
- $p(x)$: prior probability distribution.
- $p(x|y)$: posterior probability distribution over $x$.
- Commonly, we write $p(y)^{-1}$ as $\eta$ (the normalizer variable):
  $$
  p(x|y) = \eta p(y|x) p(x)
  $$

## Expectation and Covariance

- The **expectation** of a random variable $X$:
  $$
  \mathbb{E}[X] = \sum_x x p(x)
  $$

  $$
  \mathbb{E}[X] = \int x p(x) dx
  $$

- The **covariance** of $X$:
  $$
  \text{Cov}[X, X] = \mathbb{E}[X^2] - \mathbb{E}[X]^2
  $$

  $$
  \text{Cov}[X] = \Sigma
  $$
  - **Entropy**: the expected information that $x$ carries:
  $$
  H(p) = \mathbb{E}[-\log_2 p(x)] = - \sum_x p(x) \log_2 p(x)
  $$

- where $-\log_2 P(x)$ is the number of bits needed to encode $x$ using optimal encoding.

- Adding conditional $z=z$ for Bayes' Rule:
  $$
  P(x|y,z) = \frac{P(y|x,z) \, P(x|z)}{P(y|z)}
  $$

  $$
  P(x,y|z) = P(x|z) \, P(y|z)
  $$

- **Conditional independence**:
  $$
  P(x|z) = P(x|z,y)
  $$

  $$
  P(y|z) = P(y|z,x)
  $$

- Conditional independence applies whenever a variable $y$ carries no info about a variable $x$ if another variable's value $z$ is known.

## 2.3 Robot Environment Interaction

### 2.3.1 State

- Environments are categorized by states.
- State is essentially the collection of all aspects of the robot and its environment that can impact the future.
- Denote state as $X$, state at time $t$ as $X_t$.
- State variables used in proceeding text:
  - Robot pose: the location and orientation relative to a global coordinate frame.
  - Configuration of robot's actuator.
  - The robot velocity.
  - Location and surrounding features.
  - Location and velocities of moving objects/people, etc.
- A state $X_t$ is **complete** if it is the best predictor of the future.

## 2.3.2 Environment Interaction

Two fundamental types of interactions between a robot and its environment:

1. Robot can influence the state of its environment through its actuators.
2. Robot can gather info about its state through its sensors.

### Sensor Measurements
Perception is the process by which the robot uses its sensors to obtain information about the state of its environment.

### Control Actions
Change the state of the world by actively asserting forces on the robot's environment (robot motion & manipulation of objects).

### Measurement Data Notation

- $Z_t$
- $Z_{t_1:t_2} = Z_{t_1}, Z_{t_1+1}, Z_{t_1+2}, \ldots, Z_{t_2}$

### Control Data Notation

- $U_t$
- $U_{t_1:t_2} = U_{t_1}, U_{t_1+1}, U_{t_1+2}, \ldots, U_{t_2}$

## 2.3.3 Probabilistic Generative Laws

- A state at time $x_t$ is generated stochastically, so it makes sense to specify a probability distribution from which $x_t$ is generated.

- Since $x_t$ is probably conditioned by all past states, measurements, and controls, we can write the distribution as:
  $$
  P(x_t | x_{0:t-1}, z_{1:t-1}, u_{1:t})
  $$

  ...here we assume we take a control action at $u_t$ after a measurement $z_t$.

- However, if state $x$ is complete, then it is a sufficient summary of all that happened in previous time steps:
  $$
  P(x_t | x_{0:t-1}, z_{1:t-1}, u_{1:t}) = P(x_t | x_{t-1}, u_t)
  $$

  This property is called **conditional independence**.

- Similarly, we may want to model the process by which measurements are taking place. If $x_t$ is complete, we can use conditional independence to get:
  $$
  P(z_t | x_{0:t}, z_{1:t-1}, u_{1:t}) = P(z_t | x_t)
  $$
- Which is to say the state $x_t$ is sufficient to predict the measurement $z_t$.

- **State transition probability**: $p(x_t | x_{t-1}, u_t)$
  - Sometimes written as $p(x' | x, u)$

- **Measurement probability**: $p(z_t | x_t)$
  - Also written as $p(z | x)$

### 2.3.4 Belief Distributions

- **Belief**: reflects the robot's internal knowledge about the state of an environment.

- Belief distributions are posterior probabilities. We denote the belief over a state variable $x_t$ by $bel(x_t)$ which is:

$$
bel(x_t) = p(x_t | z_{1:t}, u_{1:t})
$$

- So this is a probability distribution over the state $x_t$ at time $t$ conditioned on all past measurements $z_{1:t}$ and all past controls $u_{1:t}$.

- Sometimes we calculate the posterior before measurement but after control execution:

$$
\overline{bel}(x_t) = p(x_t | z_{1:t-1}, u_{1:t})
$$
## 2.4 Bayes Filters

### 2.4.1 The Bayes Filter Algorithm

The Bayes filter algorithm is commonly used to calculate the beliefs.

**Pseudo Code:**
```pseudo 
\begin{algorithm}
\caption{Bayes\_Filter}
\begin{algorithmic}
\REQUIRE $bel(x_{t-1})$, $u_t$, $z_t$
\FORALL{$x_t$}
    \STATE $bel(x_t) = \eta \, p(z_t | x_t) \int p(x_t | u_t, x_{t-1}) \, bel(x_{t-1}) \, dx$
\ENDFOR
\RETURN $bel(x_t)$
\end{algorithmic}
\end{algorithm}
```

### 2.4.2 Example

Based on a robot estimating the state of a door using a camera:

1. Initially, set equal prior probabilities to the two possible door states:
   - $bel(x_t = \text{open}) = 0.5$
   - $bel(x_t = \text{closed}) = 0.5$

2. Assume the sensor is noisy and characterized by:
   - $P(z_t = \text{sensed\_open} | x_t = \text{open}) = 0.6$
   - $P(z_t = \text{sensed\_open} | x_t = \text{closed}) = 0.4$

- $P(z_t = \text{sensed\_open} \mid X_t = \text{closed}) = 0.2$

- $P(z_t = \text{sensed\_closed} \mid X_t = \text{closed}) = 0.8$

3) Finally, assume the robot uses a manipulator to push the door open. If the door is already open, it remains open. If closed, there is a $0.8$ chance that it will open after the action:

$$
P(X_t = \text{open} \mid U_t = \text{push}, x_{t-1} = \text{open}) = 1
$$

$$
P(X_t = \text{closed} \mid U_t = \text{push}, x_{t-1} = \text{open}) = 0
$$

$$
P(X_t = \text{open} \mid U_t = \text{push}, x_{t-1} = \text{closed}) = 0.8
$$

$$
P(X_t = \text{closed} \mid U_t = \text{push}, x_{t-1} = \text{closed}) = 0.2
$$

It can also choose not to use the manipulator, which would leave the probabilities as:

$$
P(X_t = \text{open} \mid U_t = \text{none}, x_{t-1} = \text{open}) = 1
$$

$$
P(X_t = \text{closed} \mid U_t = \text{none}, x_{t-1} = \text{open}) = 0
$$

$$
P(X_t = \text{open} \mid U_t = \text{none}, x_{t-1} = \text{closed}) = 0
$$

$$
P(X_t = \text{closed} \mid U_t = \text{none}, x_{t-1} = \text{closed}) = 1
$$

Suppose at time $t$ the robot takes no action and senses the door to be open. The resulting posterior belief is calculated by:

$$
bel(x_t) = \int P(x_t \mid u_t, x_0) \, bel(x_0) \, dx_0
$$

For discrete states:

$$
bel(x_t) = \sum_{x_0} P(x_t \mid u_t, x_0) \, bel(x_0)
$$
$$
p(x_t \mid U_t = \text{None}, \bar{x}_0 = 25-\text{open}) bel(x_0 = 25-\text{open}) + \\
p(x_t \mid U_t = \text{None}, x_0 = 25-\text{closed}) bel(x_0 = 25-\text{closed})
$$

We can now sub in the 2 possible values for the state variable $x_t$. For hypothesis $x_t = 25-\text{open}$ we obtain:

$$
bel(x_t = 25-\text{open}) = p(x_t = 25-\text{open} \mid U_t = \text{none}, x_0 = 25-\text{open}) * \\
bel(x_0 = 25-\text{open}) + p(x_t = 25-\text{open} \mid U_t = \text{none}, x_0 = 25-\text{closed}) * \\
bel(x_0 = 25-\text{closed}) \\
= 1.0 * 0.5 + 0 * 0.5 = 0.5
$$

'Likewise' for closed:

$$
bel(x_t = 25-\text{closed}) = p(x_t = 25-\text{closed} \mid U_t = \text{none}, x_0 = 25-\text{open}) * \\
bel(x_0 = 25-\text{open}) + p(x_t = 25-\text{closed} \mid U_t = \text{none}, x_0 = 25-\text{closed}) * \\
bel(x_0 = 25-\text{closed}) \\
= 0.5
$$

Moving to line 4 of Bayes filter algo:

$$
bel(x_t) = \eta p(z_t = \text{sensed-open} \mid x_t) bel(x_t)
$$

(This has 2 cases for $x_t = 25-\text{open}$ and $x_t = 25-\text{closed}$)

$$
bel(x_t = 25-\text{open}) = \eta p(z_t = \text{sensed-open} \mid x_t = 25-\text{open}) bel(x_t = 25-\text{open}) \\
= \eta 0.6 (0.5) = \eta 0.3
$$

$$
bel(x_t = 25-\text{closed}) = \eta 0.1 (0.5) = \eta 0.1
$$

We can now calculate the multiplier $\eta$ as:
$$
\eta = (0.3 + 0.1)^{-1} = 2.5
$$

So we have:
$$
bel(x_1 = x_5 - \text{open}) = 0.75
$$
$$
bel(x_1 = x_5 - \text{closed}) = 0.25
$$

This calculation is now easily iterated. Let's verify for $u_2 = \text{push}$ and $z_2 = \text{sensed-open}$ we get:
$$
\overline{bel}(x_2 = x_5 - \text{open}) = 1 \cdot 0.75 + 0.8 \cdot 0.25 = 0.95
$$
and
$$
\overline{bel}(x_2 = x_5 - \text{closed}) = 0 \cdot 0.75 + 0.2 \cdot 0.25 = 0.05
$$

$$
bel(x_2 = x_5 - \text{open}) = 0.6 \cdot 0.95 = 0.983
$$
$$
bel(x_2 = x_5 - \text{closed}) = 0.2 \cdot 0.05 = 0.017
$$
