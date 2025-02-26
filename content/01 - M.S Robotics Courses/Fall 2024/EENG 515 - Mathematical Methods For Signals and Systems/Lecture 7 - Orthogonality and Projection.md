
## The Orthogonality Principle (Formulation)

- Let $S$ be an inner product space and let $T$ be a subspace of $S$
	- Our goal is to answer: Given some $\vec{x} \in S$ what is the closest point to $\vec{x}$ in $T$ ?
	- Another way to put it: We want to find $\vec{x} \in T$ that minimizes $||\vec{x} - \vec{x'}||$ using the norm induced by the inner product on $S$
- The **Projection Theorem** tells us something about the minimizer $\vec{x'}$ namely:
	- **The error between the minimizer and $\vec{x}$ is orthogonal to $T$**
- **Theorem (Projection Theorem)**: 
	- Suppose $S$ is an inner product space and suppose $T$ is a linear subspace of $S$
	- For a given vector $\vec{x} \in S$ there is a unique vector $\vec{x'} \in T$ such that:
$$
	||\vec{x} - \vec{x'}|| \leq ||\vec{x} - \vec{z}|| \quad for \ all \ \vec{z} \in T 
$$

- 
	- Furthermore a vector $\vec{x'} \in T$ is the minimizer (the closest vector in $T$ to $\vec{x}$ ) if:
$$
	 \vec{x} - \vec{x'} \perp T
$$
	- i.e: $\vec{x} - \vec{x'},\vec{y} = 0$ for all $\vec{y} \in T$
- the minimizing vector $\vec{x'}$ is the **orthogonal projection** of $\vec{x}$ onto $T$

- Orthogonal Projection of $\vec{x}$ onto $\vec{v}$
## Approximation in a Subspace (General Case)

- Problem: 
	- Let $\vec{v_1},\vec{v_2},....,\vec{v_n}$ be a finite collection of vectors in an inner product space $S$ and suppose $T = span\{\vec{v_1},\vec{v_2},...,\vec{v_n}\}$. Given an arbitrary vector $\vec{x} \in S$, how can we compare its best approximation $\vec{x'}$ in $T$?
- The goal is to obtain the scalar coefficients $a_1,a_2,....,a_n \in R$ such that
$$
\vec{x'} = \sum_{k=1}^{n} a_k \vec{v_k}
$$
	- Minimizes $||\vec{x} - \vec{x'}||$
- We know from the projection theorem that $\vec{x} - \vec{x'} \perp span{\vec{v_1},\vec{v_2},...,\vec{v_n}}$ there for:
$$
<\vec{x}-\vec{x'},\vec{v_l}> = 0 \quad for \ all \ l=1,2,...,n
$$
- this means we require:
$$
<\vec{x} - \sum_{k=1}^{n} a_k \vec{v_k}, \vec{v_l}> = 0 \quad for \ all \ l=1,2,...,n
$$
 - Since $<\vec{x}-\vec{x'},\vec{v_l}> = 0$ then $<\vec{x},\vec{v_l}> = <\vec{x'},\vec{v_l}>$ or 
$$
<\vec{x}',\vec{v_l}> = <\vec{x},\vec{v_l}> = \sum_{k=1}^{n} a_k <\vec{v_k},\vec{v_l}>
$$
- We can set this up as a matrix defined as:
$$
\begin{bmatrix}
<\vec{v_1},\vec{v_1}> <\vec{v_2},\vec{v_1}> ..... <\vec{v_m},\vec{v_1}> \\
<\vec{v_1},\vec{v_2}> <\vec{v_2},\vec{v_2}> ..... <\vec{v_m},\vec{v_2}> \\
...................................\\
<\vec{v_1},\vec{v_m}> <\vec{v_2},\vec{v_m}> .... <\vec{v_m},\vec{v_m}>
\end{bmatrix}
\begin{bmatrix}
a_1 \\
a_2 \\
.\\
a_m
\end{bmatrix} = 
\begin{bmatrix}
<\vec{x},\vec{v_1}>\\
<\vec{x},\vec{v_2}>\\
.\\
<\vec{x},\vec{v_m}>
\end{bmatrix}
$$
$$
G \vec{a} = \vec{b}
$$
- Where G is called the **Grammian** or **Gram** matrix 
- Note: $G = G^H$
- If $G$ is invertible (if $\vec{v_1},\vec{v_2},...,\vec{v_n}$ are linearly independent)
$$
\vec{a} = G^{-1} \vec{b}
$$
