# Definitions:

 **Differentiability**: A function is differentiable at a point if there is a linear approximation that accurately represents the function's change at that point.

 **Gradient**: The gradient of a function at a point is a vector that points in the direction of the greatest rate of increase of the function.

**Jacobian**: A matrix representing the first-order partial derivatives of a vector-valued function.

 **Hessian**: A square matrix of second-order partial derivatives of a scalar-valued function, which describes the local curvature of the function.

 **Chain Rule**: A rule that calculates the derivative of the composition of two or more functions.

 **Taylor's Theorem**: A theorem that approximates a function near a point using the function's derivatives at that point.

 **Lipschitz Smoothness**: A property of a function where the gradient of the function does not change faster than a certain constant rate, ensuring the function is smooth.

 **Smoothness**: If a function is smooth, it can be approximated by a quadratic function near any point in its domain.

# Notes:

### Differentiability:

- Let $f: \mathbb{R}^n \rightarrow \mathbb{R}$ (scalar-valued)
- $f$ is (Fréchet-) differentiable at a given point $x \in \mathbb{R}^n$ if there exists a vector $g \in \mathbb{R}^n$ with:
$$\lim_{y \to 0} \frac{f(x+y) - f(x) - g^T y}{||y||} = 0$$

### Gradient:
- If $f$ is differentiable at $x$, we call the corresponding $g$ vector the gradient of $f$ at $x$. It is denoted as $\nabla f(x) \in \mathbb{R}^n$ and given by:
$$\nabla f(x) = \begin{pmatrix} \frac{\partial f}{\partial x_1} \\ \frac{\partial f}{\partial x_2} \\ \vdots \\ \frac{\partial f}{\partial x_n} \end{pmatrix} \in \mathbb{R}^n$$

### Jacobian:
- Now we say $f: \mathbb{R}^n \rightarrow \mathbb{R}^m$ be a vector field. We want to find a matrix $J \in \mathbb{R}^{m \times n}$ such that:
$$\lim_{y \to 0} \frac{||f(x+y) - f(x) - Jy||}{||y||} = 0$$
- We say this matrix $J$ is:
$$\nabla f(x) = J(x)^T = \begin{pmatrix}
\nabla f_1(x) & \nabla f_2(x) & \cdots & \nabla f_m(x) \\
\vdots & \vdots & \ddots & \vdots \\
\end{pmatrix} \in \mathbb{R}^{n \times m}$$
### Hessian

We denote the Hessian of $f: \mathbb{R}^n \rightarrow \mathbb{R}$ at $x$ as:


$$ 
\nabla^2 f(x) = \begin{bmatrix}
\frac{\partial^2 f}{\partial x_1^2} & \frac{\partial^2 f}{\partial x_1 \partial x_2} & \cdots & \frac{\partial^2 f}{\partial x_1 \partial x_n} \\
\frac{\partial^2 f}{\partial x_2 \partial x_1} & \frac{\partial^2 f}{\partial x_2^2} & \cdots & \frac{\partial^2 f}{\partial x_2 \partial x_n} \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial^2 f}{\partial x_n \partial x_1} & \frac{\partial^2 f}{\partial x_n \partial x_2} & \cdots & \frac{\partial^2 f}{\partial x_n^2}
\end{bmatrix}
$$



- If $f$ is twice differentiable, $\nabla^2 f(x)$ is symmetric.
- First-order information of $f$: gradient and Jacobian.
- Second-order info of $f$: Hessian.

### Chain Rule

Given differentiable functions $h: \mathbb{R}^n \rightarrow \mathbb{R}^m$ and $g: \mathbb{R}^m \rightarrow \mathbb{R}$, the gradient of $f(x) = g(h(x)) : \mathbb{R}^n \rightarrow \mathbb{R}$ is given by:



$$ 
\nabla f(x) = \sum_{i=1}^m \frac{\partial g}{\partial z_i} \nabla h_i(x) = \nabla h(x) \nabla g(h(x))
$$

### Taylor's Theorem

- Taylor's theorem shows how smooth functions can be approximated locally by low-order functions.
- **Theorem 1**: Given a continuously differentiable ($C^1$) function $f: \mathbb{R}^n \rightarrow \mathbb{R}$ and $x, p \in \mathbb{R}^n$, we have:

$$\[ 
f(x + p) = f(x) + \nabla f(x + \epsilon p)^T p \quad \text{for some} \quad \epsilon \in (0, 1)
\]
$$

- **Theorem 2**: Given a twice differentiable ($C^2$) function $f: \mathbb{R}^n \to \mathbb{R}$ and $x, p \in \mathbb{R}^n$, we have:
$$
f(x + p) = f(x) + \nabla f(x)^\top p + \frac{1}{2} p^\top \nabla^2 f(x + t p) p
$$
for some $t \in (0, 1)$

- The gradients of these functions:
- $C^1$:
$$
\nabla f(x + p) = f(x) + \int_0^1 \nabla f(x + t p)^\top p \, dt
$$
- $C^2$:
$$
\nabla f(x + p) = \nabla f(x) + \int_0^1 \nabla^2 f(x + t p) p \, dt
$$

### Smoothness:
- An objective function $f: \mathbb{R}^n \to \mathbb{R}$ is uniformly Lipschitz with constant $L$ that:

$$
\| \nabla f(x) - \nabla f(y) \|_2 \leq L \| x - y \|_2
$$

- For all $x, y$ in the domain of $f$, here we say $f$ is $L$-smooth
- If $f$ is $L$-smooth then for any $x, y$ in the domain of $f$ we have:
$$
f(y) \leq f(x) + \nabla f(x)^\top (y - x) + \frac{L}{2} \| y - x \|_2^2
$$
- For a $C^2$ function $f: \mathbb{R}^n \to \mathbb{R}$, $f$ is $L$-smooth if:

$$
\| \nabla^2 f(x) \| \leq L \quad \text{for all } x
$$

- or:

$$
\lambda_{\max} (\nabla^2 f(x)) \leq L \quad \text{for all } x
$$

---
