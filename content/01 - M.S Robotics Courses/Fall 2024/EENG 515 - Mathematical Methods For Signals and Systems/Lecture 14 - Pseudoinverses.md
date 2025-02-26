
## **Left and Right Inverses**:

- **Left Inverse**: A matrix A has a left inverse if $\exists B  \ni BA = I$ (there exists a B such that BA = I)
- **Right Inverse**: A matrix A has a right inverse if $\exists C \ni AC = I$ (there exists a C such that AC = I)
- **Inverse**: A square matrix A has an inverse if $\exists A^{-1} \ni A^{-1}A = AA^{-1} = I$

- Properties:
	- If $A$ has a `left inverse` $B$ then $A\vec{x} = \vec{y}$ has a solution $\vec{x} = B \vec{y}$
	- If $A$ has a `right inverse` $C$ then $A \vec{x} =\vec{y}$ has a solution $\vec{x}=C\vec{y}$

- Suppose $A \in \mathbb{R}^{m \times n}$ and consider $A\vec{x}=\vec{y}$:
	- **Existence**: if $rank(A)=r=m\leq n$ (columns of $A$ span $\mathbb{R}^m$), then:
		- There exists a right inverse $C$, typically of form $C = A^{T}(AA^T)^{-1}$
		- For any $\vec{x}\in \mathbb{R}^m$, there exists at least on solution $\vec{x} = C\vec{y}$
		- A solution exists only if $\vec{y} \in \cal{R}(A)$, which implies $\vec{y} \perp \cal{N}(A^*)$ : these points are called the **Fredholm alternative Theorem**
	- **Uniqueness**: if $rank(A)=r=n\leq m$ (columns of $A$ are linearly independent), then:
		- There exists a left inverse $B$, typically of the form $B = (A^TA)^{-1}A^T$
		- For any $\vec{y} \in \mathbb{R}^m$, there exists at most one solution $\vec{x} = B \vec{y}$ 
		- If $\vec{y}\in \cal{R}(A)$ and $\cal{N}(A^*) \neq \{0\}$ then there are infinite number of solutions to $A\vec{x}=\vec{y}$
	- **Invertibility**: (Existence and Uniqueness): if $rank(A)=r=n=m$ ($A$ is square and full rank) then:
		- There exists an inverse $A^{-1} = B = C$
		- For any $\vec{y} \in \mathbb{R}^m$ there exists one and only one solution $\vec{x} = A^{-1}\vec{y}$

## Pseudoinverse Operators

- **Pseudoinverse**: let $A:X\rightarrow Y$ be a bounded linear operator between 2 inner product spaces $X$ and $Y$.
	- 1.) Given any $\vec{y} \in Y$ let $\vec{x} \in X$ be the vector that solves:
		- $min_{\vec{x}\in X} ||\vec{y}-A\vec{x}||_Y$
	- 2.) If there are multiple minimizers, let $\vec{x}'$ denote the one having minimal norm $||\vec{x}'||_X$
- The pseudoinverse of $A$ denoted $A^+: Y \rightarrow X$ is defined as the operator mapping any $\vec{y} \in Y$ to the corresponding $\vec{x}' \in X$
- **Facts of Pseudoinverses**:
	- The pseudoinverse is always a bounded linear operator
	- Special Cases
		- If $A$ is invertible then $A^+ = A^{-1}$
		- If $A^*A$ is invertible, then $A^+ = (A^*A)^{-1}A^*$ (left inverse)
		- If $AA^*$ is invertible then $A^+ = A^*(AA^*)^{-1}$
	- Other Properties:
		- $(A^+)^+ = A$
		- $(A^+)^* = (A^*)^+$
		- $A^+AA^+ = A^+$
		- $AA^+A = A$
		- $A^+A$ and $AA^+$ are self Adjoint
		- $\cal(R)(A^+) = \cal(R)(A^*)$ and $\cal(N)(A^+) = \cal(N)(A^*)$ 
- Pseudoinverses have a useful connection to orthogonal projections specifically
	- $AA^+$ is orthogonal projection operator onto $\cal{R}(A)$. 
	- $A^+A$ is an orthogonal projection operator onto $\cal{R}(A^*)$

## Matrix Case

- Consider $X\in \mathbb{R}^n$ and $Y \in \mathbb{R}^m$ and $A:X \rightarrow Y$:
	- Given any $\vec{y} \in Y$ let $\vec{x}\in X$ be a vector that solves:
		- $min_{\vec{x}\in X} ||\vec{y}-A\vec{x}||_2$
	- and if there are multiple minimizers, let $\vec{x}'$ be the only one having minimal norm $||\vec{x}'||_2$
	- The pseudoinverse of $A$ denoted $A^+$ is a $n \times m$ matrix that allows us to compute for any $\vec{y}$ the corresponding $\vec{x}'$
		- $\vec{x}' = A^+ \vec{y}$
- Useful facts and expressions about matrix pseudoinverse:
	- If $A$ is invertible (this requires $m = n$ and $rank(A)=m=n$) then
		- $A^+ = A^{-1}$
	- If $A$ has linearly independent columns (this requires $m \geq n$ and $rank(A) = n$) then (left inverse):
		- $A^+ = (A^HA)^{-1}A^H$
	- If $A$ has linearly independent rows ($m \leq n$ and $rank(A)=m$) then (right inverse):
		- $A^+ = A^H(AA^H)^{-1}$
- Other properties for matrix case: ![[Pasted image 20240911083835.png]]

## Normal Equations:

- Repeated notes from Normla Eq
- Now lets see how this can all be interpreted using operators, Adjoint, and pseudoinverses:
	- Define linear operator : $V: R^n \rightarrow S$ by eq:
		- $V\vec{a} = \sum_{k=1}^{n} a_k \vec{v_k}$
	- Notice the best approximation is by finding $\vec{a}$ that minimizes $||\vec{x}-V\vec{a}||_S$
	- Know that the minimizer $\vec{a}$ must satisfy:
		- $V^*V\vec{a} = V^* \vec{x}$
	- by def the Adjoint of $V(V^*)$ denoted as $V^*: S \rightarrow R^n$ is a unique operator such that for all $\vec{z} \in R^n$ and $\vec{y} \in S$:
		- $<V\vec{z},\vec{y}>_S = <\vec{z},V^*\vec{y}>_l2$
	- We can write:
		- $<V\vec{z},\vec{y}>_s = <\sum_{k=1}^{n}z_k\vec{v_k}, \vec{y}> = sum_{k=1}^{n} z_k <\vec{v_k},\vec{y}>_S$
	- and
		- $<\vec{z},V^* \vec{y}>_l2 = \sum_{}^{} z_k((V^* \vec{y})_k)^*$
	- so
		- $V^*\vec{y} = \begin{bmatrix} <\vec{y},\vec{v_1}>_s\\ <\vec{y},\vec{v_2}>_s\\ ....\\ <\vec{y},\vec{v_n}>_s \end{bmatrix}$
		- s

