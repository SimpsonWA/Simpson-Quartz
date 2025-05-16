## Nonlinear Dynamic Systems

-  Nonlinear process model:
$$x_k = f(u_k, x_{k-1}) + w_k$$

-  Nonlinear measurement model:
$$z_k = h(x_k) + v_k$$

## Nonlinear Dynamic Systems with Multiplicative Noise

-  Nonlinear process model:
$$x_k = f(u_k, x_{k-1}, w_k)$$

-  Nonlinear measurement model:
$$z_k = h(x_k, v_k)$$

## Uncertainty Propagation

**Q:** How to map belief through a nonlinear function:

**Key ideas:**
- Linearization via Taylor's expansion
- Extended Kalman Filter (EKF)
- **Unscented Transform**
  - Unscented Kalman Filter (UKF)
- **Monte-Carlo Methods**
  - Sequential Monte-Carlo Methods (Particle Filters)

## Linearization via Taylor Expansion

Linearization of a function $f: \mathbb{R}^n \rightarrow \mathbb{R}^m$ around a point $a$:

$$
f(x) \approx f(a) + \frac{\partial f}{\partial x} \bigg|_{x=a} (x - a)
$$

$$
\approx x_0 + Fx
$$

Since this is affine, a Gaussian can be propagated through an affine map.

Given that $x \sim \mathcal{N}(\mu, \Sigma)$ and $y = Ax + b$, we get:

$$
y \sim \mathcal{N}(A\mu + b, A\Sigma A^T)
$$

### EKF Algorithm

