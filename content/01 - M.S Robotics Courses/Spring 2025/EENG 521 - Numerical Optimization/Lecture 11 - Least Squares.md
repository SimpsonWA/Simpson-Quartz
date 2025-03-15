
## Least Square Problems

- **least squares form:**
  $$
  f(x) = \frac{1}{2} \sum_{j=1}^{m} (r_j(x))^2 = \frac{1}{2} \|r(x)\|_2^2
  $$

- **Where each residual function** $r_j : \mathbb{R}^n \rightarrow \mathbb{R}$ **is smooth**

- **A typical setup of this problem is** $x$ **as a parameter and** $r_j$ **as the discrepancy between the model and the** $j^{th}$ **observed data point.**

- **Define the residual vector:** $r : \mathbb{R}^n \rightarrow \mathbb{R}^m$ **as**
  $$
  r(x) = [r_1(x), r_2(x), ..., r_m(x)]^T
  $$

- **Then:**
  $$
  f(x) = \frac{1}{2} \sum_{j=1}^{m} (r_j(x))^2 = \frac{1}{2} \|r(x)\|_2^2
  $$

- **Writing** $f(x) = h(r(x))$ **we can use the chain rule to get the gradient:**
  $$
  \nabla f(x) = \nabla r(x)^T \nabla h(r(x)) = \nabla r(x)^T r(x) = J(x)^T r(x),
  $$

- **where:**
  $$
  J(x) = \begin{bmatrix}
  \nabla r_1(x)^T \
  \nabla r_2(x)^T \
  \vdots \
  \nabla r_m(x)^T
  \end{bmatrix} \in \mathbb{R}^{m \times n}
  $$

- **This is the Jacobian of the residuals.**

So the gradient of the least squares function is:
$$
\nabla f(x) = \sum_{j=1}^{M} \nabla v_j(x) \nabla v_j(x) = J(x)^T r(x)
$$

And the Hessian of the least squares function is:
$$
\nabla^2 f(x) = \sum_{j=1}^{M} \nabla v_j(x) \nabla v_j(x)^T + \sum_{j=1}^{M} v_j(x) \nabla^2 v_j(x)
$$
$$
= J(x)^T J(x) + \sum_{j=1}^{M} v_j(x) \nabla^2 v_j(x)
$$

## Linear Least Squares

### Linear least squares problem

Linear least squares have the residual vectors of the form:
$$
r(x) = Jx - y
$$
where $J$ is a matrix of $m \times n$ and $y$ is a vector of size $m \times 1$.

The objective function is then:
$$
f(x) = \frac{1}{2} \| Jx - y \|^2
$$

- $J$: measurement matrix
- $y$: data vector

Since the Jacobian of the residual $r(x)$ is $J(x) = J$ and since $\nabla^2 r_j(x) = 0$ for all $j$ we simply have:

$$
\nabla f(x) = J^T r(x) = J^T (Jx - y)
$$

$$
\nabla^2 f(x) = J^T J
$$

The Hessian $\nabla^2 f(x)$ is positive definite for all $x$. This means the function is convex.

Since $f(x)$ is convex any stationary point of $f(x)$ is a global minimizer of $f$. So from the condition $\nabla f(x^*) = 0$ we obtain the normal equations:

$$
J^T J x = J^T y
$$

## Non-linear Least Squares: Gauss-Newton

### Non-linear least squares problem

Recall for a general form of least square problems:

$$
\min_x \frac{1}{2} \| r(x) \|_2^2
$$

For a smooth residual $r: \mathbb{R}^n \rightarrow \mathbb{R}^m$ (We no longer assume that $r(x) = Jx - y$)

As shown before the gradient and Hessian are:

$$
\nabla f(x) = J(x)^T r(x)
$$

$$
\nabla^2 f(x) = J(x)^T J(x) + \sum_{j=1}^m r_j(x) \nabla^2 r_j(x)
$$

## Gauss-Newton for Nonlinear Least Squares

Recall Newton's method with iterations given by:

$$
x_{k+1} = x_k + \alpha p_k
$$

where $p_k$ is obtained by solving the linear system of equations:

$$
\nabla^2 f(x_k) p_k = -\nabla f(x_k)
$$

The Gauss-Newton method uses a simple modification of Newton's method where:

$$
J(x_k)^T J(x_k) p_k = -J(x_k)^T r(x_k)
$$

So the resulting direction $p_k$ will be a descent direction if $J(x)$ is full rank and if $\nabla f(x_k) \neq 0$.

### Slide 14

Recall that:

$$
\nabla^2 f(x_k) = J(x)^T J(x) + \sum_{j=1}^m r_j(x) \nabla^2 r_j(x)
$$

The approximation of $\nabla^2 f(x)$ by $J(x)^T J(x)$ may be quite accurate when we are near $x^*$ so that the residuals $r(x)$ are small, or the residuals $r(x)$ are nearly affine as then the $\nabla^2$ Hessians are small.

From another perspective, write the 1st order Taylor series expansion of $V(x)$ at $x_n$ gives:

$$
f(x_{n+1}) \approx V(x_n) + J(x_n)p
$$

The Gauss-Newton step direction $p_n$ is actually the solution to the least squares problem involving the linearized residual:

$$
\min_p \frac{1}{2} \|J(x_n)p + V(x_n)\|^2 \Longleftrightarrow J(x_n)^T J(x_n)p = -J(x_n)^T V(x_n)
$$

Aside is Theorem 1


