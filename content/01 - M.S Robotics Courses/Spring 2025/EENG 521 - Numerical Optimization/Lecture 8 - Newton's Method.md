- 2nd order algorithm (uses $\nabla^2$)

## Newton's method

- Line search method iterations:
  $$
  x_{k+1} = x_k + \alpha_k p_k \quad k = 0, 1, 2, \ldots
  $$
  For some $p_k \in \mathbb{R}^n$ and step sizes $\alpha_k > 0$

- Newton's method is a **line search method** with choice of step direction and step size:
  $$
  p_k = -(\nabla^2 f(x_k))^{-1} \nabla f(x_k)
  $$
  $\alpha_k = 1$ (for pure Newton's method)

- As shown before if $\nabla f \neq 0$ then $-\nabla f$ is the steepest descent direction, and if $\nabla^2 f(x_k)$ is positive definite then the above guarantees $p_k$ is a descent direction for $x_k$.

- Newton method iterations:
  $$
  x_{k+1} = x_k + (-\nabla^2 f(x_k))^{-1} \nabla f(x_k)
  $$

- This is just a generalization of the univariate ($n=1$) Newton method for finding zeros of $f'(x)$:
  $$
  x_{k+1} = x_k - \frac{f'(x_k)}{f''(x_k)}
  $$

## Something about slide 6


- Consider the 1st order Taylor expansion of $\nabla f(x)$ at $x_n$:

$$
\nabla f(x_n + p) \approx \nabla f(x_n) + \nabla^2 f(x_n) p
$$

- If $\nabla^2 f(x)$ is positive definite, then the right-hand side is:

$$
p = - \left( \nabla^2 f(x_n) \right)^{-1} \nabla f(x_n)
$$

- So the Newton step aims to find a stationary point of $f$.

## Local convergence of Newton's method

**Theorem 1:**

Suppose $f \in C^2$ and let $x^*$ be a local minimizer at which $\nabla^2 f(x^*)$ is symmetric and positive definite. Suppose also $\nabla f$ is Lipschitz continuous in a neighborhood of $x^*$ with constant $L$. Consider Newton's method:

$$
x_{n+1} = x_n - \left( \nabla^2 f(x_n) \right)^{-1} \nabla f(x_n)
$$

- Then if $x_0$ is sufficiently close to $x^*$ we have:
  1. $x_n \to x^*$ quadratically, that is, $\| x_{n+1} - x^* \|_2 \leq \text{const} \cdot \| x_n - x^* \|_2^2$
  2. $\| \nabla f(x_n) \| \to 0$ quadratically, that is, $\| \nabla f(x_{n+1}) \|_2 \leq \text{const} \cdot \| \nabla f(x_n) \|_2^2$

---

**Remarks:**

- In general, Newton's method is not globally convergent, but due to Theorem 7, we can see quadratic convergence as very fast convergence. Implementation considerations and Hessian modifications.

**Computing the Step Direction**

- In practice, to obtain:

$$
p_k = -(\nabla^2 f(x_k))^{-1} \nabla f(x_k)
$$

- We don't have to invert the Hessian; rather $p_k$ can be modeled as solving a linear system of equations:

$$
\nabla^2 f(x_k) p_k = -\nabla f(x_k)
$$

**Modifying Hessians that are not positive definite**

- In general (and further away from $x^*$), the Hessian matrix $\nabla^2 f(x_k)$ may not be positive definite or invertible, so the solutions to

$$
\nabla^2 f(x_k) p_k = -\nabla f(x_k)
$$

- may not be descent directions.

- One way around this is to replace the Hessian by:

$$
B_k = \nabla^2 f(x_k) + E_k
$$

- $E_k$ is chosen to ensure that $B_k$ is sufficiently positive definite.

---

---

### COme back and the slides of the 3 methods

## Convergence of modified Newton's method

**Def 2: Bounded modified factorization:**

A sequence of modified Hessian matrices $\{B_k\}$ satisfies the bounded modified factorization property if there exists $C > 0$ such that for all $k$

$$
\|B_k\| \|B_k^{-1}\|_2 \leq C
$$

- Whenever the sequence of Hessians $\{\nabla^2 f(x_k)\}$ is bounded

**Theorem 3:**

- Let $f \in C^2$ and assume that $x_0$ is chosen such that

$$
\{x \in \mathbb{R}^n \mid f(x) \leq f(x_0)\}
$$

is compact. Then, if $\{B_k\}$ satisfies the bounded modified factorization property we have:

$$
\lim_{k \to \infty} \nabla f(x_k) = 0
$$

---
