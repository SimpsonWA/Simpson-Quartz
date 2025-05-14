
**Idea**: Given that during [[BFGS]] $H_k$ is dense and requires $O(n^2)$ storage what we want to do is store a modified version of this hessian that is implicitly based on a certain number of vector pairs to reduce the memory usage. 

---


Recall the BFGS update for the inverse Hessian $H_{k+1}$:
$$H_{k+1} = V_k^T H_k V_k + \rho_k s_k s_k^T$$
where
$$s_k = x_{k+1} - x_k, \quad y_k = \nabla f(x_{k+1}) - \nabla f(x_k) \quad \text{and} \quad V_k = I - \rho_k y_k s_k^T$$
with
$$\rho_k = \frac{1}{y_k^T s_k}$$
- In general $H_k$ is dense and requires $O(n^2)$ storage.

- Though we can store a modified version of the $H_k$ implicitly based on a certain number of (say $m$) most recent $(s_j, y_j)$ vector pairs.

Given an inital inverse Hessian approximation at the kth iteration, $H_K^0$ observe that: 
$$
\begin{aligned}
H_k &= (V_{k-1}^T \cdots V_{k-m}^T) H_k^0 (V_{k-m} \cdots V_{k-1}) \\
&\quad + \rho_{k-m}(V_{k-1}^T \cdots V_{k-m+1}^T)s_{k-m}s_{k-m}^T(V_{k-m+1} \cdots V_{k-1}) \\
&\quad + \rho_{k-m+1}(V_{k-1}^T \cdots V_{k-m+2}^T)s_{k-m+1}s_{k-m+1}^T(V_{k-m+2} \cdots V_{k-1}) \\
&\quad \vdots \\
&\quad + \rho_{k-2}V_{k-1}^T s_{k-2}s_{k-2}^T V_{k-1} \\
&\quad + \rho_{k-1} s_{k-1} s_{k-1}^T
\end{aligned}
$$

Really the core idea is to use recursion to compute the right half and the left half of $H_k q$ for some $q$recursively 

*Add Pseudocode*


