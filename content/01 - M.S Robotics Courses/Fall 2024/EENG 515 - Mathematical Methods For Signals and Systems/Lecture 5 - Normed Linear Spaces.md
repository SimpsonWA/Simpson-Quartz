
## Normed Linear Spaces:

- A **norm** is a function used to measure the size of vectors in a vector space
- **Norm** Def: A norm $||*||$ on a vector space $S$ (with scalar field $R = \mathbb{R}$ or $R = \mathbb{C}$) is a mapping $||*|| : S \rightarrow R$ with the following properties
	- $||\vec{x}|| \geq 0$ for all $\vec{x} \in S$ and $||\vec{x}|| = 0$ if $\vec{x} = \vec{0}$
	- **Triangle Inequality**: $||\vec{x}+\vec{y}|| \leq ||\vec{x}|| + ||\vec{y}||$ for all $\vec{x}$,$\vec{y} \in S$
	- $||a\vec{x}|| = |a| * ||\vec{x}||$ for any $a \in R$ and $\vec{x} \in S$
- **Normed Linear Space** Def: A normed linear space is a vector space $S$ (with scalar field $R = \mathbb{R}$ or $R = \mathbb{C}$) together with a valid norm $||*|| : S \rightarrow R$ 
- Norms give way to measure distance in a vector space: For any $\vec{x}$,$\vec{y} \in S$ we can define the distance between $\vec{x}$ and $\vec{y}$ to be:
$$
d(\vec{x},\vec{y}) = ||\vec{x}-\vec{y}||
$$
- Keep in mind a norm is a real value (scalar)

### $l_p$ norms and $l_p$ spaces:

- the $l_p$ metrics for vectors in $\mathbb{R}^n$ and $\mathbb{c}^n$ extend naturally to $l_p$ norms for these spaces:
	- $l_1$ norm: 
		- $||\vec{x}||_1 = \sum_{i=1}^{n} |x_i|$
	- $l_2$ norm ("**Euclidian**"):
		- $||\vec{x}||_2 = (\sum_{i=1}^{n} |x_i|^2)^{\frac{1}{2}}$
	- $l_p$ norm from $1 \leq p \leq \infty$:
		- $||\vec{x}||_p = (\sum_{i=1}^{n} |x_i|^p)^{\frac{1}{p}}$
	- $l_\infty$ norm:
		- $||\vec{x}||_\infty = max_{i=1,2,....,n} |x_i|$
	- A given sequence can have an $\infty$ $l_p$ norm. It is often useful to restrict out attention to those sequences having finite $l_p$ norm
	- **The Space $l_p$** def: The normed linear space $l_p$ consists of all $\infty$ sequences of real and complex numbers with $||\vec{x}||_p < \infty$
- **Theorem (Holder Inequality )**:
	- Suppose $1 \leq p$, $q \leq \infty$ with $\frac{1}{p} + \frac{1}{q} = 1$ . For any 2 sequences $\vec{x} = (x_1,x_2,....) \in l_p$ and $\vec{y} = (y_1,y_2,....) \in l_p$
$$
	\sum_{i=1}^{\infty} |x_i y_i^*| \leq ||\vec{x}||_p ||\vec{y}||_p
$$
	- Equality is achieved if $|\vec{x}_i|^p = \alpha |\vec{y}_i|^q \forall i$, for some $\alpha \in \mathbb{c}$
- By taking $p=q=2$ in the Hodler Inequality, we obtain a widely used corollary
- **Corollary (Cauchy-Schwarz inequality)**:
	- For any 2 sequences $\vec{x} = (x_1,x_2,...) \in l_2$ and $\vec{y} = (y_1,y_2,...) \in l_2$:
$$
		\sum_{i=1}^{\infty} |x_i y_i^*| \leq ||\vec{x}||_2 ||\vec{y}||_2
$$
## $L_p$ norms and $L_p$ Spaces:

- When $S$ is the set of real or complex valued functions $x(t)$ on the interval $t \in [a,b]$ the $L_p$ metrics extend naturally to the $L_p$ norms
- For $1 \leq p \leq \infty$ the $L_p([a,b])$ norm of a function $x(t)$ is:
$$
	||\vec{x}||_p = ||x(t)||_p = (\int_{a}^{b} |x(t)|^p dt)^{\frac{1}{p}}
$$
-  **The Space $L_p$** Def: The normed linear space $L_p([a,b])$ consists of all real or complex valued functions $x(t)$ on the interval $t \in [a,b]$ with $||\vec{x}||_p < \infty$