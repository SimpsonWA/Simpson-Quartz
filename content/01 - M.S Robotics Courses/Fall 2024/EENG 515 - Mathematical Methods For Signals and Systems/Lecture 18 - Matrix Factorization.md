
## Overview:

- In problems its useful to factorize a matrix, writing it as a product of other matrices:
- **Factorizations**:
	- LU-Decomposition: Useful for solving $A\vec{x} = \vec{b}$ without computing $A^{-1}$
	- Cholesky Decomposition: useful for statistical signal processing, and kalman filtering
	- QR-Decomposition: Useful for least square problems

## LU Factorization:

- In LU factorization we write a square ($n \times n$) matrix $A$ as:
$$
A = LU \quad (1)
$$
- Where:
	- $L$: is the $(n \times n)$ and lower 1's on the diagonal 
	- $U$ is the $(n \times n)$ and upper Triangle
$$
L = \begin{bmatrix}
1 & 0 & 0 &0 \\
l_{21} &1 &0 &0\\
l_{31} &l_{32} &1 &0 \\
. & . & . & .\\
l_{n1} &l_{n2} &.... &1
\end{bmatrix} \quad (2)
$$
$$
U = \begin{bmatrix}
u_{11} & u_{12}  & u_{13} &... &u_{1n} \\
0 & u_{22} & u_{23} & ... &u_{2n}\\
0 & 0 & u_{33} & ... &u_{3n} \\
. & . & . & . & .\\
0 & 0 & 0 & ... &u_{nn}
\end{bmatrix} \quad (3)
$$
### LU Factorization: Solving Linear Equations:

- Suppose we want to solve $A\vec{x} = \vec{b}$ without computing $A^{-1}$ 
- If we know $A = LU$ then we can write:
$$
LU\vec{x} = \vec{b}
$$
- given $\vec{b}$ we want to solve $LU\vec{x} = \vec{b}$ for $\vec{x}$ 

- **Steps**:
	- Define the vector $\vec{y} = U \vec{x}$ in terms of the solution $\vec{x}$ we are looking for
	- Since $\vec{x}$ is unknown and so is $\vec{y}$ now $LU\vec{x} = \vec{b}$ becomes $L\vec{y} = \vec{b}$
	- We will first solve $L\vec{y} = \vec{b}$ for $\vec{y}$ 
	- Then we will solve for $U\vec{x} =\vec{y}$  for $\vec{x}$
- Solving for $L\vec{y}= \vec{b}$ for $\vec{y}$:
$$
\begin{bmatrix}
1 & 0 & 0 &0 \\
l_{21} &1 &0 &0\\
l_{31} &l_{32} &1 &0 \\
. & . & . & .\\
l_{n1} &l_{n2} &.... &1
\end{bmatrix} 
\begin{bmatrix}
y_1\\
y_2\\
y_3\\
.\\
y_n\\
\end{bmatrix} = 
\begin{bmatrix}
b_1\\
b_2\\
b_3\\
.\\
b_n\\
\end{bmatrix} \quad (4)
$$
	- So we can see that $y_1 = b_1$
	- and $y_2 = b_2 - l_{21}y_1$ and so on
	- in general we can see that: 
$$
y_j = b_j - \sum_{i=1}^{j-1} l_{ji}y_{i} \quad (5)
$$
- In total it requires about $\frac{n^2}{2}$ operations to find $y$

- After we know $\vec{y}$ we can solve for $U\vec{x} = \vec{y}$ to find $\vec{x}$ 
$$
\begin{bmatrix}
u_{11} & u_{12}  & u_{13} &... &u_{1n} \\
0 & u_{22} & u_{23} & ... &u_{2n}\\
0 & 0 & u_{33} & ... &u_{3n} \\
. & . & . & . & .\\
0 & 0 & 0 & ... &u_{nn}
\end{bmatrix} \begin{bmatrix}
x_1\\
x_2\\
x_3\\
.\\
x_n\\
\end{bmatrix} = 
\begin{bmatrix}
y_1\\
y_2\\
y_3\\
.\\
y_n\\
\end{bmatrix} \quad (6)
$$

## Cholesky Factorization:

- **Positive Definite Matrix**: Let $A$ be a square $(n \times n )$ Hermitian symmetric matrix. We say that $A$ is positive definite if:
$$
\vec{x}^{H} A \vec{x} > 0 \quad (7)
$$
	- Holds for all nonzero $\vec{x} \in \mathbb{R}^n$ (or $\mathbb{C}^n$)
- In Cholesky factorization we can write a square $(n \times n)$ Hermitian symmetric positive definite matrix $A$ as:
$$
A = LL^{H} \quad (8)
$$
- Where $L$ is $(n\times n)$ and lower triangle with positive entries on the diagonal 

#### Cholesky Factorization: Solving Linear Equations

- Can use Cholesky factorization to solve for $A\vec{x} = \vec{b}$ without computing $A^{-1}$ 
- Write $A\vec{x} = LL^{h}\vec{x} = \vec{b}$ Given $\vec{b}$ we want to solve $LL^{h}\vec{x} = \vec{b}$ for $\vec{x}$ :
##### Steps
- Define a Vector:
$$
\vec{y} = L^{H}\vec{x} \quad (9)
$$
- in terms of $\vec{x}$ we are looking for
- since $\vec{x}$ is unknown, so is $\vec{y}$ 
- We can 1st solve for $L\vec{y} = \vec{b}$ for $\vec{y}$
- Then we can solve for $L^{H}\vec{x} = \vec{y}$ for $\vec{x}$

## QR Factorization:

- **Unitary matrix**: let $Q$ be a square $(n\times n)$ matrix. We say $Q$ is unitary (or orthogonal) if:
$$
Q^{H}Q = I_{n\times n} \quad(10)
$$
### Properties of Unitary Matrices:

- A square ($n \times n$) matrix is unitary if and only if all of its columns are orthonormal. Similarly a square matrix is unitary if and only if all of its rows are orthonormal 
- If $Q$ is unitary, it also follows that $QQ^{H} = I$ and $Q^{-1} = Q^{H}$ 
- **Isometric Property**: an $n \times n$ matrix $Q$ is unitary if and only if:
$$
||Q\vec{x}||_{2}  = \sqrt{\vec{x}^H Q^H Q \vec{x}} = \sqrt{\vec{x}^H \vec{x}} = ||\vec{x}||_2 \quad (11)
$$
- $(11)$ for all $\vec{x} \in \mathbb{R}^n$ or $\mathbb{C}^n$
- $(11)$: Therefore if $Q$ is unitary we will have:
$$
||Q||_2 = 1 \quad ||Q^{-1}||_2 = 1 \quad (12)
$$
- $(12)$ and so:
$$
\kappa_{2}(Q) = 1 \quad (13)
$$

- In QR Decomposition we can write an $m \times n$ matrix $A$ as:
$$
A = QR \quad (14)
$$
- Where:
	- $Q$ is unitary and $m \times n$
	- $R$ is upper triangle and $m \times n$  

