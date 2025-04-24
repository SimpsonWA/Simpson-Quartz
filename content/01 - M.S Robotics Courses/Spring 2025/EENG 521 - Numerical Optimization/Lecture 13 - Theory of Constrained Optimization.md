## Constrained Optimization Problem Form

### Problem Formulation

Minimize $f(x)$ subject to:
$$
c_E(x) = 0, \, i \in \mathcal{E} \\
c_I(x) \geq 0, \, i \in \mathcal{I}
$$

- $f$: objective function  
- $x = (x_1, x_2, \ldots, x_n) \in \mathbb{R}^n$ (unknowns/parameters)  
- $\mathcal{E} \subseteq \mathbb{N}$: indices of equality constraints  
- $\mathcal{I} \subseteq \mathbb{N}$: indices of inequality constraints  
- $c_i: \mathbb{R}^n \rightarrow \mathbb{R}$: constraint functions  

### Feasible Set

Feasible set given by:
$$
\Omega = \{ x \in \mathbb{R}^n : c_E(x) = 0, \, i \in \mathcal{E}, \, c_I(x) \geq 0, \, i \in \mathcal{I} \}
$$

In general, $\Omega$ is not convex.

### Optimality

Optimality is exactly the same as from lecture 12 (copy from here).

### Example: Single Equality Constraint

Consider circle: $\min x_1 + x_2 = f(x)$ subject to $x_1^2 + x_2^2 - 2 = 0$ ($c_1(x)$).

We say $x^* = (-1, 1)$ is a global minimizer.

At $x^*$, constraint normal $\nabla c_1(x^*) \parallel \nabla f(x^*)$ which means there exists a scalar $\lambda_1^*$ such that:
$$
\nabla f(x^*) = \lambda_1^* \nabla c_1(x^*)
$$

- $\nabla c_1(x) = \begin{bmatrix} 2x_1 \\ 2x_2 \end{bmatrix}$  
  $\nabla f(x) = \begin{bmatrix} 1 \\ 1 \end{bmatrix}$  

- Constraint normals: $\nabla c_1(x)$  

- For this example, $\nabla c_1(x^*) = \begin{bmatrix} -2 \\ -2 \end{bmatrix}$,  
  $\nabla f(x^*) = \begin{bmatrix} 1 \\ 1 \end{bmatrix}$  

So:  
$$
\nabla f(x^*) = \lambda_1^* \nabla c_1(x^*) \Rightarrow \lambda_1^* = -\frac{1}{2}
$$

- Same example: different perspective linearization  

- **Question**: At a feasible point $x$ where $c_1(x) = 0$, can we take a small step $s$ while remaining feasible and decreasing our function value?

- To retain feasibility, we require $c_1(x + s) = 0$:

$$
0 = c_1(x + s) \approx c_1(x) + \nabla c_1(x)^T s = \nabla c_1(x)^T s
$$

- Thus, to retain feasibility and obtain descent, we need a step $s$ such that:  

$$
\nabla c_1(x)^T s = 0 \quad \text{and} \quad \nabla f(x)^T s < 0
$$

- So if we cannot find a step/direction $s$, then we may be at a local minimum. The only way for $s$ not to exist is if $\nabla f(x)$ and $\nabla c_1(x)$ are parallel.
## Another Perspective: Lagrangian

Combining the objective function and the constraint function, let's introduce a Lagrangian function:

$$
L(x, \lambda_1) = f(x) - \lambda_1 C_1(x)
$$

Differentiating the Lagrangian with respect to $x$, we have:

$$
\nabla_x L(x, \lambda_1) = \nabla f(x) - \lambda_1 \nabla C_1(x)
$$

The condition where $\nabla f(x^*)$ and $\nabla C_1(x^*)$ are parallel is equivalent to the existence of $\lambda_1^*$ (called the Lagrangian multiplier):

$$
\nabla_x L(x^*, \lambda_1^*) = 0
$$

Thus, $x^*$ is a local minimizer.

### Example: Single Inequality

Now we include the interior circle: minimize $x_1, x_2$, subject to:

$$
2 - x_1^2 - x_2^2 \geq 0
$$

This can also be expressed as:

$$
x_1^2 + x_2^2 \leq 2 \quad (C_1(x))
$$

We see that $x^* = (-1, 1)$ is still a global minimizer. At the point $x^*$, $\nabla f(x^*)$ and $\nabla C_1(x^*)$ are parallel.

## Linear Function

