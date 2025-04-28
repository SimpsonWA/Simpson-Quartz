**Idea**:  Quasi-Newton methods are a type of [[Line Search Method]] designed for optimization problems. They are first order methods, meaning they rely only on [[Gradient]] information, not direct second derivatives ([[Hessian]]s) like Newton's Method. The goal is to achieve superlinear convergence, similar to [[Newtons Method]], without needing to compute or invert the Hessian matrix, which is expensive in high dimensions.

---
# Newtons Method

In Newton’s Method for optimization, we update the iterate using the true Hessian and true gradient:
$$
x_{k+1} = x_k - (\nabla^2 f(x_k))^{-1} \nabla f(x_k)
$$
Where: 
- $\nabla f(x_k) \in \mathbb{R}^n$ : Gradient
-  $\nabla^2 f(x_k) \in \mathbb{R}^{n \times n}$ : Hessian

Where the n-dimensional Newtons method above is a generalization of the univarite (n=1) Newton's method for finding zeros of $f'(x)$:
$$
x_{k+1} = x_k - \frac{f'(x)}{f''(x)}
$$
---
# Secant Method for n=1

Like Newton's method (univariate method) $(n = 1)$, Secant method is a root finding algorithm that can be used for finding zeros of $f'(x)$:
$$
x_{n+1} = x_n - \frac{f'(x_n)(x_n - x_{n-1})}{f'(x_n) - f'(x_{n-1})}
$$
So the intuition behind this is that instead of evaluating the exact slope (second derivative) the secant method is instead using the slope between two recent points to estimate the curvature. 

We can interpret the Secant method as:

$$
x_{n+1} = x_n - \frac{f'(x_n)}{\frac{f'(x_n) - f'(x_{n-1})}{x_n - x_{n-1}}}
$$

The denominator is an approximation of $f''(x_k)$ (but is formed only using first order info). This is Newton-like, but the Secant method is called Quasi-Newton method.

---
# Generalizing Secant method for $n > 1$

Quasi-Newton methods involve iterations of the form:

$$
x_{n+1} = x_n - \alpha (B_k)^{-1} \nabla f(x_k)
$$
Where $B_k$ is some approximation of the Hessian $\nabla^2 f(x_k)$ that is constructed using 1st order information.

### Challenges for $n > 1$:

Extending the secant method to $n>1$ is not trivial. The reason being is that the Hessian is an $n \times n$ matrix, while each gradient $\nabla f(x_k), \nabla f(x_{k-1})$ are  $n \times 1$ vectors. So changes in the gradient only give limited information about the hessian 

So to get around this we use a special equation called the secant equation which captures teh relationship between hessian and changes in the the gradients from one step to the next. 

---

# Secant Equation

Taking the 1st order Taylor expansion of $\nabla f(x)$ at $x_k$ and considering the expansion at $x_{k-1}$:

$$\nabla f(x_{k-1}) \equiv \nabla f(x_k) + \nabla^2 f(k_n) (x_{k-1} - x_k)$$

Defining vectors:
- $s_{k-1} = x_k - x_{k-1}$  
- $y_{k-1} = \nabla f(x_k) - \nabla f(x_{k-1})$

We have an approximation that the true Hessian satisfies: $\nabla^2 f(x_k) s_{k-1} \approx y_{k-1}$. This leads to the secant equation, which we can require an approximation $B_k$ to satisfy:

$$B_k s_{k-1} = y_{k-1}$$
- $B_k \in \mathbb{R}^{n \times n}$
- $s_{k-1} \in \mathbb{R}^{n}$
- $y_{k-1} \in \mathbb{R}^{n}$

### Optimization Problem

For clearer notation, we will rewrite the secant equation as:

$$B_{k+1} s_k = y_k $$
Where: 

$$ s_k = x_{k+1} - x_k \quad \text{and} \quad y_k = \nabla f(x_{k+1}) - \nabla f(x_k) $$

To reduce the remaining degrees of freedom and determine $B_{k+1}$ uniquely, it is common to solve the problem: (to find $B_{k+1}$)

$$ \min_B \| B - B_k \| \quad (1) $$

subject to: $B = B^T$, $B s_k = y_k$

$(1)$ solves the closest symmetric matrix to $B_k$ that satisfies the secant method. Different norms give different quasi-Newton methods.

---

# DFP Update:

- [[DFP]]

# BFGS: 

- [[BFGS]]