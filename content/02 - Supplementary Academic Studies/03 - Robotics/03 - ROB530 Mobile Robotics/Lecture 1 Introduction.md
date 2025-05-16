## Joint and Conditional Distributions

- Let $X$ and $Y$ be 2 random variables.

- The **joint probability** of $X$ and $Y$ is:
$$
P(X, Y) = P(X = x \text{ and } Y = y)
$$

- If $X$ and $Y$ are independent:
$$
P(X, Y) = P(X) P(Y)
$$

- The **conditional probability** is:
$$
P(X|Y) = \frac{P(X, Y)}{P(Y)} \quad ; \quad P(Y) > 0
$$

## Marginalization

- Given $P(X, Y)$, the marginal distribution of $X$ can be computed by summing (integrating) over $Y$.
$$
P(X) = \sum_{y \in Y} P(X, Y) = \sum_{y \in Y} P(X|Y) P(Y)
$$
- Continuous:

$$
p(x) = \int_{y \in Y} p(x, y) \, dy = \int_{y \in Y} p(x|y)p(y) \, dy
$$

### Bayes' Rule

$$
p(x, y) = p(x|y)p(y) = p(y|x)p(x)
$$

$$
p(x|y) = \frac{p(y|x)p(x)}{p(y)} = \frac{p(y|x)p(x)}{\sum_{x \in X} p(y|x)p(x)}
$$

$$
\text{Posterior} = \frac{\text{Likelihood} \times \text{Prior}}{\text{Evidence (marginal likelihood)}}
$$

### Bayes' Rule with Prior Knowledge

Given 3 random variables $X$, $Y$, $Z$, Bayes' rule relates the prior probability $p(x|z)$ and the likelihood function $p(y|x,z)$ as:

$$
p(x|y,z) = \frac{p(y|x,z)p(x|z)}{p(y|z)}
$$

Given $Z$ and that $X$ and $Y$ are conditionally independent:
$$
p(x, y|z) = p(x|z)p(y|z)
$$
## Univariate Normal Distribution

- The univariate (1-D) Gaussian distribution with mean $\mu$ and variance $\sigma^2$ has the following PDF:

$$
p(x) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left( -\frac{1}{2} \frac{(x - \mu)^2}{\sigma^2} \right)
$$

- This is often written as:

$$
x \sim \mathcal{N}(\mu, \sigma^2)
$$

$$
\mathcal{N}(x; \mu, \sigma^2)
$$

## Multivariate Normal Distribution

- The multivariate Gaussian distribution of an $n$-dimensional random vector $x \sim \mathcal{N}(\mu, \Sigma)$ with mean $\mu = \mathbb{E}(x)$ and covariance $\Sigma = \text{Cov}(x) = \mathbb{E}[(x - \mu)(x - \mu)^T]$ is:

$$
p(x) = (2\pi)^{-\frac{n}{2}} |\Sigma|^{-\frac{1}{2}} \exp\left( -\frac{1}{2} (x - \mu)^T \Sigma^{-1} (x - \mu) \right)
$$

- $\mu \in \mathbb{R}^n$
- $\Sigma \in \mathbb{R}^{n \times n}$

## Marginalization and Conditioning of Normal Distribution

- Let $x$ and $y$ be jointly Gaussian random vectors:
$$
\begin{bmatrix}
x \\
y
\end{bmatrix}
\sim \mathcal{N} \left( \begin{bmatrix}
\mu_x \\
\mu_y
\end{bmatrix}, \begin{bmatrix}
A & C \\
C^T & B
\end{bmatrix} \right)
$$

- The marginal distribution of $x$ is:
$$
x \sim \mathcal{N}(\mu_x, A)
$$

- The conditional distribution of $x$ given $y$ is:
$$
x|y \sim \mathcal{N}(\mu_x + C B^{-1} (y - \mu_y), A - C B^{-1} C^T)
$$

## Bayes Filter

### Framework:
- **Given:**
  - Stream of observations $z_{1:t}$ and action data $u_{1:t}$
  - Sensor measurement model $p(z_t | x_t)$
  - Action/motion/transition model $p(x_t | x_{t-1}, u_t)$

- **Want:**
  - The state $x_t$ of dynamical system
  - The posterior of state is called belief:
  $$
  bel(x_t) = p(x_t | z_{1:t}, u_{1:t})
  $$

```pseudo
\begin{algorithm}
\caption{Bayes Filter}
\begin{algorithmic}
\REQUIRE $p(x_{t-1} | z_{1:t-1}, u_{1:t-1})$
\FOR{each time step $t$}
    \STATE Observe $z_t$
    \STATE Apply action $u_t$
    \STATE Compute prediction:
    \STATE $p(x_t | z_{1:t-1}, u_{1:t}) = \int p(x_t | x_{t-1}, u_t) p(x_{t-1} | z_{1:t-1}, u_{1:t-1}) dx_{t-1}$
    \STATE Compute belief update:
    \STATE $p(x_t | z_{1:t}, u_{1:t}) \propto p(z_t | x_t) p(x_t | z_{1:t-1}, u_{1:t})$
\ENDFOR
\end{algorithmic}
\end{algorithm}
```
