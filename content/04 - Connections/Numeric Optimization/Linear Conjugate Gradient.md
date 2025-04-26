**Idea**: Given a [[Linear System of Equations]] where $A \in \mathbb{R}^{n \times n}$ is [[Symmetric]] and [[Positive Definite]]. Then we can find a unique solution to the equation using a quadratic optimization problem. This is an iterative algorithm that can be used for these linear system of equations especially when $n$ is large.


# Setup 

Consider a [[Linear System of Equations]]: 
$$ Ax = b \quad (1) $$
Here $A \in \mathbb{R}^{n \times n}$ is [[Symmetric]] and [[Positive Definite]]

The unique solution to $(1)$ is given by the quadratic optimization problem: 
$$ \min_{x \in \mathbb{R}^n} \varphi(x) = \frac{1}{2} x^T A x - b^T x \quad (2) $$
### Useful Fact:

At any point $x \in \mathbb{R}^n$ the residual of the linear system $Ax = b$, that is: 
$$ r(x) := Ax - b $$
is equal to the gradient of the quadratic objective function $\phi$ at $x$ :
$$ \nabla \phi(x) = Ax-b = r(x)$$

# Conjugate Directions 

**Definition**: A collection of nonzero vectors $\{p_0,p_1,\dots,p_l\}$ is said to be conjugate with respect to a symmetric and positive definite matrix $A$ if: 

$$
p_i^T A p_j = 0 \quad \text{for all } i \neq j
$$
Equivalently these vectors are also called **A-conjugate** or **A-orthogonal**

Using a iterative algorithm with exact line search will converge to the exact solution $x^*$ to $(1)$ and $(2)$ in at most $n$ iterations with $n$ A-conjugate directions

# Conjugate Gradient Iterations (Naiive)

Let $x_0 \in \mathbb{R}^n$ be the starting point. Compute the residual $r_0 = Ax_0 - b = \nabla \phi(x_0)$ , and let the first search direction $p_0 = -r_0$. The algorithm proceeds by:

$$
x_{k+1} = x_k + \alpha_k p_k
$$

where $\alpha_k$ is chosen via exact line search:

$$
\alpha_k = \frac{-r_k^T p_k}{p_k^T A p_k}
$$

Since $\varphi$ is quadratic:

$$
p_{k+1} = -(Ax_{k+1} - b) + \beta_{k+1} p_k
$$

with the special choice of:

$$
\beta_{k+1} = \frac{r_{k+1}^T A p_k}{p_k^T A p_k}
$$

This choice forces $p_{k+1}$ to be A-conjugate with respect to $\{p_0, p_1, \ldots, p_k\}$.

## Conjugate Gradient Properties

Assume the iterates $x_k$ are generated with CG and $x_k \neq x^*$. Then the following are true:

1. $p_l^T A p_z = 0$ for all $z = 0, 1, 2, \ldots, k-1$ (Search directions are A-orthogonal).
2. $r_k^T p_z = 0$ for $z = 0, 1, \ldots, k-1$.
3. $r_k^T r_l = 0$ for all $l = 0, 1, 2, \ldots, k-1$. (Residuals are orthgonal)
4. $x_k$ minimizes $\varphi(x)$ over $x_0 + \mathcal{K}(r_0, k)$ with Krylov subspace $\mathcal{K}(r_0, k) = \text{span}\{r_0, Ar_0, \ldots, A^{k-1} r_0\}$.
5. $\text{span}\{r_0, r_1, \ldots, r_k\} = \mathcal{K}(r_0, k)$.
6. $\text{span}\{p_0, p_1, \ldots, p_k\} = \mathcal{K}(r_0, k)$.

Note that Conjugate Gradient iterations can be expressed as:
$$
x_{k+1} = x_k - c_k \nabla \phi(x_k) + d_k (x_k - x_{k-1})
$$
Which is a momentum [[Gradient Descent]] algorithm where we have a tendency to continue in the previous direction $x_k - x_{k-1}$ but with a turn around toward $- \nabla \phi(x_k)$. This method is commonly refered to as a *heavy-ball method*

# Conjugate Gradient Algorithm 
