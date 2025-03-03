
If $f \in C^1$ (continuously differentiable) and consider a point $x \in \mathbb{R}^n$. A vector $p \in \mathbb{R}^n$ is called a **descent direction** of $f$ at $x$ if:   

$$
p^T \nabla f(x) < 0
$$
This condition ensures that moving in the direction $p$ decreases the value of $f$ locally.


A vector $p_k \in \mathbb{R}^n$ is a descent direction of $f \in C^1$ at $x_k \in \mathbb{R}^n$ if:

$$ p_k^T \nabla f(x_k) < 0 $$

# Types of Descent Directions

1. [[Gradient Descent]]:  $p_k = -\nabla f(x_k)$
2. [[Newtons Method]]:  $p_k = -B_k \nabla f(x_k)$ where $B_k = \nabla^2 f(x)$
3. [[Quasi Newton Method]]:  $p_k = -B_k^{-1} \nabla f(x_k)$ where $B_k \approx \nabla^2 f(x)$
4. **Generally:** $p_k = -B_k^{-1} \nabla f(x_k)$ where $B_k$ is symmetric and positive definite.

- If $B_k$ is not symmetric and positive definite, $B_k^{-1} \nabla f(x_k)$ may not be a descent direction.