**Question:** At a feasible point $x$ where $c_1(x) \geq 0$, can we take a small step $S$ while remaining feasible and decreasing our function value?

**Case 1:** $x$ lies strictly inside the circle $c_1(x) > 0$. In this case, we can simply take a step $S$ proportional to $-\nabla f(x)$ unless $\nabla f(x) = 0$.

**Case 2:** $x$ lies on the boundary of the circle $c_1(x) = 0$. In this case, $c_1$ is active.

$$
\nabla c_1(x) \cdot S \geq 0 \quad \text{and} \quad \nabla f(x) \cdot S \leq 0
$$

**Feasibility** and **Descent**

The only way such an $S$ cannot exist is if $\nabla f(x)$ and $\nabla c_1(x)$ point in the same direction (there exists a non-negative $\lambda$ such that $\nabla f(x) = \lambda \nabla c_1(x)$).

## Lagrangian

We can again combine the objective function and constraint function for a Lagrangian function:

$$
\mathcal{L}(x, \lambda_1) = f(x) - \lambda_1 c_1(x)
$$
## Stationary Condition for Inequality Constraints

Recall: $\nabla_x \Sigma(x, \lambda) = \nabla f(x) - \lambda \nabla C_i(x)$

For the problem with a single inequality constraint, the necessary condition for $x^*$ to be a local minimum can be summarized as:

$$
\nabla_x \Sigma(x^*, \lambda_i^*) = 0 \quad \text{for some } \lambda_i^* \geq 0
$$

Where we also require:

$$
\lambda_i^* C_i(x^*) = 0 \quad (2)
$$

**(2) is known as the complementarity condition.** It ensures $\lambda_i^*$ is zero when $C_i(x^*) > 0$ (even when $x^*$ is strictly inside the circle).

---

## Example: Problem with Two Inequality Constraints

Consider minimizing $x_1 + x_2$ subject to:

1. $2 - x_1^2 - x_2^2 \geq 0$
2. $x_2 \geq 0$

Here, $C_1(x)$ and $C_2(x)$ define the constraints. $x_2$ has a non-smooth boundary.

We find that $x^* = (-\sqrt{2}, 0)^T$ is the global minimizer. At this point:

- Constraint normals $\nabla C_1(x^*)$ and $\nabla C_2(x^*)$ are not parallel to $\nabla f(x^*)$.

$$
\nabla C_1(x) = \begin{bmatrix} -2x_1 \\ -2x_2 \end{bmatrix}, \quad \nabla C_2(x) = \begin{bmatrix} 0 \\ 1 \end{bmatrix}
$$
## Linearization

### Question:
At $x = (-\sqrt{2}, 0)^T$ where $c_1(x) = 0$ and $c_2(x) = 0$, can we take a small step $s$ while remaining feasible and decreasing our function value? This would require:

$$
\nabla c_1(x)^T s \geq 0 \quad \text{and} \quad \nabla c_2(x)^T s \geq 0 \quad \text{and} \quad \nabla F(x)^T s < 0
$$

- Feasibility  
- Descent  

But such an $s$ cannot exist.

### Question:
Same as above, but $x = (\sqrt{2}, 0)^T$. This would require:

$$
\nabla c_1(x)^T s \geq 0 \quad \text{and} \quad \nabla c_2(x)^T s \geq 0 \quad \text{and} \quad \nabla F(x)^T s < 0
$$

- Feasibility  
- Descent  

Can such an $s$ exist?

## Lagrangian

### Lagrangian function:
$$
\mathcal{L}(x, \lambda) = F(x) - \lambda_1 c_1(x) - \lambda_2 c_2(x)
$$

$$
\nabla_x \mathcal{L}(x, \lambda) = \nabla F(x) - \lambda_1 \nabla c_1(x) - \lambda_2 \nabla c_2(x)
$$

$$
\lambda \in \mathbb{R}^2
$$
## Necessary Conditions for Local Minimization

### Problem with Two Inequality Constraints
For the problem with two inequality constraints, the necessary conditions for $x^*$ to be a local minimizer can be summarized as:

$$
\nabla_x \mathcal{L}(x^*, \lambda^*) = 0 \quad \text{for some} \quad \lambda^* \geq 0
$$

Where $c_1$ and $c_2$ are inequality constraints, requiring:

$$
\lambda_1^* \geq 0, \, \lambda_2^* \geq 0
$$

We also require:

$$
\lambda_1^* c_1(x^*) = 0 \quad \text{and} \quad \lambda_2^* c_2(x^*) = 0
$$

