
- **1st criterion of favorable step size** (Armijo condition - sufficient decrease):

$$f(x_k + \alpha p_k) \leq f(x_k) + \alpha c_1 \nabla f(x_k)^T p_k \quad \text{for some} \quad c_1 \in (0, 1)$$

- Essentially, the new step $f(x_k + \alpha p_k)$ should be below the line of $\Phi(\alpha)$.

- **Condition 2 (curvature condition):**

$$\nabla f(x_k + \alpha p_k)^T p_k \geq c_2 \nabla f(x_k)^T p_k \quad \text{for some} \quad c_2 \in (c_1, 1), \quad c_2 \sim 0.1 \rightarrow 0.9$$

- This condition helps in avoiding small step sizes.


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

