# Descent Directions

### Definition 

Let $f \in C^1$ (continuously differentiable) and consider a point $x \in \mathbb{R}^n$. A vector $p \in \mathbb{R}^n$ is called a **descent direction** of $f$ at $x$ if:  
$$
p^T \nabla f(x) < 0
$$  
This condition ensures that moving in the direction $p$ decreases the value of $f$ locally.


### Local Decrease

If $f \in C^1$, $x \in \mathbb{R}^n$, and $p \in \mathbb{R}^n$ is a descent direction of $f$ at $x$, then for all sufficiently small $\epsilon > 0$, the function satisfies:  
$$
f(x + \epsilon p) < f(x)
$$  
This result formalizes the notion that taking a small step along a descent direction reduces the function value.


### Steepest Descent Direction

Among all descent directions $p$ with a normalized length $\|p\|_2 = 1$, the direction of **steepest descent** is given by:  
$$
p = -\frac{\nabla f(x)}{\|\nabla f(x)\|_2} \tag{1}
$$  
This direction corresponds to the negative gradient of $f(x)$ and achieves the maximum rate of decrease in $f$.



### SPD Matrix Times Steepest Descent Direction

Let $f \in C^1$, $x \in \mathbb{R}^n$, and $p$ be the steepest descent direction defined in \((1)\). For any symmetric positive definite (SPD) matrix $B \in \mathbb{R}^{n \times n}$, the vector $Bp$ is also a descent direction of $f$ at $x$.  
This follows from the property $p^T B^T \nabla f(x) < 0$, which preserves the descent condition for SPD matrices $B$.


# Gradient Descent Algorithm



### Gradient Descent

At each iteration of the gradient descent algorithm, we take a step in the direction of the negative gradient:  
$$
x_{k+1} = x_k - \alpha_k \nabla f(x_k) \quad k = 0, 1, 2, \ldots
$$  

Where $\alpha_k > 0$ is the step size, and:  
$$
x_{k+1}, x_k \in \mathbb{R}^n, \quad \nabla f(x_k) \in \mathbb{R}^n, \quad \alpha_k \in \mathbb{R}
$$  

Since the algorithm moves in the direction of the negative gradient, it is also known as the **steepest descent algorithm**.


### Gradient Descent Stepsizes

Stepsizes $\alpha_k$ can be updated at each iteration using the **line search method**:  
$$
\alpha_k = \arg \min_{\alpha} f(x_k - \alpha \nabla f(x_k))
$$  
This approach finds the optimal step size $\alpha_k$ by minimizing the function along the descent direction.


### Stepsize Choice for L-Smooth Functions

A function $f \in C^1$ is **L-smooth** if its gradient satisfies the Lipschitz condition:  
$$
\| \nabla f(y) - \nabla f(x) \|_2 \leq L \| y - x \|_2 \quad \forall x, y \in \mathbb{R}^n
$$  

For $L$-smooth functions, a good choice of step size $\alpha$ is:  
$$
\alpha = \frac{1}{L}
$$  

With this choice, the gradient descent algorithm proceeds as:  
$$
x_{k+1} = x_k - \frac{1}{L} \nabla f(x_k) \quad k = 0, 1, 2, \ldots
$$


# Step Size Interpretation

#### Lemma 5: Optimal Step Size in Gradient Descent

Let $f: \mathbb{R}^n \rightarrow \mathbb{R}$ be $L$-smooth and let $x_k \in \mathbb{R}^n$. The following quadratic upper bound holds for $f$ at $x_k$:  
$$
f(y) \leq f(x_k) + \nabla f(x_k)^T (y - x_k) + \frac{L}{2} \| y - x_k \|_2^2 \quad (2)
$$  

The right-hand side of \((2)\) is minimized by:  
$$
y = x_k - \frac{1}{L} \nabla f(x_k)
$$  

Thus, the minimum of the quadratic approximation $g(y)$ is achieved at:  
$$
x_k - \frac{1}{L} \nabla f(x_k)
$$

### Descent Lemma

**Lemma 6:** If $f: \mathbb{R}^n \rightarrow \mathbb{R}$ is $L$-smooth, then gradient descent with a constant step size $\alpha = \frac{1}{L}$ satisfies:  
$$
f(x_{k+1}) \leq f(x_k) - \frac{1}{2L} \| \nabla f(x_k) \|_2^2
$$  
This inequality guarantees that each step decreases the function value proportionally to the squared gradient norm.

#### Theorem 7: Convergence of Gradients to Zero

Let $f: \mathbb{R}^n \rightarrow \mathbb{R}$ be $L$-smooth and bounded below ($f(x) \geq \bar{f}$ for all $x$). Then, gradient descent with a constant step size $\alpha = \frac{1}{L}$ generates a sequence of iterates where the gradient converges to zero:  
$$
\lim_{k \to \infty} \| \nabla f(x_k) \|_2 = 0
$$  
This result ensures that the gradient descent algorithm converges to a critical point of $f$.