This is known as **complementary conditions**.

### Definitions

#### Def 2: Active Set
The active set $A(x)$ at any feasible point $x$ consists of the equality constraint indices from $\mathcal{E}$ together with indices of the inequality constraints $\mathcal{I}$ for which $c_i(x) = 0$:

$$
A(x) = \mathcal{E} \cup \{ i \in \mathcal{I} \mid c_i(x) = 0 \}
$$

#### Def 3: Linear Constraint Qualification (LICQ)
Given a point $x$ and the active set $A(x)$, the LICQ holds if the set of active constraint gradients $\{ \nabla c_i(x), i \in A(x) \}$ is linearly independent.

## 1st Order Optimality Conditions

### Lagrangian Function

Define the Lagrangian function for the general constrained problem:

$$
\mathcal{L}(x, \lambda) = f(x) - \sum_{i \in \mathcal{E} \cup \mathcal{I}} \lambda_i C_i(x)
$$

### Theorem 4: 1st Order Necessary Conditions (KKT Conditions)

Let $x^*$ be a local minimizer of (C1) with $f \in C^1$ and $C_i \in C^1$ and LICQ holds. Then there are Lagrange multipliers $\lambda_i^*, i \in \mathcal{E} \cup \mathcal{I}$ such that the following conditions are satisfied:

- $\nabla_x \mathcal{L}(x^*, \lambda_i^*) = 0$
- $C_i(x^*) = 0$ for all $i \in \mathcal{E}$
- $C_i(x^*) \geq 0$ for all $i \in \mathcal{I}$
- $\lambda_i^* \geq 0$ for all $i \in \mathcal{I}$ (only for inequality constraints)
- $\lambda_i^* C_i(x^*) = 0$ for all $i \in \mathcal{E} \cup \mathcal{I}$

### Gradient Expression

Because $\lambda_i^*$ must be inactive for inactive inequalities, we can write $\nabla_x \mathcal{L}(x^*, \lambda_i^*) = 0$ as:

$$
\nabla_x f(x^*) = \nabla f(x^*) - \sum_{i \in \mathcal{E} \cup \mathcal{I}} \lambda_i^* \nabla C_i(x^*) = 0
$$

At a local minimum $x^*$, the gradient of $f(x)$ can be expressed as:

$$
\nabla f(x^*) = \sum_{i \in A(x^*)} \lambda_i^* \nabla c_i(x^*)
$$

---

## Strict Complementary

**Definition 5: Strict Complementarity**

Given a local minimum $x^*$ of $c(x)$ and a vector $\lambda^*$ satisfying the KKT conditions (8)-(12), strict complementary holds if for each index $i \in \mathcal{E}$, exactly one of $\lambda_i^*$ or $c_i(x^*)$ is 0. This means:

- $\lambda_i^* > 0$ whenever $c_i(x^*) = 0$.

---

## Second-Order Optimality Conditions

Given $x^*$ and $\lambda^*$ satisfy the KKT conditions, a direction $w \in \mathbb{R}^n$ is said to be critical if it meets the following conditions:

$$
\begin{cases} 
\nabla c_i(x^*)^T w = 0 & \forall i \in \mathcal{E}, \\
\nabla c_i(x^*)^T w = 0 & \forall i \in A(x^*) \text{ with } \lambda_i^* > 0, \\
\nabla c_i(x^*)^T w \geq 0 & \forall i \in A(x^*) \text{ with } \lambda_i^* = 0.
\end{cases}
$$

It follows that $w \in \mathcal{F}(x^*)$, and as a result of these conditions, we have:

$$
\sigma = \nabla_x \mathcal{L}(x^*, \lambda^*)^T w = \nabla f(x^*)^T w + \sum_{i \in \mathcal{E} \cup \mathcal{A}} \lambda_i^* \nabla c_i(x^*)^T w = \nabla f(x^*)^T w
$$
- So since $\nabla f(x^*)^T W = 0$, we see that critical directions $W$ are directions for which it is not known from 1st order information if $f$ will decrease or increase.

## 2nd Order KKT Conditions

### Theorem 6: 2nd Order Necessary Conditions

Let $x^*$ be a local minimizer of $f$ with $f \in C^2$ and all $g_i \in C^2$, and LICQ holds. Then for any critical direction $W$:

$$
W^T \nabla_{xx}^2 L(x^*, \lambda^*) W \geq 0 \quad (14)
$$

For a sufficient condition, we can use a strict inequality $(> 0)$ in (14) for $W \neq 0$.
