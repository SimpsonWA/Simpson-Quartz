### Quadratic Programming

**QP of the form:**
$$
\min_x \frac{1}{2} x^T G x + c^T x \quad \text{s.t.} \quad Ax - b \geq 0
$$

- $G : \mathbb{R}^{n \times n}$ and symmetric  
- $c : \mathbb{R}^n$  
- $b : \mathbb{R}^m$  
- $A : \mathbb{R}^{m \times n}$  

It is also possible for QPs to have equality constraints.

#### Optimality Conditions of QP

The Lagrangian of a QP with inequality constraints:

$$
\mathcal{L}(x, \lambda) = \frac{1}{2} x^T G x + c^T x - \lambda^T (Ax - b)
$$

So the KKT conditions are:

$$
\nabla_x \mathcal{L}(x^*, \lambda^*) = G x^* + c - A^T \lambda^* = 0 \quad \text{(2)}
$$

$$
Ax^* - b \geq 0 \quad \text{(3)}
$$

$$
(Ax^* - b)^T \lambda^* = 0 \quad \text{(4)}
$$

$$
\lambda^* \geq 0 \quad \text{(5)}
$$
### Convex QPs

A convex QP is one where the matrix $Q$ is positive semidefinite. (If $Q$ is strictly positive definite then the QP is strictly convex)

For a convex QP, the KKT conditions are necessary and sufficient for $x^*$ to be a global minimizer.

### Methods for solving QP:

3 main options:

1. Active set methods: guess at active set $\mathcal{I}(x^*) = \{i \in \{1, \ldots, m\} | (a_i^T x^* = b_i)\}$ solve problems with active constraints treated as equality constraints. Check that feasible active set is needed.
2. Projected gradient method: similar to GD, but heading (projecting) the gradient direction to remain in the active set.
3. Interior point methods.

### Interior point methods for QPs:

We start by modifying the KKT conditions.

### KKT with slack variable $y \in \mathbb{R}^n$:

$$
Gx + c - A^T \lambda = 0 \quad (1)
$$

$$
Ax - b - y = 0 \quad (2)
$$

$$
y_i \lambda_i = 0, \quad i = 1, 2, \ldots, m \quad (3)
$$

$$
y, \lambda \geq 0 \quad (4)
$$

---

### Perturbed KKT conditions

For $\tau > 0$ the perturbed KKT conditions again define a central path we follow using a ...

---

### Newton step

Let $x^k \in \mathbb{R}^n$, $y^k > 0$ and $\lambda^k > 0$. A Newton step for the perturbed KKT conditions (6) satisfy:

---

## Primal-Dual System in Optimization

### System of Equations:

$$
\begin{pmatrix}
G_k & 0 & -A^T \\
A & -I & 0 \\
\Theta & \Lambda^k & \gamma_k
\end{pmatrix}
\begin{pmatrix}
\Delta x \\
\Delta y \\
\Delta \lambda
\end{pmatrix}
=
-\begin{pmatrix}
G_k x^k - A^T \lambda^k + c \\
A x^k - y^k - b \\
\gamma_k (\Theta e - \delta_k \mu_k e)
\end{pmatrix}
\tag{7}
$$

### Definitions:

When $\mu_k = \frac{1}{n} (y^k)^T \lambda^k$ (duality measure)

$\delta_k \in [0, 1]$ (control of aggression)

Solving equation (7), we update variables at each iteration as follows:

---

### Solving the Primal-Dual System:

At each iteration, we solve:

$$
\begin{pmatrix}
A & 0 & -A^T \\
A & -I & 0 \\
0 & \Lambda & \gamma
\end{pmatrix}
\begin{pmatrix}
\Delta x \\
\Delta y \\
\Delta \lambda
\end{pmatrix}
=
-\begin{pmatrix}
-r_c \\
-r_p \\
-\gamma r_e + \sigma \mu e
\end{pmatrix}
$$

---

### Methods:

(Your continuation from the notes would go here...)

