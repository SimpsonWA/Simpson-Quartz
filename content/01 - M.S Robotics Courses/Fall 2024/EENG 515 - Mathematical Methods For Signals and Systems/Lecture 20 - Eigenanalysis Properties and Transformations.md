
- **Theorem (Eigenvectors corresponding to distinct eigenvalues)**: Eigenvectors corresponding to distinct eigenvalues are linearly independent
## Diagonalization:

- If $A$ is an $(n \times n)$ matrix that happens to have $n$ linearly independent eigenvectors, then it can be written (or diagonalized) as:

$$
A=T \Lambda T^{-1} \quad (1)
$$
- $(1)$ Where $T$ is an $n \times n$ invertible matrix, containing the eigenvectors of $A$
- $(1)$ $\Lambda$ is a $n \times n$ diagonal matrix containing the eigenvalues of $A$

## Understanding and applying the operator A:

- Let $\vec{x} \in \mathbb{C}^n$ then:
$$
A\vec{x} = T \Lambda T^{-1} \vec{x} \quad (2)
$$\
- **1st**: $(2)$ Let $\vec{x} = \alpha_1 \vec{v_1} + \alpha_2 \vec{v_2} + ... \alpha_n \vec{v_n}$ for some coefficients $\alpha_1 , \alpha_2,...,\alpha_n$ 
- **1st**:$(2)$ Then we can write $\vec{x} = T \vec{\alpha}$ where:
$$
\vec{\alpha} = \begin{bmatrix} \alpha_1 \\...\\ \alpha_n \end{bmatrix} \in \mathbb{C}^n \quad (3)
$$
- **1st**: $(3)$ since $T$ is invertible $\vec{\alpha}$ must satisfy:
$$
\vec{\alpha} = T^{-1}\vec{x} \quad (4)
$$
- **1st**: $(4)$ Thus $T^{-1}\vec{x}$ computes the expansion Coefficients needed to express $\vec{x}$ in terms of eigenvectors of $A$
- **2nd**: Note that in the expression $(2)$ the portion:
$$
\Lambda T^{-1} \vec{x} = \Lambda \vec{\alpha} = \begin{bmatrix} \lambda_1 \alpha_1 \\ ...\\ \lambda_n \alpha_n \end{bmatrix} \quad (5)
$$
- **3rd** Thus:
$$
A\vec{x} = T\Lambda T^{-1}\vec{x} = 
\begin{bmatrix}
\vec{v_1} \ \vec{v_2} \ ... \ \vec{v_n} 
\end{bmatrix}
\begin{bmatrix}
\lambda_1 \alpha_1 \\
...\\ 
\lambda_n \alpha_n 
\end{bmatrix} \quad (6)
$$
- **3rd**: Rebuilds a signal as a linear combination of eigenvectors, but now each expansion has been scaled by the corresponding eigenvalue of $A$ 

- Thus diagonalization can be summarized in 3 steps:
1. Transform (Find the $\alpha_i$'s)
2. Multiply (Scale the $\alpha_i$'s by the $\lambda_i$'s)
3. Inverse Transform (Rebuild using $\vec{v_i}$'s)

## Diagonalizations of Self-Adjoint Matrices

- **Lemma** (Eigenvalues of self Adjoint matrix): If $A = A^{H}$ then all eigenvalues of $A$ are real valued (even if $A$ itself has complex entries)
- **Lemma** (Eigenvectors of self Adjoint matrix): If $A = A^{H}$ then there exists a set of $n$ orthonormal eigenvectors $\vec{v_1} \ \vec{v_2} \ ... \ \vec{v_n}$ such that:
$$
A\vec{v_i} = \lambda_i \vec{v_i} \quad (7)
$$
- $(7)$: for all $i = 1,2,...,n$

## Positive Definite Matrices: Definition

- Let $A$ be a square $n \times n$ Hermitian matrix such that $A = A^H$
- Recall that we say $A$ is positive definite if:
$$
\vec{x}^H A \vec{x} > 0 \quad (8)
$$
- $(8)$ holds for all non-zero $\vec{x} \in \mathbb{R}^n$ or $\mathbb{C}^n$
- Similarly we say that $A$ is **positive semi-definite** if 
$$
\vec{x}^H A \vec{x} \geq 0 \quad (9)
$$
- $(9)$ hold for all non-zero $\vec{x} \in \mathbb{R}^n$ or $\mathbb{C}^n$

## Positive Definite Matrices: Eigenvalues:

- If $A = A^H$ we already know the eigenvalues of $A$ are real
- If $A$ is positive definite then all eigenvalues of $A$ are positive
- If $A$ is positive semi-definite then all eigenvalues of $A$ are non-negative
