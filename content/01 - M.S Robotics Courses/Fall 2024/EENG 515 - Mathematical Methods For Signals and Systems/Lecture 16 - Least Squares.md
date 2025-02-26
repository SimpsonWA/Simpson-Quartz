
## Least - Square Problems:

- In cases where no solution exists to the equation $A\vec{x} = \vec{y}$ we may want to find the best approximation solution $\vec{x}' \in X=\mathbb{R}^n$ or $\mathbb{C}^n$
- In general there maybe more than one vector $\vec{x}'$ that solves the normal equations and that minimizes $||\vec{y}-A\vec{x}||_2$
- However they all give the same approximation in the $Y$: We know that there is a unique vector $\vec{y}' \in colspan(A)$ such that $(y-y')\perp colspan(A)$ using the standard inner product and this vector $\vec{y}'$ is the unique minimizer of:
	- $min_{\vec{y'} \in colspan(A)} \quad ||\vec{y}-\vec{y'}||_2$ 
![[Pasted image 20240911170629.png]]

- If the columns of A are linearly independent, then $A^H A$ will be invertible, and the solution to the normal equations will be
	- $\vec{x}' = (A^H A)^{-1}A^H\vec{y} =  A^+\vec{y}$
- If the columns of A are linearly dependent then $A^H A$ will not be invertible and the solution having the smallest $l_2$ norm will be given by:
	- $\vec{x}' = A^{+}\vec{y}$
	- Although: $A^{+} \neq (A^H A)^{-1}A^H$
- We will have $\vec{y}' = A\vec{x}' = AA^{+}\vec{y}$ which is the orthogonal projection of $\vec{y}$ onto the column span of $A$

## Least Square Problems: Weighted Least Squares

- Suppose we use a weighted inner product on the space $Y = \mathbb{R}^m$. Specifically consider
	- $<\vec{v},\vec{z}>_W := \vec{z}^H W \vec{v} = \sum_{m}^{i=1} w_i v_i z^{*}_i$
	- $W = diag(w_1,w_2,....,w_m)$
- and each $w_i > 0$ using this inner product the induced norm becomes:
	- $||\vec{z}||^2_W = <\vec{z},\vec{z}>_W = \vec{z}^H W \vec{z} = \sum_{m}^{i=1} w_i |z_i|^2$
- Now consider the corresponding weighted least square problem. Given $\vec{y} \in Y$ how can we find $\vec{x}' \in X$ such that:
	- $||\vec{y}-A\vec{x}'||_W$
	- Is as small as possible?
- We can solve this as any minimizer $\vec{x}'$ must satisfy the normal equations:
$$
\begin{bmatrix}
<a_1,a_1>_W \ <a_2,a_1>_W \ .... \ <a_n,a_1>_W \\
<a_1,a_2>_W \ <a_2,a_2>_W \ .... \ <a_n,a_2>_W \\
..... \ ...... \ .... \ ....... \\
<a_1,a_m>_W \ <a_2,a_m>_W \ .... \ <a_n,a_m>_W \\
\end{bmatrix}
\begin{bmatrix}
x'_1\\
x'_2\\
...\\
x'_n
\end{bmatrix} = 
\begin{bmatrix}
<\vec{y},\vec{a_1}>_W \\
<\vec{y},\vec{a_2}>_W \\
...\\
<\vec{y},\vec{a_n}>_W \\
\end{bmatrix}
$$
- or equivalently
	- $A^H W A \vec{x}' = A^H W \vec{y}$
- if the columns of $A$ are linearly indpendent the $A^H W A$ will be invertible and the unique solution of the normal equation will be
	- $\vec{x}' = (A^H WA)^{-1} A^H W \vec{y}$

## Least square problems linear regression

- Problem we want to solve:
	- Suppose we observe $m$ data points $(t_1,f_1),(t_2,f_2),...,(t_m,f_m) \in \mathbb{R}^2 \ or  \ \mathbb{C}^2$ We would like to estimate a slope $a\in \mathbb{R}  \ or \ \mathbb{C}$ can an intercept $b\in \mathbb{R}  \ or \ \mathbb{C}$ such that:
		- $f_i = at_i + b$
	- For all $i=1,2,...,m$. Suppose we choose a least squares error metric. Then we want to solve:
		- $min_{a,b} \sum_{i=1}^{m} |f_i - (at_i +b)^2|$
	- We can pose this as a matrix form:
		- $\vec{f} = \begin{bmatrix} f_1 \\ f_2 \\ ... \\ f_m \end{bmatrix}$, $A = \begin{bmatrix} t_1 \ 1 \\ t_2 \ 1 \\ ... \\ t_m \ 1 \end{bmatrix}$, and $\vec{c} = \begin{bmatrix} a \\ b \end{bmatrix}$
	- The columns of $A$ are linearly independent, unless the $t_i$ are all equal
	- Now finding a new $a$ and $b$ can be expressed as:
		- $min_{\vec{c}} ||\vec{f}-A\vec{c}||_2^2$
	- Assume the $t_i$ not all equal the optimal solution is given by 
		- $\vec{c}' = (A^H A)^-1 A^H \vec{f}$
	- What if instead we had confidence in certain points
		- We can solve a weighted least square problem:
			- $min_{a,b} \sum_{m}^{i=1} w_i |f_i - (at_i + b)|^2$
		- Where weights $w_i$ are larger the more confident we are with $f_i$
	- If $t_i$ not all equal the optimal solution is:
		- $\vec{c}' = (A^H W A)^-1 A^H W \vec{f}$
	- Where $W$ is:
		- $W = diag(w_1,w_2,...,w_m)$

## Least Square problems: Other Lp norms

- So far we only focused on $l_2$ norms
- But what about the other $l_p$ norms
- We can solve other $l_p$ norms by using the **iterative reweighted least squares** (IRLS) algorithm:
- **Setup**:
	- Suppose $A$ is a real valued $m \times n$ matrix when $m \geq n$ and suppose the columns of $A$ are linearly independent. Let $\vec{y} \in \mathbb{R}^m$. Let $p \in [1,\infty)$ with $p \neq 2$. Then we want to solve:
		- $min_{\vec{x}\in \mathbb{R}^n} ||\vec{y}-A\vec{x}||_p$
	- it follows that this has the same minimizer $\vec{x}'$ as the weighted problem:
		- $min_{\vec{x} \in \mathbb{R}^n} \sum_{m}^{i=1} w'_i |y_i - (A\vec{x})_i|^{2}$ 
	- Where the weights are given by:
		- $w'_i = |y_i - (A\vec{x})_i|^{p-2}$
	- If we have the weights the optimal solution $\vec{x}'$ is given by:
		- $\vec{x}' = (A^H W' A)^{-1}A^H W' \vec{y}$
![[Pasted image 20240912163537.png]]
