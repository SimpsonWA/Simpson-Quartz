
We begin with the standard primal and dual formulations:

$$
\min_{x} c^T x \quad \text{s.t.} \quad Ax = b, \quad x \geq 0
$$

The corresponding dual problem is:

$$
\max_{\lambda, s} b^T \lambda \quad \text{s.t.} \quad A^T \lambda + s = c, \quad s \geq 0
$$

### KKT Conditions

The KKT conditions for the primal-dual pair are:

$$
A^T \lambda + s = c
$$

$$
Ax = b
$$

$$
x, s \geq 0
$$

$$
x_i s_i = 0 \quad \text{for all } i
$$

To solve for $(x^*, \lambda^*, s^*)$, we reformulate the conditions as:

$$
F(x, \lambda, s) = \begin{bmatrix} A^T \lambda + s - c \\ Ax - b \\ XSe \end{bmatrix} = 0 \quad \text{and} \ x,s \geq 0 \tag{2}
$$

where:

$$
X = \text{diag}(x_1, \dots, x_n), \quad S = \text{diag}(s_1, \dots, s_n), \quad e = (1, \dots, 1)^T
$$
Our goal is to solve $F(x,\lambda,s)$ and the inequality $x,s\geq 0$ to find ($x^*,\lambda^*,s^*$)


## Properties of Interior Point Methods

- Interior point methods create $(x^k, y^k, s^k)$ that satisfy:
  - $x^k > 0$ and $s^k > 0$ (interior points only)
  - $A^T y^k + s^k - c \approx 0$ and $Ax^k - b \approx 0$
  - $\|A^T y^k + s^k - c\| \to 0$ and $\|Ax^k - b\| \to 0$ as $k \to \infty$

- Duality measure:
  $$
  \mu^k = \frac{(s^k)^T x^k}{n} \to 0 \text{ monotonically as } k \to \infty
  $$

## Pure Newton for Root Finding

- Recall univariate $(n = 1)$ Newton's method for finding zeros of a function $f(x)$:
  $$
  x^{k+1} = x^k - \frac{f(x^k)}{f'(x^k)}
  $$

- So for the multivariate function $F(x, \lambda, s)$, the pure Newton search direction is:
  $$
  \begin{pmatrix}
  0 & A^T & I \\
  A & 0 & 0 \\
  S^k & 0 & X^k
  \end{pmatrix}
  \begin{pmatrix}
  \Delta y \\
  \Delta x \\
  \Delta s
  \end{pmatrix}
  =
  \begin{pmatrix}
  A^T y^k + s^k - c \\
  Ax^k - b \\
  X^k S^k e
  \end{pmatrix}
  $$



- Though we don't completely adopt his idea as taking steps in $(\Delta x, \Delta \lambda, \Delta s)$ we will violate the condition for $x, s \geq 0$. Though we could take small steps as a scale of $(\Delta x, \Delta \lambda, \Delta s)$ though convergence would be slow:
    - Affine search direction $(\Delta x, \Delta \lambda, \Delta s)$

### Relaxing Newton

- Recall the duality measure that gives us the average of the pairwise products $x_k s_k$. Suppose we don't aim to zero these out at the rate $\mu_k$, but we aim to reduce the duality measure to $\sigma_k \mu_k$ for some $\sigma_k \in (0, 1)$.
    
- Thus, the modified search direction becomes:
    
$$
\begin{pmatrix} 0 & A^T & I \\ A & 0 & 0 \\ S_k & 0 & X_k \end{pmatrix} \begin{pmatrix} \Delta x \\ \Delta \lambda \\ \Delta s \end{pmatrix} =

\begin{pmatrix} A^T \lambda + s - c \\ Ax - b \\ S_k X_k e - \sigma_k \mu_k e \end{pmatrix} $$
# Idea of path-following method

- For a given $τ \geq 0$ lets relax the complementary conditions and consider:
  $$
  F_{τ}(x, \lambda, s) = \begin{bmatrix}
  A^T \lambda + s - c \\
  Ax - b \\
  XSe - τe
  \end{bmatrix} = 0, \quad x, s \geq 0 \tag{1}
  $$

- So when $τ = 0$ we get original KKT given by (2)

- For any $τ > 0$, (1) has a unique solution $(x(τ), \lambda(τ), s(τ))$ if the original problem (2) has a solution

- Duality measure:
  $$
  \mu = \frac{s(τ)^T x(τ)}{n} = τ
  $$

- The central path is given:
  $$
  C := \left\{ (x(τ), \lambda(τ), s(τ)) \mid τ > 0 \right\}
  $$

## Using the central path

- Rather than taking Newton steps towards $(x^*, \lambda^*, s^*)$, most primal-dual path-following methods take a series of Newton steps towards the central path, letting $\tau \to 0$ along the way.

$$
\ldots
$$

$$
\ldots
$$

4. Copy Algorithm Slide 14

5. Copy extensions to the algorithm.

6. Copy Mehrotra's method (combination of all the extensions)
