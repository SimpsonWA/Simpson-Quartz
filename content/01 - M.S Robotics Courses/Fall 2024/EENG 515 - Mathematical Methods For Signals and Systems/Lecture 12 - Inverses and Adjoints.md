
## Inverse Operators

- A linear operator $A: X \rightarrow Y$ between 2 vector spaces $X$ and $Y$ is said to be **invertible** if there exists an operator $A^{-1}: Y \rightarrow X$ such that **(1)** and **(2)** are true:
$$
AA^{-1} = I \quad i.e: \quad AA^{-1}\vec{y} = \vec{y} \quad for \ all\ \vec{y}\in Y \quad (1)
$$
$$
A^{-1}A = I \quad i.e: \quad A^{-1}A \vec{x} = \vec{x} \ for \ all\ \vec{x}\in X
$$
- $A^{-1}$ is the inverse of $A$
- **Lemma**: if $A$ is an invertible linear operator $A^{-1}$ is a linear operator
- **Invertibility** is a topic of interest where we want to identify the "input" of a system from the "output" of that system
	- EG: Given $A$ and $\vec{y}$ find $\vec{x}$ such that $A\vec{x} =\vec{y}$

## Inverse Operators: Matrix Case

- Restricted to $X = \mathbb{R}^n \ or \ \mathbb{C}^n$ and $Y = \mathbb{R}^m \ or \ \mathbb{C}^m$ 
- An $m\times n$ matrix $A$ cannot be invertible only $n \times n$ square matrices of $A$ are invertible
	- Though not all $n \times n$ matrices are invertible
- **Nonsingular** matrix: an invertible matrix
- If $A$ is a square (say, $n \times n$) matrix, then the following statements are all equivalent (note that some of these concepts will be defined later):
	- $A$ is invertible
	- $A$ is nonsingular
	- $det(A) \neq 0$
	- $A\vec{x} = \vec{0} \ if \ \vec{x} = \vec{0}$
	- The rows of A are linearly independent
	- The columns of A are linearly independent
	- $dim(\cal{N}(A)) = 0$ which means $\cal{N}(A) = \{\vec{0}\}$  
	- $dim(\cal{R}(A)) = n$
	- $rank(A) = n$
	- A is full rank
	- all eigenvalues of A are non-zero
	- The matrix $A^{H}A$ is positive definite
	- $A^{H}$ is invertible
- **Schur Complement of A**:
$$
S = A_{22} - A_{21}A^{-1}_{11}A_{12}
$$
## Adjoint Operators

- **Adjoint Operator**: Let $A:X\rightarrow Y$ be a bounded linear operator between 2 inner product spaces $X$ and $Y$. The **Adjoint** of $A$, denoted $A^{*}: Y \rightarrow X$ is the unique operator such that:
$$
<A\vec{x},\vec{y}>_Y = <\vec{x},A^{*}\vec{y}>_X \quad for \ all \ \vec{x}\in X \ and \ \vec{y}\in Y
$$
- **Self-Adjoint**: The operator $A:X \rightarrow X$ is said to be self-Adjoint if $A = A^{*}$
- **Lemma**: If $A$ is a bounded linear operator with Adjoint $A^{*}$ then $A^{*}$ is itself bounded linear operator and :
$$
||A^{*}|| = ||A||
$$
- **Lemma**: if $A$ is a bounded linear operator with Adjoint $A^{*}$ then $(A^{*})^{*} = A$
- **Lemma**: if $A$ is an invertible linear operator with adjoint and bounded inverse $A^{-1}$ then 
$$
(A^{-1})^{*} = (A^{*})^{-1}
$$
- **Theorem**: Let $A:X\rightarrow Y$ be a bounded linear operator between 2 inner product spaces $X$ and $Y$. Then for a fixed $\vec{y}\in Y$ the vector $\vec{x} \in X$ is a minimizer $||\vec{y}-A\vec{x}||_Y$ if:
$$
A^{*}A\vec{x} = A^{*}\vec{y}
$$
	- if $A^{*}A$ is invertible then the unique minimizer is given by:
$$
\vec{x} = (A^{*}A)^{-1}A^{*}\vec{y}
$$
## Adjoint Operators: Matrix Case

- In the case of $X = \mathbb{R}^n$ and $Y = \mathbb{R}^m$ recall $A:X\rightarrow Y$ can be represented as multiplication by an $m \times n$ matrix
### What is the Adjoint of a matrix?:

- Using the standard inner product of $X$ and $Y$ the Adjoint of $A$ is the unique operator such that 
$$
\vec{y}^{H}A\vec{x} = <A\vec{x},\vec{y}> = <\vec{x},A^{*}\vec{y}> = \vec{y}^{H}(A^{*})^{H}\vec{x}
$$
- for all $\vec{x}$ and $\vec{y}$
- **Self adjoining matrix operators**:
	- $A = A^{H}$
	- Symmetic if real
	- Conjugate symmetry if complex 
	- Herman if Complex
- **Theorem**: let $A$ be a real valued $m \times n$ matrix for a fixed $\vec{y} \in \mathbb{R}^m$, the vector $\vec{x} \in \mathbb{R}^n$ is a minimizer of $||\vec{y}-A\vec{x}||_2$ if
$$
A^{H}A\vec{x} = A^{H}\vec{y}
$$
- if $A^{H}A$ is invertible, then the unique minimizer of  $||\vec{y}-A\vec{x}||_2$  is given by 
$$
\vec{x} = (A^{H}A)^{-1}A^{H}\vec{y}
$$
- where $(A^{H}A)^{-1}A^{H}$ is the pseudoinverse
