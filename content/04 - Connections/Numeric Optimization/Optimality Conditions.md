### Stationary Points:
A point $x^* \in \mathbb{R}^n$ is a **stationary point** of $f$ if:  
$$
\nabla f(x^*) = 0
$$  
This means that the gradient of the function at $x^*$ is zero , indicating a potential local extremum (minimum, maximum, or saddle point).

### First-Order Necessary Condition:
If $f$ is continuously differentiable ($f \in C^1$) and $x^* \in \mathbb{R}^n$ is a [[Local Minimizer]] of $f$, then:  
$$
\nabla f(x^*) = 0
$$  
- **Interpretation**: Every local minimizer must be a stationary point, meaning the gradient of the function at a local minimizer is zero.

### Second-Order Necessary Conditions:
If $f$ is twice continuously differentiable ($f \in C^2$) and $x^* \in \mathbb{R}^n$ is a [[Local Minimizer]] of $f$, then:
1. $\nabla f(x^*) = 0$
2. $\nabla^2 f(x^*) \succeq 0$ (the [[Hessian]] is [[Positive Semi-Definite]]).

- **Interpretation**: For a point to be a local minimizer, not only must the gradient vanish, but the Hessian must also be positive semi-definite at that point. This ensures that the function is curving upwards in all directions locally.

### Second-Order Sufficient Conditions:
If $f$ is twice continuously differentiable ($f \in C^2$) and:
1. $\nabla f(x^*) = 0$
2. $\nabla^2 f(x^*) \succ 0$ (the Hessian is [[Positive Definite]] ),  

then $x^*$ is a [[Strict Local Minimizer]] of $f$.

- **Interpretation**: If the gradient is zero and the Hessian is [[Positive Definite]] , then $x^*$ is not just a local minimum, but a strict local minimum, meaning it is the lowest point in its neighborhood.


| Condition                          | Requirements                                        | Result                     |
| ---------------------------------- | --------------------------------------------------- | -------------------------- |
| First-Order Necessary Condition    | $\nabla f(x^*) = 0$                                 | Local minimizer candidate. |
| Second-Order Necessary Condition   | $\nabla f(x^*) = 0$ and $\nabla^2 f(x^*) \succeq 0$ | Local minimizer candidate. |
| Second-Order Sufficient Condition  | $\nabla f(x^*) = 0$ and $\nabla^2 f(x^*) \succ 0$   | [[Strict Local Minimizer]] |
| Convex Function + Stationary Point | $f$ convex, $\nabla f(x^*) = 0$                     | [[Global Minimizer]]       |
