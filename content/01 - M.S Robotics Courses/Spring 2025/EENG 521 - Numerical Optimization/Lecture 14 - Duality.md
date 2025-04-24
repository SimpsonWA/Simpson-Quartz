## Definitions and Properties

- We consider primal (original) problems of the form:
$$\min_x f(x) \quad \text{s.t.} \quad C(x) \geq 0 \quad (1)$$

- $f: \mathbb{R}^n \rightarrow \mathbb{R}$ as a convex function

- Inequality constraints $C(x)$ in a vector form:
$$C(x) = \left( C_1(x), \ldots, C_m(x) \right)^T \in \mathbb{R}^m \quad \text{for each} \quad i = 1, 2, \ldots, m$$

- $C_i$ is a convex function (By slide 12.6 $\Omega$)

- There are no equality constraints

## Primal Optimality Conditions

- The Lagrangian of function (1) is given by:
$$\mathcal{L}(x, \lambda) = f(x) - \lambda^T C(x) \quad (2)$$

- With the Lagrangian multipliers $\lambda_i$ collected in a vector $\lambda \in \mathbb{R}^m$

- The 1st order KKT conditions are given by:
$$
\nabla_x \mathcal{L}(x^*, \lambda^*) = 0, \quad C(x^*) \geq 0, \quad \lambda^* \geq 0, \quad \lambda_i^* C_i(x^*) = 0 \quad \text{for all} \quad i = 1, \ldots, m
$$
## The Dual Objective

- The main idea with duality is to create an alternative problem from the functions and data that define the primal problem.

- To achieve this, we define the dual objective function $q: \mathbb{R}^m \to \mathbb{R}$ as:

$$
q(\lambda) := \inf_x \mathcal{L}(x, \lambda) \quad (4)
$$

- For some $\lambda$, $\mathcal{L}(\cdot, \lambda)$ may be bounded below, so we define the domain $D$ of $q$ as the set of values $\lambda$ where $q(\lambda)$ is finite:

$$
D := \{\lambda : q(\lambda) > -\infty\}
$$

### Theorem 1: Concavity of the Dual Objective

- The dual objective $q(\lambda)$ is a concave function of $\lambda$, and the domain $D$ of $q$ is a convex set.

- Note: "$\odot$" represents element-wise operations.

## Theorem 2 (Weak Duality)

For any $\bar{x}$ that is feasible for (1) and any $\bar{\lambda} \geq 0$, we have:
$$
f(\bar{x}) \geq g(\bar{\lambda})
$$

---

## The Dual Problem

Using the dual objective function $g(\lambda)$, we can formulate the dual problem of (1) given by:
$$
\max_{\lambda \in \mathbb{R}^m} g(\lambda) \quad \text{such that} \quad \lambda \geq 0
$$

# ADD HERE
---

## Theorem 3 (Duality Theorem)

Suppose $\bar{x}$ is a solution to the primal problem and $f$ and $c_i$ are convex. Then, any $\bar{\lambda}$ for which $(\bar{x}, \bar{\lambda})$ satisfy the KKT conditions (3) is a solution to the dual problem (5).


## Theorem 4: Strong Duality

Suppose that $f$ and $C_2$ are convex and $C_2 \neq \emptyset$. Suppose that $\bar{x}$ is a solution of (1) at which LICQ holds. Suppose that $\lambda^*$ solves (5) and the infimum $\inf_x L(x, \lambda^*)$ is attained at $x^*$. Assume also that $L(x, \lambda^*)$ is strictly convex. Then $\bar{x} = x^*$ and $f(\bar{x}) = L(x^*, \lambda^*)$.

---

## Theorem 5: Slater's Condition

Consider a primal problem of the form:
$$\min_x f(x) \quad \text{such that} \quad Ax = b \quad \text{and} \quad c(x) \geq 0$$

Where $f$ and $-c_i$ are convex. Then the strong duality holds if there exists a strictly feasible point (i.e., some $x \in \mathbb{R}^n$ such that $Ax = b$ and $c(x) > 0$).
