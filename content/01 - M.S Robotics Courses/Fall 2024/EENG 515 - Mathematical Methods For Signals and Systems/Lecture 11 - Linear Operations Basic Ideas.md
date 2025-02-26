## Overview

- **Vector Spaces**: 
	- Compare vectors - Metrics (Distance, Inner Product, Angles)
	- Size of Vectors - Norms, Induced norms
- **Projections onto Subspaces**:
	- Orthogonality
	- Projection Theorem
- Now we want to bring in the idea of "systems" operators and transformations that map vectors in some vector space to vectors in some other vector spaces
- In discussing operators we will generalize the ideas of projection and size of vectors:
	- **Projections**: Generalize to mappings between spaces
	- **Size of Vectors**: Generalizes the **operator norm** (gain) 
		- What is the largest ratio $\frac{||\vec{y}||}{||\vec{x}||}$
## Linear Operators

- **Linear Operators**: Suppose $X$ and $Y$ are vector spaces with a scalar field $R$. We say the operator $A:X\rightarrow Y$ is a **Linear operator** if :
$$
A(\alpha_1\vec{x_1}+\alpha_2\vec{x_2}) = A(\alpha_1\vec{x_1}) + A(\alpha_2\vec{x_2})
$$
- for all $\alpha_1,\alpha_2 \in R$ and $\vec{x_1},\vec{x_2} \in X$
- **Linear Functional** : When $Y = \mathbb{R}$ or $\mathbb{C}$ a linear operator $A:X\rightarrow Y$ is also known as a linear functional 

## Linear Operators: Matrix Case

- If $X = \mathbb{R}^n$ and $Y = \mathbb{R}^m$ any linear operator from $X$ to $Y$ can be represented as multiplication by an $m \times n$ matrix:
$$
\begin{bmatrix}
y_1 \\
y_2 \\
.\\
y_m
\end{bmatrix} = 

\begin{bmatrix}
a_{11} , a_{12}, ... ,a_{1n} \\
a_{21} , a_{22}, ... ,a_{2n} \\
..............\\
a_{m1} , a_{m2}, ... ,a_{mn}
\end{bmatrix}

\begin{bmatrix}
x_1 \\
x_2 \\
.\\
x_m
\end{bmatrix}
$$
- $\vec{y} = A \vec{x}$

## Operator Norms

- **Operator Norms** help us talk about the gain of a system
- **Operator Norms** : Let $X$ and $Y$ be normed linear spaces with corresponding norms $||*||_x$ and $||*||_y$ and suppose $A: X \rightarrow Y$ is a linear operator then the **Operator Norm** ($||A||$) is defined as
$$
||A|| := sup_{\vec{x}\in X, \vec{x} \neq \vec{0}}
 \frac{||A\vec{x}||_Y}{||\vec{x}||_X}$$
 - **Bounded Linear Operator**: A linear operator $A: X \rightarrow Y$ with operator norm $||A||$ is said to be bounded if $||A|| < \infty$
