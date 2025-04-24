**BFGS** is a type of [[Quasi-Newton Method]], and can be seen as a refined variant of the [[DFP]] (Davidon, Fletcher, Powell) algorithm. It is named after its developers: Broyden, Fletcher, Goldfarb, and Shanno.


# Formulation 

**Idea**: The BFGS algorithm determines the [[Descent Direction]] by preconditioning the gradient using curvature information. It incrementally improves an approximation of the Hessian matrix of the loss function, using gradient evaluations guided by a generalized secant condition.


So from the [[Secant Method]] we impose the **secant condition** on the Hessian approximation $B_{k+1}$ as:
$$
B_{k+1}s_k = y_k
$$
We can note that $H_{k+1} = B_{k+1}^{-1}$, and can write:
$$
H_{k+1}y_k = s_k
$$

The BFGS method is then based on the following optimization problem to obtain $H_{k+1}$
$$
\min_H \|H - H_k\| \quad s.t \ \ H = H^T, \ \ Hy_k = s_k
$$
The solution to this optimization problem provides the BFGS update for the inverse Hessian approximation: 
$$
H_{k+1} = (I - \rho_k s_k y_k^T) H_k (I - \rho_k y_k s_k^T) + \rho_k s_k s_k^T
$$

Where : $\rho_k = (y_k^T s_k)^{-1}$

# Pseudocode

[[Wolfe Conditions]]
```pseudo 
\begin{algorithm}
\caption{BFGS Optimization Algorithm}
\begin{algorithmic}
\REQUIRE Initial point $x_0$, function $f$, gradient $\nabla f$, tolerance $\varepsilon$, initial inverse Hessian approximation $H_0$
\STATE $k \gets 0$
\WHILE{$\|\nabla f(x_k)\| > \varepsilon$}
    \STATE Compute search direction: $p_k \gets -H_k \nabla f(x_k)$
    \STATE Compute step size $\alpha_k$ satisfying Wolfe conditions
    \STATE Update iterate: $x_{k+1} \gets x_k + \alpha_k p_k$
    \STATE Compute $s_k \gets x_{k+1} - x_k$,  $y_k \gets \nabla f(x_{k+1}) - \nabla f(x_k)$
    \STATE Compute $\rho_k \gets \frac{1}{s_k^\top y_k}$
    \STATE Update inverse Hessian approximation:
    $
    H_{k+1} \gets (I - \rho_k s_k y_k^\top) H_k (I - \rho_k y_k s_k^\top) + \rho_k s_k s_k^\top
    $
    \STATE $k \gets k + 1$
\ENDWHILE
\end{algorithmic}
\end{algorithm}

```


