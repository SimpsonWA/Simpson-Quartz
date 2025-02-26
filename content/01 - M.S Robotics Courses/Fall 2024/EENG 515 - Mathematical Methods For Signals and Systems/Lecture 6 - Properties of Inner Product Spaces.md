## Inner product spaces:

- Inner product is a function used to compare 2 vectors in a vector space
	- examples: angle between 2 vectors, orthonormal bases, orthogonal bases, etc
- **Inner Product**: An inner product $<*,*>$ on a vector space $S$ is a mapping $<*,*>: S \times S \rightarrow R$ with following properties
	- $<\vec{x},\vec{y}> = (<\vec{y},\vec{x}>)^*$ for all $\vec{x}$,$\vec{y} \in S$ (**Conjugate Symmetry**)
	- For any $\vec{x}$, $\vec{y}$,$\vec{z} \in S$ and any $a,b \in R$ (**Linearity**)
		- $<a\vec{x} + b\vec{y},\vec{z}> = a<\vec{x},\vec{z}> +b<\vec{y},\vec{z}>$
	- For any $\vec{x} \in S$ $<\vec{x},\vec{x}>$ is real valued an non-negative and $<\vec{x},\vec{x}> = 0$ if $\vec{x} = \vec{0}$
- **Inner Product Space**: An inner product space is a vector space $S$ together with a valid inner product $<*,*>:S \times S \rightarrow R$
- Standard inner product on $\mathbb{R}^n$ or $\mathbb{C}^n$ (dot product):
	- When $S=\mathbb{R}^n$ or $\mathbb{C}^n$ the standard inner product between 2 vectors $\vec{x},\vec{y} \in S$ is:
$$
<\vec{x},\vec{y}> = \sum_{i=1}^{n} x_yy_i^* = [y_1^*,y_2^*,...,y_n^*]\begin{bmatrix}
x_1 \\ 
x_2\\
...\\
x_n
\end{bmatrix}
$$

- **Standard inner product for Functions**: For real or complex calued functions on an interval $[a,b]$, the standard inner product is given:
$$
<\vec{x},\vec{y}> = \int_{a}^{b} x(t)y^{*}(t)dt
$$

- **Orthogonality**: 2 vectors $\vec{x}$ and $\vec{y}$ in an inner product space $S$ are said be orthogonal if $<\vec{x},\vec{y}> = 0$

## Induced Norm:

- Any valid inner product induces a valid norm by:
$$
||\vec{x}|| = \sqrt{<\vec{x},\vec{x}>}
$$
- or
$$
||\vec{x}||^2 = {<\vec{x},\vec{x}>}
$$
- These are induced norms
## Angles:

- **Angle in real inner product spaces**: The angle between 2 vectors $\vec{x}$ and $\vec{y}$ in a real inner product space is a number $\theta \in [0, \pi]$ given by:
$$
cos(\theta) = \frac{<\vec{x},\vec{y}>}{||\vec{x}|| ||\vec{y}||}
$$
	- Where $||*||$ is the induced norm in this inner product space
- **Angle in Complex Inner Product Spaces**: The angle between 2 vectors $\vec{x}$ and $\vec{y}$  in a complex inner product space (where $R=\mathbb{C}$) is a number $\theta \in [0, \frac{\pi}{2}]$ given by
$$
cos(\theta) = \frac{|<\vec{x},\vec{y}>|}{||\vec{x}|| ||\vec{y}||},
$$
	- Where $||*||$ is the induced norm in this linear product space

## Orthogonal Bases:

- **Orthogonal Bases**: A finite set of non-zero vectors $(\vec{v}_1,\vec{v}_2,...,\vec{v}_n)$ in an inner product space $S$ is said to form the orthogonal bases for $S$ if the following conditions are satisfied:
	- $<\vec{v}_k, \vec{v}_l> = 0$ for all $k \in l$
	- $span(\vec{v}_1,\vec{v}_2,...,\vec{v}_n) = S$

## Orthonormal Basis (Orthobasis):

- A orthogonal basis is Orthobasis if every basis vector $\vec{v}_k$ has a unit norm (i.e $||\vec{v}_k|| = 1$) according to the induced norm in the inner product space 
