
- **Best approximation to a vector**:
	- For an orthonormal collection of vectors $\vec{v_1},\vec{v_2},...,\vec{v_n}$ in an inner product space $S$ and an arbitrary vector $\vec{x} \in S$ , the best approximation $\vec{x}'$ to $\vec{x}$ among all vectors in $T = span\{\vec{v_1},\vec{v_2},...,\vec{v_n}\}$ is given by:
$$
\vec{x}' = \sum_{k=1}^{n} <\vec{x},\vec{v_k}>\vec{v_k}
$$
- For an **expansion** we want to consider a case where $\vec{v_1},\vec{v_2},...,\vec{v_n}$ form an orthonormal basis for the *entire* space $S$:
	- In this case $\vec{x}' = \vec{x}$ so:
$$
\vec{x} = \sum_{k=1}^{n} <\vec{x},\vec{v_k}>\vec{v_k}
$$
- Notice that $\vec{x}$ is on both sides of this equation so it is know as a **Reproducing Vector**

- If $S$ is infinite-dimensional and we have a infinite sequence of orthonormal vectors $\vec{v_1},\vec{v_2},...,\vec{v_n}$ that form a basis of $S$ as long as 
$$
\sum_{k=1}^{\infty} |<\vec{x},\vec{v_k}>|^2 < \infty
$$
- we can also write
$$
\vec{x} = \sum_{k=1}^{\infty} <\vec{x},\vec{v_k}> \vec{k}
$$
- Where the **transform coefficients** are $<\vec{x},\vec{v_1}>,<\vec{x},\vec{v_2}>,....$


## Perseval's Theorem 

### Setup:
- $S$ is a finite-dimensional inner product space we denote the inner product of $S$ by $<*,*>_s$ 
- Suppose $\vec{v_1},\vec{v_2},...,\vec{v_n}$ form an orthonormal basis for s
- Suppose that $\vec{x}$ and $\vec{y}$ are 2 arbitrary vectors in $S$ and denote their transform coefficients as 
$$
\alpha_k = <\vec{x},\vec{v_k}>_s \quad and \quad  \beta = <\vec{y},\vec{v_k}>_2 \quad for \ k = 1,2,....,  n
$$
- Let $\vec{\alpha}$ and $\vec{\beta}$ denote vectors by:
$$
\vec{\alpha} = \begin{bmatrix}
\alpha_1 \\
\alpha_2 \\
.\\
\alpha_n
\end{bmatrix} \quad and \quad 
\vec{\beta} = \begin{bmatrix}
\beta_1 \\
\beta_2 \\
.\\
\beta_n
\end{bmatrix}
$$
- **Perseval's Theorem**: 
$$
<\vec{x},\vec{y}>_s = \sum_{k=1}^{n} \alpha_k\beta_k^{*} = <\vec{\alpha},\vec{\beta}>_{l2}
$$
- **Properties**
	- By taking $\vec{x} = \vec{y}$ thus $\vec{\beta}  =\vec{\alpha}$ we obtain 
$$
	||\vec{x}||_{s}^2 = ||\vec{\alpha}||_{l2}^2
$$
	- the vectors $\vec{x}$ and $\vec{y}$ are orthogonal in $S$ if $\vec{\alpha}$ and $\vec{\beta}$ are orthogonal in $l_2$

## Truncating and quantizing Orthobasis expansions

- **Truncating**: One common type of manipulation involves transforming a signal to some domain, setting some coefficients to zero, and inverting the transform.
- **Quantizing**: Another common type of manipulation involves transforming a signal to some domain and then quantizing the transform coefficients so they can be encoded in binary.