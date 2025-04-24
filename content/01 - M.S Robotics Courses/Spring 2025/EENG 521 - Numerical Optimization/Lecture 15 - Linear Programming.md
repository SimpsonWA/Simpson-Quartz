

- Linear programs (LP) are convex optimization problems involving linear objective functions and linear constraint functions.

## Standard Form of LPs

$$
\begin{aligned}
&\min_{x \in \mathbb{R}^n} \quad c^T x \quad (1)\\
&\text{s.t.} \quad Ax = b, \quad x \geq 0 
\end{aligned}
$$

Where:
- $A \in \mathbb{R}^{m \times n}$
- $b \in \mathbb{R}^m$
- $c \in \mathbb{R}^n$

We assume $m \leq n$ and $\text{rank}(A) = m$.

The feasible set $\Omega = \{x : Ax = b, x \geq 0\}$ for an LP is always a convex polytope in $\mathbb{R}^n$.

## Optimality and Duality

The Lagrangian of (1) is:

$$
\mathcal{L}(x, \lambda, s) = c^T x - \lambda^T (Ax - b) - s^T x
$$

Where:
- $\lambda$ is the Lagrange multiplier vector for the equality constraint.
- $s$ is the Lagrange multiplier vector for the inequality constraint.

The **necessary KKT conditions** are given by:

$$
A^T \lambda + s = c, \tag{3}
$$
$$
Ax = b,
$$
$$
x, s \geq 0,
$$
$$
x_i s_i = 0 \text{ for all } i
$$

Suppose $(x^*, \lambda^*, s^*)$ satisfies the first-order KKT conditions. Then for an LP, this is sufficient to say $x^*$ is a global minimizer of (1).

## Duality

The dual problem of (1) is given as:

$$
\max_{\lambda, s} q(\lambda, s) \text{ s.t. } s \geq 0
$$

where the dual objective function is given by:

$$
q(\lambda, s) = \inf_x \mathcal{L}(x, \lambda, s) = \inf_x c^T x - \lambda^T (Ax - b) - s^T x
$$

$$
\inf_x (c^T - \lambda^T A - s^T) x + b^T \lambda
$$

When $c^T - \lambda^T A - s^T \neq 0$, $q(\lambda, s) = -\infty$, so the dual problem simplifies to:

$$
\max_{\lambda, s} b^T \lambda \text{ s.t. } A^T \lambda + s = c \text{ and } s \geq 0
$$

We can rewrite the problem equivalently as:

$$
\max_{\lambda} b^T \lambda \text{ s.t. } A^T \lambda \subseteq C \tag{8}
$$

From (7), we see that $s \subseteq s$, essentially acting as the slack variable from our example.

Closely related to the dual problem (8) is the minimization problem:

$$
\min_{\lambda} -b^T \lambda \text{ s.t. } C - A^T \lambda \geq 0 \tag{9}
$$

## The Lagrangian

The Lagrangian of (9) is:

$$
\mathcal{L} (x, \lambda) = b^T \lambda - x^T (C - A^T \lambda) \tag{10}
$$

where $x$ is the Lagrange multiplier vector of the dual problem.

## Necessary KKT Conditions

The first-order KKT conditions for (9) are:

$$
Ax = b, A^T \lambda \subseteq C, x \geq 0, x_i (C - A^T \lambda)_i = 0 \text{ for all } i
$$

With the substitution $s = C - A^T \lambda$, these optimality conditions are identical to those in (8) for the primal function.

(Slide 12 is primal-dual symmetry)

## Simplex Method