Moreover, among the first $k$ iterations, there exists an iterate $x_m$ such that:  
$$
\| \nabla f(x_m) \|_2 \leq \sqrt{\frac{2L(f(x_0) - \bar{f})}{k}}
$$  
This bound shows that the gradient at some iterate $x_m$ is proportional to the decrease in the function value over $k$ iterations.

# Convergence in Convex Case

#### Lemma 8: Tangent of a Convex Function

If $f \in C^1$, then $f$ is convex if for any $x, y \in \mathbb{R}^n$:  
$$
f(y) \geq f(x) + \nabla f(x)^T (y - x)
$$  
This condition implies that the function lies above the tangent hyperplane at any point $x$.


#### Lemma 9: Hessian of a Convex Function

If $f \in C^2$, then $f$ is convex if its Hessian is positive semidefinite:  
$$
\nabla^2 f(x) \succeq 0
$$  
for all $x \in \mathbb{R}^n$.  
This condition ensures that the function has no local maxima and is "curved upwards" everywhere.


#### Theorem 10: Convergence of Gradient Descent under Convexity

Let $f \in C^1$ be $L$-smooth and convex with minimizer $x^* \in \mathbb{R}^n$. Then gradient descent with constant step size $\alpha = \frac{1}{L}$ converges to the optimal value $f^* = f(x^*)$ with the following rate:  
$$
f(x_k) - f^* \leq \frac{1}{2k} \| x_0 - x^* \|_2^2
$$  
This result shows that the function value decreases at a rate proportional to $\frac{1}{k}$ after $k$ iterations, where $x_0$ is the initial point and $x^*$ is the minimizer.

# Strong Convexity

### Definition: Strong Convexity

A function $f: \mathbb{R}^n \rightarrow \mathbb{R}$ is **strongly convex** with parameter $m$ if there exists $m > 0$ such that:  
$$
f((1-\alpha)x + \alpha y) \leq (1-\alpha)f(x) + \alpha f(y) - \frac{m}{2} \alpha (1-\alpha) \|x-y\|^2
$$  
for all $x, y \in \mathbb{R}^n$ and $\alpha \in [0, 1]$.

This definition means that $f$ lies significantly above its linear interpolation, with a margin proportional to $\|x-y\|^2$.


### Implication of Strong Convexity

A key implication of strong convexity is that $f$ lies well above any tangent of $f$.


#### Lemma 1: Tangent of a Strongly Convex Function

If $f \in C^1$, then $f$ is strongly convex with parameter $m$ if for any $x, y \in \mathbb{R}^n$:  
$$
f(y) \geq f(x) + \nabla f(x)^T (y - x) + \frac{m}{2} \|y - x\|^2
$$  
This inequality shows that the function not only lies above the tangent hyperplane at $x$ but also includes a quadratic term that ensures strong separation from the tangent.

#### Lemma 2: Hessian of a Strongly Convex Function

If $f \in C^2$, then $f$ is strongly convex with parameter $m$ if:  
$$
\nabla^2 f(x) \succeq mI
$$  
for all $x \in \mathbb{R}^n$.  
This means that the smallest eigenvalue of the Hessian is at least $m > 0$, ensuring that $f$ has a strong upward curvature everywhere.

# Convergence of Gradient Descent under Strong Convexity

#### Theorem: First Convergence of Gradient Descent under Strong Convexity

Let $f \in C^2$ be **L-smooth** and **strongly convex** with parameter $\mu$.  

If gradient descent is performed with **exact line search**, where the stepsize is determined by:  
$$
\alpha_k = \arg \min_{\alpha} f(x_k - \alpha \nabla f(x_k)),
$$  
then the algorithm converges to the optimal value $f^*$ with the following rate:  
$$
f(x_k) - f^* \leq \left(1 - \frac{\mu}{L}\right)^k (f(x_0) - f^*),
$$  
where:  
- $\mu > 0$ is the strong convexity parameter,  
- $L > 0$ is the Lipschitz constant of the gradient,  
- $f^* = f(x^*)$ is the minimum value of $f$,  
- $x_k$ represents the sequence of iterates.

### Key Implications:
- **Exponential Convergence**: The term $\left(1 - \frac{\mu}{L}\right)^k$ ensures **linear (geometric)** convergence to the optimal value $f^*$.
- **Convergence Rate**: The ratio $\frac{\mu}{L}$ determines the speed of convergence. A larger $\frac{\mu}{L}$ implies faster convergence.
- **Exact Line Search**: Using exact line search ensures the optimal stepsize at each iteration, leading to efficient convergence.

This result highlights the benefits of strong convexity in achieving faster convergence rates in gradient descent.

