
**Newtons Method** is a special type of [[Line Search Method]] with a choice of step direction and a step size of:
- $\alpha_k = 1$
- $p_k = -(\nabla^{2} f(x_k))^{-1} \nabla f(x_k)$
 
 If the hessian $\nabla^2 f(x_k)$ is **positive definite** then $p_k$ is guaranteed to be a descent direction of $f$ at $x_k$ and can be chosen as: 

$$
p_k = -(\nabla^{2} f(x_k))^{-1} \nabla f(x_k)
$$


# Newton's Method with Hessian Modification

Away from the solution the Hessian matrix $\nabla^2 f(x)$ may not be positive definite, so the Newton Direction $p_k$ is defined as:

$$
\nabla^2 f(x_k) p_k = - \nabla f(x_k)
$$

**Line Search Newton with Modification**
```pseudo
	\begin{algorithm}
	\caption{Backtracking Algorithm}
	\begin{algorithmic}
	  \Procedure{Newton-Line-Search}{$x_0$}
		\For{$k=0,1,2,\dots$}
		\State Factorize $B_k = \nabla^2 f(x_k) + E_k$ 
		\State Solve $B_k p_k = - \nabla f(x_k)$
		\State set $x_{k+1} \leftarrow x_k + \alpha_k p_k$
        \EndFor
	  \EndProcedure
	\end{algorithmic}
	\end{algorithm}
```
