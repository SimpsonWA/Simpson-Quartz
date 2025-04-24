- Constrained optimization problems have the form:
$$\min_{x \in \Omega} f(x)$$
- Where $\Omega \subseteq \mathbb{R}^n$ is a convex subset of $\mathbb{R}^n$

## Convex Sets

- Definition of convex sets:
  - A set $\Omega \subseteq \mathbb{R}^n$ is convex if for any $x, y \in \Omega$ and $\lambda \in [0,1]$, the point $\lambda x + (1-\lambda) y \in \Omega$

*Slide 4:* The right example is non-convex since there is some linear boundary. However, open sets could be convex as there is no boundary.

## Properties of Convex Sets

- Add all of the properties we just covered here.

### Examples of Convex Sets:

- **Hyperplane**: $\{x : a^T x = b\}$ with $a \neq 0 \in \mathbb{R}^n$ and $b \in \mathbb{R}$
- **Halfspace**: $\{x : a^T x \leq b\}$ with $a \neq 0 \in \mathbb{R}^n$ and $b \in \mathbb{R}$
- **Norm ball**: $\{x : \|x - x_0\| \leq r\}$ $r$ any valid norm
- **Polyhedron**: $\{x : Ax \leq b, cx = 0\}$
- **Nonnegative orthant**: $\mathbb{R}^n_+ = \{x : x \geq 0\}$
- **Positive semidefinite cone**: $S^n_+ = \{X : X \text{ symmetric}, X \succeq 0\}$

### Closed Set

**Closed Set**:

- A set $S \subseteq \mathbb{R}$ is closed if it contains all of its limit points.

Essentially, a closed set contains its own boundary.

### Stationary and Optimality

**Optimality**:

- For $f \in C^1$ consider the constrained optimization problem:

$$
\min_{x \in S} f(x) \quad (1)
$$

- Where $S$ is closed and convex feasible set

**Def 3**:

- $x^* \in S$ is a local minimizer of (1) if there exists a neighborhood $U(x^*)$ containing $x^*$ such that for all $y \in U(x^*) \cap S$, $f(x^*) \leq f(y)$

- $x^* \in \Omega$ is a global minimizer of (1) if for all $y \in \Omega$, $f(x^*) \leq f(y)$

- In the above conditions, if $f(x^*) < f(y)$ for all $y \neq x^*$, then the solution is strict.

### Stationary

Stationary points of constrained problems:

Let $f \in C^1$ and $\Omega \subset \mathbb{R}^n$ be closed and convex, and consider the constrained optimization problem (1). Then $x^* \in \Omega$ is a stationary point of (1) if:

$$
\nabla f(x^*)^T (x - x^*) \geq 0 \quad \forall x \in \Omega
$$

- Which is to say that there can be no feasible descent directions of $f$ at $x^*$.

- So really, it's to say that at the minimizer point $x^*$, the gradient $\nabla f(x^*)$ and all vectors created by $(x - x^*)$ form angles that are less than or equal to $90^\circ$.

## Interpreting and Using Stationary Conditions

For different convex feasible sets $\Omega$, the stationary condition (2) takes different forms:

- **Unconstrained**: When $\Omega = \mathbb{R}^n$, stationary requires that $\nabla f(x^*) = 0$.
- **Non-negative orthant**: When $\Omega = \mathbb{R}^n_+$, stationary requires that:
  $$
  \frac{\partial f}{\partial x_i}(x^*) = 
  \begin{cases} 
  0, & x_i^* > 0 \\
  \geq 0, & x_i^* = 0 
  \end{cases}
  $$
- **Unit ball**: When $\Omega = \{ x \in \mathbb{R}^n : \| x \|_1 \leq 1 \}$ (using the $\| \cdot \|_1$ norm), stationary requires that $\nabla f(x^*) = 0$ or $\| x^* \|_1 = 1$ and there exists $\lambda \geq 0$ such that $\nabla f(x^*) = \lambda x^*$.

### Connecting Stationarity to Optimality

**Theorem 8: Stationarity as a Necessary Optimality Condition**

- If $x^* \in \Omega$ is a local minimum of (1), then $x^*$ must be a stationary point of (1).
- Recall that a function $f: \mathbb{R}^n \rightarrow \mathbb{R}$ is said to be convex if for any $x, y \in \Omega$:
  $$
  f(\alpha x + (1 - \alpha) y) \leq \alpha f(x) + (1 - \alpha) f(y) \quad \text{for all } \alpha \in [0, 1].
  $$
## Theorem 6: Stationarity as a Sufficient Optimality Condition

Suppose the objective function in problem (1) is convex. Then $x^* \in \Omega$ is a global minimum of (1) if and only if $x^*$ is a stationary point of (1).

## Orthogonal Projections onto Convex Sets

### First Projection Theorem

**Theorem 7:**  
Let $\Omega \subseteq \mathbb{R}^n$ be a nonempty closed convex set. Then the orthogonal projection operator $P_{\Omega}: \mathbb{R}^n \rightarrow \Omega$ is defined by:

$$
P_{\Omega}(x) = \arg \min_{y \in \Omega} \|x - y\|^2
$$

This is well-defined, meaning that for any $x \in \mathbb{R}^n$, the minimization problem (3) has a unique optimal solution.

### Examples

- **Non-negative Orthant**:  
  When $\Omega = \mathbb{R}_+^n$, to compute $z = P_{\Omega}(x)$, we take:

  $$
  z_i = 
  \begin{cases} 
  x_i, & x_i \geq 0 \\
  0, & x_i < 0 
  \end{cases}
  $$

- **Box**:  
  When $\Omega = \{x \in \mathbb{R}^n : a \leq x \leq b\}$, to compute $z = P_{\Omega}(x)$, we take:

  $$
  z_i = 
  \begin{cases} 
  a_i, & x_i \leq a_i \\
  x_i, & a_i \leq x_i \leq b_i \\
  b_i, & x_i \geq b_i 
  \end{cases}
  $$
  ## Box Projection

- For $\Omega = \{ x \in \mathbb{R}^n : \| x \|_{l_2} \leq r \}$ (using the $l_2$ norm), to compute $z = P_{\Omega}(x)$ we use:
$$
z =
\begin{cases} 
x, & \| x \|_{l_2} \leq r \\
\frac{r x}{\| x \|_{l_2}}, & \| x \|_{l_2} > r 
\end{cases}
$$

## Second Projection Theorem

**Theorem 8:**  
Let $\Omega$ be a closed convex set and consider any $x \in \mathbb{R}^n$. Then $z = P_{\Omega}(x)$ if and only if $z \in \Omega$ and:
$$
(x - z)^T (y - z) \leq 0 \quad \text{for all} \quad y \in \Omega
$$

## Connecting Stationarity to Projections

**Theorem 9:**  
Let $f \in C^1$ and $\Omega \subset \mathbb{R}^n$ be a nonempty closed convex set. Then $x^*$ is a stationary point of problem (1) if and only if there exists $\alpha > 0$ such that:
$$
x^* = P_{\Omega}(x^* - \alpha \nabla f(x^*)) \quad \text{"fixed point"}
$$

## Projected Gradient Descent

Using:
$$
x^* = P_{\Omega}(x^* - \alpha \nabla f(x^*))
$$

We can apply the following projected gradient descent (PGD) algorithm:
$$
x_{k+1} = P_{\Omega}(x_k - \alpha_k \nabla f(x_k))
$$

