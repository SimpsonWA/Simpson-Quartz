
# What is a Solution?

For an objective function $f: \mathbb{R}^n \rightarrow \mathbb{R}$, the goal is to solve:  
$$
\min_{x \in \mathbb{R}^n} f(x)
$$

### Types of Solutions

1. **Global Minimizer** $(x^*)$:  
   $f(x^*) \leq f(x)$ for all $x \in \mathbb{R}^n$.  
   - The solution is the absolute best value across the entire domain.

2. **Strict Global Minimizer** $(x^*)$:  
   $f(x^*) < f(x)$ for all $x \in \mathbb{R}^n$ with $x^* \neq x$.  
   - No other point achieves the same value as $f(x^*)$.

3. **Local Minimizer** $(x^*)$:  
   There exists a neighborhood $U(x^*)$ containing $x^*$ such that:  
   $f(x^*) \leq f(x)$ for all $x \in U(x^*)$.  
   - The solution is the best within a small region around $x^*$.

4. **Strict Local Minimizer** $(x^*)$:  
   There exists a neighborhood $U(x^*)$ containing $x^*$ such that:  
   $f(x^*) < f(x)$ for all $x \in U(x^*)$ with $x \neq x^*$.  
   - No other point in the local neighborhood achieves the same value as $f(x^*)$.

---

## Optimality Conditions

**Stationary Points**:
A point $x^* \in \mathbb{R}^n$ is a **stationary point** of $f$ if:  
$$
\nabla f(x^*) = 0
$$

**First-Order Necessary Condition**:
If $f$ is continuously differentiable ($f \in C^1$) and $x^* \in \mathbb{R}^n$ is a local minimizer of $f$, then:  
$$
\nabla f(x^*) = 0
$$
- **Interpretation**: Every local minimizer of $f$ must also be a stationary point.

**Second-Order Necessary Conditions**:
If $f$ is twice continuously differentiable ($f \in C^2$) and $x^* \in \mathbb{R}^n$ is a local minimizer of $f$, then:  
1. $\nabla f(x^*) = 0$  
2. $\nabla^2 f(x^*) \succeq 0$ (the Hessian is positive semi-definite).

**Second-Order Sufficient Conditions**:
If $f$ is twice continuously differentiable ($f \in C^2$) and:
1. $\nabla f(x^*) = 0$  
2. $\nabla^2 f(x^*) \succ 0$ (the Hessian is positive definite),  

then $x^*$ is a **strict local minimizer** of $f$.

---

## Minimizers of Convex Functions

### Definition: Convex Function
A function $f: \mathbb{R}^n \rightarrow \mathbb{R}$ is **convex** if for any $x, y \in \mathbb{R}^n$ and $\alpha \in [0, 1]$,  
$$
f(\alpha x + (1 - \alpha) y) \leq \alpha f(x) + (1 - \alpha) f(y)
$$

### Key Properties
1. If $f$ is convex, any **local minimizer** $x^*$ is also a **global minimizer**.
2. If $f$ is convex and differentiable, any **stationary point** $x^*$ is a **global minimizer**.

---

### Summary of Necessary and Sufficient Conditions

| Condition                           | Requirements                   | Result                          |
|-------------------------------------|--------------------------------|---------------------------------|
| First-Order Necessary Condition     | $\nabla f(x^*) = 0$            | Local minimizer candidate.      |
| Second-Order Necessary Condition    | $\nabla f(x^*) = 0$ and $\nabla^2 f(x^*) \succeq 0$ | Local minimizer candidate.      |
| Second-Order Sufficient Condition   | $\nabla f(x^*) = 0$ and $\nabla^2 f(x^*) \succ 0$ | Strict local minimizer.         |
| Convex Function + Stationary Point  | $f$ convex, $\nabla f(x^*) = 0$ | Global minimizer.               |
