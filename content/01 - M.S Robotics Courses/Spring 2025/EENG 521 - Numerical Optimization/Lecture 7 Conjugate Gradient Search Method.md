## Linear Conjugate Gradient Method

- Consider the linear system of equations: $$ Ax = b \quad (1) $$
    
- Where $A \in \mathbb{R}^{n \times n}$ is symmetric and positive definite.
    
- The unique solution to (1) is given by the quadratic optimization problem: $$ \min_{x \in \mathbb{R}^n} \varphi(x) = \frac{1}{2} x^T A x - b^T x \quad (2) $$
    
- At any point $x \in \mathbb{R}^n$, the residual of the linear system $Ax = b$, denoted $r(x) \in \mathbb{R}^n$, is defined as: $$ r(x) := Ax - b $$
    
- $r(x)$ is equal to the gradient of the quadratic function $\varphi$ at $x$: $$ \nabla \varphi(x) = Ax-b = r(x)$$


### Definition: Conjugate Directions

- A collection of non-zero vectors $\{p_0, p_1, \ldots, p_{n-1}\}$ is said to be conjugate with a symmetric and positive definite matrix $A$ if: $$ p_i^T A p_j = 0 \quad \text{for all } i \neq j $$

*These vectors are sometimes referred to as $\Lambda$-conjugate or $\Lambda$-orthogonal.*

*With $\Lambda$-conjugate search directions, an iterative algorithm with exact line search will converge to $x^*$ in at most $\Lambda$ steps.*

### CG Iterations (Naive)

Let $x_0 \in \mathbb{R}^n$ be the starting point. Compute the residual $r_0 = Ax_0 - b$, and let the first search direction $p_0 = -r_0$. The algorithm proceeds by:

$$
x_{k+1} = x_k + \alpha_k p_k
$$

where $\alpha_k$ is chosen via exact line search:

$$
\alpha_k = \frac{-\nabla \varphi_k^T p_k}{p_k^T A p_k}
$$

Since $\varphi$ is quadratic:

$$
p_{k+1} = -(Ax_{k+1} - b) + \beta_{k+1} p_k
$$

with the special choice of:

$$
\beta_{k+1} = \frac{r_{k+1}^T A p_k}{p_k^T A p_k}
$$

This choice forces $p_{k+1}$ to be $\Lambda$-conjugate with respect to $\{p_0, p_1, \ldots, p_k\}$.

## CG Properties

Assume the iterates $x_k$ are generated with CG and $x_k \neq x^*$. Then the following are true:

1. $p_l^T A p_z = 0$ for all $z = 0, 1, 2, \ldots, k-1$ (Search directions are A-orthogonal).
2. $r_k^T p_z = 0$ for $z = 0, 1, \ldots, k-1$.
3. $r_k^T r_l = 0$ for all $l = 0, 1, 2, \ldots, k-1$.
4. $x_k$ minimizes $\varphi(x)$ over $x_0 + \mathcal{K}(r_0, k)$ with Krylov subspace $\mathcal{K}(r_0, k) = \text{span}\{r_0, Ar_0, \ldots, A^{k-1} r_0\}$.
5. $\text{span}\{r_0, r_1, \ldots, r_k\} = \mathcal{K}(r_0, k)$.
6. $\text{span}\{p_0, p_1, \ldots, p_k\} = \mathcal{K}(r_0, k)$.

---

## CG Convergence

Let $A \succeq 0$ with eigenvalues $\lambda_1 \leq \lambda_2 \leq \ldots \leq \lambda_n$. Define $\| \cdot \|_A$ such that $\| z \|_A^2 = z^T A z$.

Two main results about CG convergence:

1. $$ \| x_{k+1} - x^* \|_A^2 \leq \left( \frac{\lambda_n - \lambda_1}{\lambda_n + \lambda_1} \right)^2 \| x_0 - x^* \|_A^2 $$
2. If $A$ has $n$ distinct eigenvalues, CG converges in $n$ iterations.

## Preconditioned (Linear) Conjugate Gradient

### Modifying the Problem Setup

- Suppose we have a square and nonsingular matrix $C$. Notice that $Ax = b$ has the same solution as:
$$
C^{-T}Ax = C^{-T}b
$$

- Which has the same solution as:
$$
C^{-T}AC^{-1}Cx = C^{-T}b
$$

- Utilizing $\hat{x} = Cx$, we can consider instead the system:
$$
C^{-T}AC^{-1}\hat{x} = C^{-T}b
$$

- Noticing that $C^{-T}AC^{-1}$ is symmetric and positive definite, we can use CG to solve:
$$
C^{-T}AC^{-1}\hat{x} = C^{-T}b
$$

- To minimize:
$$
\min_{\hat{x} \in \mathbb{R}^n} \varphi(\hat{x}) = \frac{1}{2} \hat{x}^T (C^{-T}AC^{-1}) \hat{x} - (C^{-T}b)^T \hat{x}
$$
