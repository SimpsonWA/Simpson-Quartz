
## Secant method for $n = 1$

- Like Newton's method (univariate method) $(n = 1)$, Secant method is a root finding algorithm that can be used for finding zeros of $f'(x)$:

$$
x_{n+1} = x_n - \frac{f'(x_n)(x_n - x_{n-1})}{f'(x_n) - f'(x_{n-1})}
$$

- We can interpret the Secant method as:

$$
x_{n+1} = x_n - \frac{f(x_n)}{\frac{f(x_n) - f(x_{n-1})}{x_n - x_{n-1}}}
$$

- The denominator is an approximation of $f'(x_k)$ (but is formed only using first order info). This is Newton-like, but the Secant method is called Quasi-Newton method.

## Generalizing Secant method for $n > 1$

- Quasi-Newton methods involve iterations of the form:

$$
x_{n+1} = x_n - \alpha (B_n)^{-1} \nabla f(x_n)
$$
- Where $B_n$ is some approximation of the Hessian $\nabla^2 f(x_n)$ that is constructed using 1st order information.

**Secant equation**

Taking the 1st order Taylor expansion of $\nabla f(x)$ at $x_n$ and considering the expansion at $x_{n-1}$:

$$\nabla f(x_{n-1}) \equiv \nabla f(x_n) + \nabla^2 f(x_n) (x_{n-1} - x_n)$$

Define vectors:

$s_{n-1} = x_n - x_{n-1}$ and $y_{n-1} = \nabla f(x_n) - \nabla f(x_{n-1})$

We have an approximation that the true Hessian satisfies: $\nabla^2 f(x_n) s_{n-1} \approx y_{n-1}$. This leads to the secant equation, which we can require an approximation $B_n$ to satisfy:

$$B_n s_{n-1} = y_{n-1}$$

$$[n \times n] [n \times 1] = [n \times 1] \text{ : well determined}$$

**Optimization problem**

For clearer notation, we will rewrite the secant equation as:

$$B_{n+1} s_n = y_n \text{ (same as } B_n s_{n-1} = y_{n-1})$$
We have:

$$ s_k = x_{k+1} - x_k \quad \text{and} \quad y_k = \nabla f(x_{k+1}) - \nabla f(x_k) $$

To reduce the remaining degrees of freedom and determine $B_{k+1}$ uniquely, it is common to solve the problem: (to find $B_{k+1}$)

$$ \min_B \| B - B_k \| \quad (1) $$

subject to: $B = B^T$, $B s_k = y_k$

(1) solves the closest symmetric matrix to $B_k$ that satisfies the secant method. Different norms give different quasi-Newton methods.

**DFP update**

Choosing a weighting $W$ norm:

$$ \| A \\|_W = \| W^{1/2} A W^{1/2} \|_F $$

With a particular choice of $W$, problem (1) has an explicit solution:

$$ B_{k+1} = (I - \rho_k y_k s_k^T) B_k (I - \rho_k s_k y_k^T) + \rho_k y_k y_k^T $$

where $\\rho_k$:

$$ \rho_k = \frac{1}{y_k^T s_k} \quad \text{(scalar)} $$

This is called the Davidon–Fletcher–Powell or DFP update.

### Approximating and updating Hessian Inverse (DFP update)

- The Newton's method requires the inverse Hessian matrix rather than updating $B_n$ at each iteration and having:
$$
x_{k+1} = x_k - \alpha (B_n)^{-1} \nabla F(x_k)
$$
We can instead update $H_k = B_n^{-1}$ (which is an approximation of the inverse of $B_n$) at each iteration:
$$
x_{k+1} = x_k - \alpha_k H_k \nabla F(x_k)
$$

### DFP update (Revised)

- Recall the DFP update for $B_{n+1}$ is given by:
$$
B_{n+1} = (I - p_k y_k^T s_k^T) B_n (I - p_k s_k y_k^T) + p_k s_k y_k^T
$$

- Using the Sherman-Morrison-Woodbury formula:
$$
(A + U V^T)^{-1} = A^{-1} - A^{-1} U (I + V^T A^{-1} U)^{-1} V^T A^{-1}
$$

- It is possible to derive the following DFP update for $H_{n+1} = B_n^{-1}$:
$$
H_{n+1} = H_k - \frac{H_k y_k y_k^T H_k}{y_k^T H_k y_k} + \frac{s_k s_k^T}{y_k^T s_k}
$$

- This reveals that we only need to compute a rank-2 update to $H_k$ at each iteration:
$$
H_{k+1} = H_k + U_k \quad \text{rank}(U_k) = 2
$$
### From DFP to BFGS

- We can make a small derivation to use a new Quasi-Newton method BFGS (Broyden, Fletcher, Goldfarb, and Shanno). Recall the secant equation for BFGS:

$$
B_{k+1}s_k = y_k
$$

- Noting $H_{k+1} = B_{k+1}^{-1}$, we can write:

$$
H_{k+1}y_k = s_k
$$

- The BFGS method is based on the following optimization problem to obtain $H_{k+1}$:

$$
\min_H \|H - H_k\|
$$

s.t. $H = H^T$, $Hy_k = s_k$ (2)

- The solution to (2) provides the BFGS update for the inverse Hessian approximation:

$$
H_{k+1} = (I - \rho_k s_k y_k^T) H_k (I - \rho_k y_k s_k^T) + \rho_k s_k s_k^T
$$

- Where $\rho_k = (y_k^T s_k)^{-1}$

# Convergence

## BFGS: Hereditary Positive Definiteness

### Theorem 1:
Let $H_k$ be symmetric and positive definite. Then the BFGS update:

$$
H_{k+1} = (I - \rho_k s_k y_k^T) H_k (I - \rho_k y_k s_k^T) + \rho_k s_k s_k^T
$$

is symmetric and positive definite iff $s_k^T y_k > 0$.

### Corollary 2:
If $H_0$ is symmetric and positive definite and all $s_k^T y_k > 0$ for all $k$, then $H_k$ are symmetric and positive definite. It follows that all step directions $p_k = -H_k \nabla f(x_k)$ are descent directions.

## Global Convergence of BFGS

### Theorem 3:
Assume:
- $f \in C^2$ and the level set $L = \{ x \in \mathbb{R}^n : f(x) \leq f(x_0) \}$ is convex
- $H_0$ is symmetric and positive definite
- There exist positive constants $m$ and $M$ such that:

$$
m \|z\|^2 \leq z^T \nabla^2 f(x) z \leq M \|z\|^2
$$

for all $z \in \mathbb{R}^n$ and $x \in L$. Then $f$ is strongly convex in $L$ with constant $m$ and has Lipschitz gradients with constant $M$.

Then the sequence $\{x_k\}$ generated by the BFGS with each $d_k$ satisfying the Wolfe conditions converges to a unique $x^*$ of $f$ in $L$.

# Local Convergence Rate of BFGS

**Theorem 4:**

Suppose the assumptions of Theorem 3 hold and that the BFGS iterates $x_k$ converge to a minimizer $x^*$ at which $\nabla^2 f$ is Lipschitz continuous:

$$
\|\nabla f(x) - \nabla f(x^*)\|_2 \leq L \|x - x^*\|_2 \quad \forall x
$$

Then $x_k \to x^*$ superlinearly. That is $\|x_{k+1} - x^*\|_2 = o(\|x_k - x^*\|_2)$.
