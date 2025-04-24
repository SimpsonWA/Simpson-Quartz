## L18 Proximal Methods

### Proximal Operators

**Def 1: Closed Function**  
$f:\mathbb{R}^n \rightarrow \mathbb{R} \cup \{+\infty\}$ is **closed** if its **epigraph**:

$$epi(f) := \{(x,t) \in \mathbb{R}^n \times \mathbb{R} \mid f(x) \leq t\}$$

is a closed subset of $\mathbb{R}^{n+1}$.

**Def 2: Proper Convex Function**  
A function $f:\mathbb{R}^n \rightarrow \mathbb{R} \cup \{+\infty\}$ is proper convex if:

- $f(x) < +\infty$ for at least one point $x$ and  
- $f$ is convex.

**Def 3: Proximal Operator**  
The proximal operator $prox_f: \mathbb{R}^n \rightarrow \mathbb{R}^n$ of a closed proper convex function $f:\mathbb{R}^n \rightarrow \mathbb{R} \cup \{+\infty\}$ is given by:

$$prox_f(u) = \arg \min_x \left( f(x) + \frac{1}{2} \|x - u\|_2^2 \right)$$
### Scaled Proximal Operators
We often encounter proximal operators of a scaled function $tf$ (for $t \geq 0$), so:

$$\text{prox}_{tf}(u) = \arg \min_x (tf(x) + \frac{1}{2} \|x - u\|_2^2)$$

$$= \arg \min_x (f(x) + \frac{1}{2t} \|x - u\|_2^2)$$

- $\text{prox}_{tf}$: scaled version of the proximal operator of $f$

### Fixed Points
- Suppose $f$ is a proper convex function. Then a point $x^* \in \mathbb{R}^n$ is a global minimizer of $f$ if and only if it is a fixed point of $\text{prox}_{tf}$:

$$x^* = \text{prox}_{tf}(x^*)$$

### Moreau-Yosida Regularization
- Given $t \geq 0$, the Moreau envelope of $f$ with parameter $t$ is given by:

$$M_{tf}(u) = \inf_x (tf(x) + \frac{1}{2t} \|x - u\|_2^2)$$

- The Moreau envelope represents the value related to the proximal operator.

$$
M_{ef}(U) = \left( f(x) + \frac{1}{2t} \|x - u\|^2 \right) \bigg|_{x = \text{prox}_{tf}(U)}
$$

So the most important fact is that the Moreau envelope $M_{ef}(U)$ has the same minimizer as $f$.

### Moreau Gradient

The gradient of the Moreau envelope is the proximal operator:

$$
\text{prox}_{tf}(U) = U - t \nabla M_{ef}(U)
$$

### Proximal Algorithms

Iterations of the proximal minimization algorithm:

$$
X_{k+1} = \text{prox}_{tf}(X_k)
$$

Also known as the proximal point algorithm.

### Proximal Gradient Method

Suppose we have an optimization problem where the objective function can be decomposed as:

$$
\min f(x) + g(x)
$$

- $f: \mathbb{R}^n \to \mathbb{R}$ is closed, proper, convex, and differentiable.
- $g: \mathbb{R}^n \to \mathbb{R} \cup \{+\infty\}$ is closed, proper, and convex.

## Proximal Gradient Algorithm

The iterations of the proximal gradient algorithm are:

$$ x_{k+1} = \text{prox}_{\eta g} \left( x_k - \eta \nabla f(x_k) \right) $$

where $\eta$ represents the time steps.

If we add $f = 0$, $y = 0$, and $g = I_{\mathbb{R}}$, we obtain a specific case where $\eta f$ influences the optimization process.

Adding acceleration leads to an **accelerated proximal gradient method**.

## Alternating Direction Method of Multipliers (ADMM)

Consider an optimization problem decomposed as:

$$ \min (f(x) + g(y)) $$

where both $f$ and $g$ are closed and convex.

The iterations of the ADMM algorithm are:

$$ x_{k+1} = \text{prox}_{\eta f} (z_k - u_k) $$

$$ z_{k+1} = \text{prox}_{\eta g} (x_{k+1} + u_k) $$

$$ u_{k+1} = u_k + x_{k+1} - z_{k+1} $$

ADMM guarantees convergence at a rate of $O\left(\frac{1}{k}\right)$.

## Alternating Direction Method of Multipliers (ADMM)

Consider the optimization problem:

$$
\min_{x,z} f(x) + g(z) \quad \text{s.t.} \quad x = z, \tag{1}
$$

This is known as the **consensus form** of the original problem $\min_{x} f(x) + g(x)$.

### Lagrangian Formulation

The Lagrangian function for (1) is:

$$
\mathcal{L}(x,z,y) = f(x) + g(z) + y^T(x - z).
$$

### Augmented Lagrangian Formulation

The augmented Lagrangian adds a quadratic penalty term:

$$
\mathcal{L}_p(x,z,y) = f(x) + g(z) + y^T(x - z) + \frac{p}{2} \|x - z\|_2^2.
$$

where $p > 0$ is a penalty parameter promoting consensus.

### ADMM Algorithm Steps

The ADMM updates follow:

1. **Minimization with respect to $x$**  
   $$ x_{k+1} = \arg\min_x \mathcal{L}_p(x, z_k, y_k) $$
   
2. **Minimization with respect to $z$**  
   $$ z_{k+1} = \arg\min_z \mathcal{L}_p(x_{k+1}, z, y_k) $$

3. **Dual variable update**  
   $$ y_{k+1} = y_k + p(x_{k+1} - z_{k+1}) $$

### Convergence

ADMM is guaranteed to converge at a rate of $O\left(\frac{1}{k}\right)$ under convex assumptions.

