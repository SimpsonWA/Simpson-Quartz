
- **Range space**: let $A:X\rightarrow Y$ be a linear operator between 2 vector spaces $X$ and $Y$, the **Range** or **range space** of $A$ (denoted $\cal{R}(A)$) is:
$$
\cal{R}(A):=\{\vec{y} \in Y: A\vec{x}=\vec{y} \quad for \ some \ \vec{x}\in X\}
$$
- the range space is a linear subspace of $Y$

- **Null space**: let $A:X\rightarrow Y$ be a linear operator between 2 vector spaces $X$ and $Y$. The **Null Space** or **Null** denoted $\cal{N}(A)$ is:
$$
\cal{N}(A):=\{\vec{x} \in X: A\vec{x}=\vec{0} \in Y\}
$$
- the null space is a linear subspace of $X$

- When $X$ and $Y$ are inner product spaces we can talk about the **Range Space** of $A^{*}$ (which is the linear subspace of $X$) and the **Null Space** of $A^{*}$(which is a linear subspace of $Y$). We then have **4 Fundamental Subspaces of a Linear Operator**:
$$
	\begin{align*}
	\cal{R}(A) := \{\vec{y} \in Y: A\vec{x}=\vec{y} \quad for \ some \ \vec{x}\in X\} \\
	\cal{N}(A):=\{\vec{x} \in X: A\vec{x}=\vec{0} \in Y\} \\
	\cal{R}(A^{*}):=\{\vec{x} \in X: A^{*}\vec{y}=\vec{x} \quad for \ some \ \vec{y}\in Y\} \\
	\cal{N}(A^{*}):=\{\vec{y} \in Y: A^{*}\vec{x}=\vec{0} \in Y\}
	\end{align*}
$$
![[Pasted image 20240907105207.png]]

## Fundamental Subspaces: Matrix Case

- Again consider a case where $X = \mathbb{R}^n$ and $Y = \mathbb{R}^m$ recall $A:X\rightarrow Y$ can be represented as multiplication by an $m \times n$ matrix
- When $A$ is a matrix $\cal{R}(A)$ is just the span of columns of $A$ and $\cal{R}(A^{*})$ is just the span of rows of $A$
$$
\begin{align}
\cal{R}(A) = colspan(A) \\
\cal{R}(A^*) = rowspan(A)
\end{align}
$$
**Matrix Rank**: The **Rank** of a matrix equals the dimension of its column span and the dimension of its row span:
$$
rank(A) = dim(\cal{R}(A)) = dim(\cal{R}(A^{*}))
$$
- We say that $A$ is
	- **Full Rank**: if $rank(A) = min\{m,n\}$
	- **Rank Deficient** if it is not full rank
- The rank of A relates to the dimensions of its four fundamental subspaces:
	- $dim(\cal{R}(A)) = rank(A) = dim(colspan(A))$
	- $dim(\cal{N}(A)) = n- rank(A)$
	- $dim(\cal{R}(A^*)) = rank(A) = dim(rowspan(A))$
	- $dim(\cal{N}(A^*)) = m - rank(A)$
- Note for any $m \times n$ matrix A:
	- $dim(\cal{R}(A)) + dim(\cal{N}(A)) = n =$ number of columns of $A$
	- $dim(\cal{R}(A^*)) + dim(\cal{N}(A^*)) = m =$ number of rows of $A$
	- $dim(\cal{R}(A)) + dim(\cal{N}(A^*)) = m =$ number of rows of $A$
	- $dim(\cal{R}(A^*)) + dim(\cal{N}(A)) = n =$ number of columns of $A$
- Additionally for 2 matrices $A$ and $B$:
	- $rank(AB) \leq min\{rank(A),rank(B)\}$
	- $rank(A+B) \leq rank(A) + rank(B)$
## Projection Operators

- A linear operator $P:X\rightarrow X$ from a vector space $X$ into itself is called a **projection operator** or **idempotent** if:
$$
P^2 = P
$$
- **Orthogonal Projection**: a projection operator $P$ in an inner product space $X$ is called **orthogonal projection** if $\cal{R}(P) \perp \cal{N}(P)$ (i.e if $<\vec{x},\vec{y}> =0$ for all $\vec{x}\in \cal{R}(P)$ or $\vec{x}\in \cal{N}(P)$)
- A bounded linear operator $P: X\rightarrow X$ on an inner product space $X$ is an orthogonal projection if 
	- P is **Idempotent** $P^2 =P$
	- P is **Self-adjoint** $P = P^*$
- as mentioned before, the minimizing vector $\vec{x}'$ is referred to as the orthogonal projection of $\vec{x}$ onto $T$
	- in other words $\vec{x}' = P \vec{x}$ where P is an orthogonal projection operator with $\cal{R}(P) = T$

## Projection operators: Matrix Case

- Consider $X = \mathbb{R}^n \ or \ \mathbb{C}^n$ and $P:X\rightarrow X$ can be represented as multiplication by an $n \times n$ matrix then:
	- an $n \times n$ matrix $P$ is a projection if $P^2 = P$
	- an $n \times n$ matrix $P$ is an **orthogonal projection** if $P^2 = P$ and $P^{H} = P$
- There is a recipe for construction projection matrices in $X = \mathbb{R}^n \ or \ \mathbb{C}^n$. Consider a set of $m$ linearly independent vectors $\vec{v}_1,\vec{v}_2,...,\vec{v}_n \in \mathbb{R}^n \ or \ \mathbb{C}^n$ 
- We can construct an orthogonal projection matrix $P$ onto the subspace of T which spans the vectors as follows:
	- Construct an $n \times n$ matrix where $colspan(A) = T$
$$
A = [\vec{v_1} \vec{v_2} .... \vec{v_n}]
$$
	- Let:
$$
P = A(A^{H}A)^{-1}
A^{H}$$

![[Pasted image 20240907143809.png]]


