**Line search methods involve the iteration of form:**

$$ x_{k+1} = x_k + \alpha_k p_k, \quad k = 0, 1, 2, \ldots $$

for some vector $p_k \in \mathbb{R}^n$ and step sizes $\alpha_k \geq 0$.

- Gradient descent is a line search method with $p_k = -\nabla f(x_k)$ at each iteration.

## Descent Direction

A vector $p_k \in \mathbb{R}^n$ is a descent direction of $f \in C^1$ at $x_k \in \mathbb{R}^n$ if:

$$ p_k^T \nabla f(x_k) < 0 $$

**Candidates for descent direction:**

1. **Gradient method:** $p_k = -\nabla f(x_k)$
2. **Newton method:** $p_k = -B_k \nabla f(x_k)$ where $B_k = \nabla^2 f(x)$
3. **Quasi-Newton methods:** $p_k = -B_k^{-1} \nabla f(x_k)$ where $B_k \approx \nabla^2 f(x)$
4. **Generally:** $p_k = -B_k^{-1} \nabla f(x_k)$ where $B_k$ is symmetric and positive definite.

- If $B_k$ is not symmetric and positive definite, $B_k^{-1} \nabla f(x_k)$ may not be a descent direction.

# Exact Line Search Problem

- Exact line search problem:

$$\min_{\alpha > 0} \Phi(\alpha) \quad \text{where} \quad \Phi(\alpha) = f(x_k + \alpha p_k)$$

$$\Phi'(\alpha) = \nabla f(x_k + \alpha p_k)^T p_k$$

$$\Phi'(0) = \nabla f(x_k)^T p_k$$

## The Wolfe Conditions

- **1st criterion of favorable step size** (Armijo condition - sufficient decrease):

$$f(x_k + \alpha p_k) \leq f(x_k) + \alpha c_1 \nabla f(x_k)^T p_k \quad \text{for some} \quad c_1 \in (0, 1)$$

- Essentially, the new step $f(x_k + \alpha p_k)$ should be below the line of $\Phi(\alpha)$.

- **Condition 2 (curvature condition):**

$$\nabla f(x_k + \alpha p_k)^T p_k \geq c_2 \nabla f(x_k)^T p_k \quad \text{for some} \quad c_2 \in (c_1, 1), \quad c_2 \sim 0.1 \rightarrow 0.9$$

- This condition helps in avoiding small step sizes.

### Wolfe Conditions

- Let $p_k$ be a descent direction of $f \in C^1$ at $x_k$. Then $\alpha_k > 0$ satisfies the Wolfe conditions if:

$$
f(x_k + \alpha_k p_k) \leq f(x_k) + \alpha_k c_1 \nabla f(x_k)^T p_k \tag{1}
$$

and

$$
\nabla f(x_k + \alpha_k p_k)^T p_k \geq c_2 \nabla f(x_k)^T p_k \tag{2}
$$

- with $0 < c_1 < c_2 < 1$.

- **Strong Wolfe conditions** modify (2):

$$
|\nabla f(x_k + \alpha_k p_k)^T p_k| \leq c_2 |\nabla f(x_k)^T p_k| \tag{3}
$$

by preventing $\Phi'(\alpha_k)$ from being too positive.

### Existence of Favorable Step Sizes

**Lemma 2:** Let $p_k$ be a descent direction of $f \in C^1$ at $x_k$. Suppose $\phi(\alpha) = f(x_k + \alpha p_k)$ is bounded below for $\alpha > 0$. Then there exist intervals of step sizes satisfying the Wolfe conditions and the strong Wolfe conditions.

## Convergence of Line Search Methods

**Theorem 3:**

Let $x_{k+1} = x_k + \alpha_k p_k$. Assume for each $k \geq 0$ that $p_k$ is a descent direction and that $\alpha_k$ satisfies the Wolfe conditions. Assume also that $f$ is bounded below and continuously differentiable in an open set $\mathcal{N}$ that contains:

$$ \{ x \in \mathbb{R}^n : f(x) \leq f(x_0) \} $$

Furthermore, assume that $f$ is $L$-smooth on $\mathcal{N}$. Then:

$$
\sum_{k=0}^{\infty} \cos^2 \theta_k \| \nabla f(x_k) \|_2^2 < \infty \quad (4)
$$

where $\theta_k$ denotes the angle between $p_k$ and $-\nabla f(x_k)$, defined as:

$$
\cos \theta_k = \frac{-\nabla f(x_k)^T p_k}{\| \nabla f(x_k) \|_2 \| p_k \|_2}
$$

- Equation (4) is known as the **Zoutendijk condition**.

This condition implies:

$$
\cos^2 \theta_k \| \nabla f(x_k) \|_2^2 \to 0
$$

If $p_k$ is chosen so that $\theta_k$ is bounded away from $90^\circ$, i.e., there is $\delta > 0$ such that $\cos \theta_k \geq \delta > 0$ for all $k$, then **global convergence** follows from any $x_0$:

$$
\lim_{{k \to \infty}} \| \nabla f(x_k) \|_2 = 0
$$

## Convergence in General Line Search Algorithms

**Theorem 4:**

- Consider any algorithm that satisfies:
  1. Every iteration decreases the objective function.
  2. Every nth iteration is a steepest descent step with step size satisfying the Wolfe conditions.
  
Then:

$$
\lim_{{k \to \infty}} \| \nabla f(x_{n_k}) \|_2 = 0
$$

**COPY ALGOS**


