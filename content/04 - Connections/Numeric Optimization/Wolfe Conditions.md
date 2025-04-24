When using iterative optimization methods like [[Gradient Descent]] or [[Quasi Newton Method]], choosing an appropriate step size $\alpha$ is crucial. Line search methods aim to find a step size that balances progress with stability.

Two commonly used criteria are the **Armijo (sufficient decrease)** condition and the **Curvature** condition. Together, they form the **Wolfe Conditions**, which help ensure convergence without overshooting or stagnating.

---
# Armijo Condition (Sufficient Decrease) :

The **Armijo condition** ensures that the function decreases sufficiently along the search direction $p_k:$

$$f(x_k + \alpha p_k) \leq f(x_k) + \alpha c_1 \nabla f(x_k)^T p_k \quad \text{for some} \quad c_1 \in (0, 1)$$

- Geometrically, this means the value $f(x_k + \alpha p_k)$ should lie below the linear approximation (or "Armijo line") of $f$ at $x_k$.

![[SufficentDecrease.png]]

---
## Armijo Backtracking Algorithm: 

```pseudo
	\begin{algorithm}
	\caption{Backtracking Algorithm}
	\begin{algorithmic}
	  \Procedure{Backtracking}{$A, p, r$}
	    \State Choose $\bar{\alpha} > 0$, $\rho \in (0,1)$, $c_1 \in (0,1)$
	    \State Set $\alpha \leftarrow \bar{\alpha}$
	    \While{$f(x_k + \alpha p_k) > f(x_k) + \alpha c_1 \nabla f(x_k)^T p_k$}
	      \State $\alpha \leftarrow \rho \alpha$
	    \EndWhile
	    \Return $\alpha_k = \alpha$
	  \EndProcedure
	\end{algorithmic}
	\end{algorithm}

```

---

# Curvature Condition:

The **curvature condition** ensures that the step size is not too small and that the slope has been sufficiently reduced:

$$\nabla f(x_k + \alpha p_k)^T p_k \geq c_2 \nabla f(x_k)^T p_k \quad \text{for some} \quad c_2 \in (c_1, 1), \quad c_2 \sim 0.1 \rightarrow 0.9$$

---

# Wolfe Conditions 

A step size $\alpha_k > 0$ satisfies the **Wolfe conditions** if:
**1. Armijo Condition**: 
$$
f(x_k + \alpha_k p_k) \leq f(x_k) + \alpha_k c_1 \nabla f(x_k)^T p_k \tag{1}
$$

and
**2. Curvature Condition**
$$
\nabla f(x_k + \alpha_k p_k)^T p_k \geq c_2 \nabla f(x_k)^T p_k \tag{2}
$$

- with $0 < c_1 < c_2 < 1$.
![[Curvature Condition.png]]

# Strong Wolfe conditions:

The **strong Wolfe conditions** replace the curvature condition with a stronger version:
$$
|\nabla f(x_k + \alpha_k p_k)^T p_k| \leq c_2 |\nabla f(x_k)^T p_k| \tag{3}
$$

This prevents the directional derivative $\Phi'(\alpha_k)$ from being too large in magnitude (either too positive or too negative), which helps maintain stability.

