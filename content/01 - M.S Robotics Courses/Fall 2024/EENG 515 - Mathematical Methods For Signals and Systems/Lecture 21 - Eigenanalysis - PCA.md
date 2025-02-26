
# Application: Principle Component Analysis (PCA):

- Principle component analysis is a standard technique for dimensionality reduction for data sets that have a low-dimensional structure

## Karhunen-Loeve (KL) Transform:

- Consider a random vector $\vec{x} \in \mathbb{R}^n$ with known covarience matrix $R$.
$$
R = \begin{bmatrix} 
\vec{x} ... \vec{x}^T
\end{bmatrix} = 
\begin{bmatrix}
Ex_{1}^{2} & Ex_1x_{2}  & ...  & Ex_{1}x_{n} \\ 
Ex_{2}x_{1} & Ex_2x_{2}  & ...  & Ex_{2}x_{n} \\ 
.... & .... & ... & ... &  \\ 
Ex_{n}x_{1} & Ex_nx_{2}  & ...  & Ex_{n}^2 \\ 
\end{bmatrix}
$$
- Where $E[*]$ means expectation
- We will assume $\vec{x}$ is zero-mean aka:
$$
E[\vec{x}] = \begin{bmatrix} Ex_{1} \\ ... \\ Ex_n\end{bmatrix} = \vec{0}
$$
- The goal of the KL transform is to construct a matrix k such that:
	- K is square ($n \times n$)
	- K has rank r. For some prescribed integer $r<n$ and
	- When we multiply k by typical realizations of the random vector $\vec{x}$ the result $x' = k\vec{x}$ is an accurate assessment of $\vec{x}$ itself
- k should act as a projection onto an r-dimensional subspace where most realizations of $\vec{x}$ will live.
![[Pasted image 20240927191400.png]]

- The value of doing this is that $\vec{x}'$ can be described using only r numbers and so we can view $\vec{x}'$ as a compressed version of $\vec{x}$
- To choose k given R suppose we want to minimize the expected squared error:
$$
e^{2}(k)= E[||\vec{x} - k \vec{x}||_{2}^{2}]
$$
$$
= E[||(I-K) \vec{x}||_{2}^{2}]
$$
$$
= trace[(I-k)R(I-K)^T]
$$
- since $k$ is rank $r$, real, and symmetric then:
$$
k = UM_rU^T
$$
- Where:
![[Pasted image 20240927191853.png]]

