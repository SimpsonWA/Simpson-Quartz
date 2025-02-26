# Definitions:

**Objective**: a scalar quantitively measure of the performance of the system under study

**Modeling**: The process of identifying objective, variables, and constraints for a given problem

**Optimality conditions**: mathematical expressions for checking that the current set of variables is indeed the solution of the problem

**Constrained**: A type of optimization problem where the solution is subject to certain restrictions or conditions, called constraints. These constraints can be equalities (e.g $g(x) = 0$) or inequalities (e.g $h(x) \leq 0$)

**Unconstrained**: A type of optimization problem without any restrictions or conditions. The goal is to find the maximum or minimum of a function $f(x)$ in an open domain.

**Continuous optimization**:  Optimization problems where the variables can take any value within a continuous range, typically represented by real numbers. Such problems are often solved using calculus-based methods. Example: Minimizing $f(x) = x^2$ where $x$ can be any real number.

**Discrete  optimization**: Optimization problems where the variables are restricted to discrete values, such as integers or binary values. These problems often arise in scheduling, allocation, or combinatorics.  
Example: Assigning jobs to workers such that the total cost is minimized, where assignments are binary (assigned = 1, not assigned = 0).

**Global optimization**: The process of finding the absolute best solution (global minimum or maximum) to an optimization problem across the entire domain. This often requires overcoming local solutions that are suboptimal.

**local optimization**: The process of finding the best solution within a localized region of the domain, often relying on gradient-based methods. Local solutions may not be the best overall.

**Stochastic optimization**: Optimization techniques that incorporate randomness or probabilistic components, often used when the objective function is noisy, expensive to evaluate, or incomplete.

**Deterministic Optimization**: Optimization methods that rely on exact and predictable rules, producing the same results given the same initial conditions. These methods do not include randomness and typically involve systematic techniques like gradient descent or Newton's method.

**Feasible region**: The set of all points in the domain of an optimization problem that satisfy all the given constraints (both equality and inequality). The feasible region represents the allowable solutions to the problem, and optimization is performed within this region. It can be a bounded or unbounded subset of the domain depending on the problem.

**Integer programming**: A type of optimization problem where some or all the decision variables are restricted to take integer values.

**linear programming**: When the objective function and all the constraints are linear functions of x

**Nonlinear programming**: where at least some of the constraints or the objective are nonlinear functions

**Convex** : 
A term used to describe certain mathematical properties of sets and functions that play a crucial role in optimization problems. Convexity ensures that the optimization problem has favorable properties, such as the absence of local minima that are not global minima. The definitions of convexity in the context of sets and functions are as follows:

**Convex Set**:
A set $S$ in a vector space is convex if, for any two points $x_1, x_2 \in S$ and any $\lambda$ such that $0 \leq \lambda \leq 1$, the point $\lambda x_1 + (1-\lambda)x_2$ also belongs to $S$.  
- **Example**: A circle, an ellipse, or a polygon without indentations is a convex set.  

**Convex Function**:
A function $f(x)$ is convex if, for any two points $x_1, x_2$ in its domain and any $\lambda$ such that $0 \leq \lambda \leq 1$, it satisfies:  
$$f(\lambda x_1 + (1-\lambda)x_2) \leq \lambda f(x_1) + (1-\lambda) f(x_2)$$  
This implies that the line segment between any two points on the graph of the function lies above or on the graph.  

# Notes

## Overview

- Optimization problems involve:
  - An **objective**: A scalar measure of system performance.
  - **Variables**: The characteristics of the system affecting the objective.
  - **Constraints**: Restrictions that must be satisfied by the solution.
- The goal is to find values that satisfy constraints while optimizing (minimizing or maximizing) the objective.

## Steps in Optimization

1. **Modeling**: Identify the objective, variables, and constraints for the problem.
2. **Solving**: Use optimization algorithms (often with computers) to find solutions.
3. **Analyzing**: Verify the solution using **optimality conditions**.

---

## Mathematical Formulation

The general optimization problem can be expressed as:  
$$
\min_{x \in \mathbb{R}^n} f(x) \quad \text{subject to} \quad
\begin{cases} 
c_i(x) = 0, & i \in \epsilon \\ 
c_i(x) \geq 0, & i \in \mathcal{I}
\end{cases}
$$  

- $f: \mathbb{R}^n \rightarrow \mathbb{R}$: **Objective function**.  
- $x = (x_1, \ldots, x_n)^\top \in \mathbb{R}^n$: Vector of variables (unknowns or parameters).  
- $c_i: \mathbb{R}^n \rightarrow \mathbb{R}$: **Constraint functions**.  
- $\epsilon$: Index set for equality constraints.  
- $\mathcal{I}$: Index set for inequality constraints.  
- $S = \{x \in \mathbb{R}^n : c_i(x) = 0 \ \forall i \in \epsilon, \ c_i(x) \geq 0 \ \forall i \in \mathcal{I}\}$: **Feasible set**.
