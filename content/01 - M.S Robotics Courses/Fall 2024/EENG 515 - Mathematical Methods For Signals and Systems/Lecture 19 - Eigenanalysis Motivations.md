
## Discrete time LTI Systems:

- **LTI**: Linear and time invariant
- We can write $x[n]$ as a sum of scaled and shifted impulses:
$$
x[n] = \sum_{k=-\infty}^{\infty} x[k]\delta[n-k] \quad (1)
$$
- And we can write $y[n]$ as a sum of scaled and shifted impulse responses:
$$
y[n] = \sum_{k=-\infty}^{\infty} x[k]h[n-k] \quad (2)
$$
- This is known as the convolution formula

- For every LTI system, there are certain input signals for which the resulting output signal is merely a scaled version of the input signal:
$$
y[n] = \alpha x[n] \quad (3)
$$
- $(3)$ For some $\alpha \in \mathbb{C}$. These input signals are called eigenfunctions (or **eigenvectors**) of the system

- **Theorem (Eigenfunctions of an LTI system)** : For any LTI system, every complex exponential signal of form $x[n] = e^{jw_{0}n}$ (for every $w_{0} \in \mathbb{R}$) is an eigenfunction of the system

- Using discrete time Fourier Transform (**DTFT**) we can write $x[n]$ as a linear combination of complex exponentials:
$$
x[n] = \frac{1}{2\pi} \int_{-\pi}^{\pi} X(e^{jw})e^{jwn}\ dw \quad (4)
$$
- $(4)$: Where DTFT coefficients are given by:
$$
X(e^{jw}) = \sum_{n=-\infty}^{\infty} x[n] e^{-jwn}
$$
- Suppose $x[n]$ and $h[n]$ are linear combinations of complex exponentials
$$
\begin{align}
x[n] = \frac{1}{2\pi} \int_{-\pi}^{\pi} X(e^{jw})e^{jwn}\ dw \quad (4) \\
h[n] = \frac{1}{2\pi} \int_{-\pi}^{\pi} H(e^{jw})e^{jwn}\ dw  \quad (5)
\end{align}
$$
- We can write $y[n]$ as a linear combination of these ($4,5$) responses:
$$
y[n] = \frac{1}{2\pi} \int_{-\pi}^{\pi} X(e^{jw})H(e^{jw})e^{jwn}\ dw \quad (6)
$$
- We can think of an LTI system as a multiplier in the Frequency domain
$$
y[n] = IDTFT\{DTFT\{x[n]\} * DTFT\{h[n]\}\}
$$
- Where $IDTFT$: Inverse discrete time Fourier transform 

## Finding eigenvalues and eigenvectors of a matrix

### Finding Eigenvalues

- Suppose $A$ is an $(n \times n)$ matrix
- We want to know: for what values of $\lambda \in \mathbb{C}$ does there exist a non-zero $\vec{x} \in \mathbb{C}^n$ such that:
$$
A\vec{x} = \lambda \vec{x} \quad (7)
$$
- We know that for such a $(\lambda, \vec{x})$ pair to exist we must have:
$$
(A-\lambda I )\vec{x} = \vec{0} \quad (8)
$$
- $(8)$: and there for $\vec{x} \in \cal{N}(A-\lambda I)$

- For such a non-zero $\vec{x}$ to exist in the nullspace of $A - \lambda I$ we need :
$$
dim(\cal{N}(A-\lambda I)) > 0
$$
- We can find all $\lambda$ such that $det(A - \lambda I) = 0$ to get the **Eigenvalues** of $A$:
$$
det(A - \lambda I) = 0
$$

### Finding Eigenvectors

- Suppose $\lambda$ is an eigenvalue of $A$, which has size of $(n \times n)$ 
- Then for every $\vec{x} \in \cal{N}(A-\lambda I)$ is considered an eigenvector of $A$. Corresponding to the eigenvalue $\lambda$
- Because $\cal{N}(A - \lambda I)$ is a linear subspace of $\mathbb{C}^n$ we conventionally just specify enough vectors to span in this subspace.
- So we can say $(A-\lambda I)\vec{v} = \vec{0}$ and the $v$ values that correspond will be the eigenvectors

