## Overview:

- Suppose we have a vector $\vec{y} \in Y$ and an $m \times n$ matrix $A$ are given. In this set of note we focus on the eq:
$$
A\vec{x} = \vec{y}
$$
- Note this gives $m$ known equations ($A$ and $\vec{y}$ are the knowns) in $n$ unknowns ($\vec{x}$)
- Questions that arise
	- Is there a solution $\vec{x} \in X$ to this equation?
		- If so is it unique 
		- How do we find it
		- How sensitive to change is it (i.e: noise in $\vec{y}$)
	- If there is no solution how can we best approximate it?
		- How good is this approximation?
- Useful to write $A$ as its Columns and rows:
	- $A = [\vec{a_1} \ \vec{a_2} ... \ \vec{a_n}]$
	- $A^T = [\vec{r_1}^T \ \vec{r_2}^T \ ... \ \vec{r_n}^T]$
	- where each $\vec{a_k} \in Y$ and each $\vec{r_k}^T \in X$

## How many Solutions: 

- Lets interpret $A\vec{x} = \vec{y}$ in the space $Y = \mathbb{R}^n$ or $\mathbb{C}^n$
- We can write $A\vec{x} = \vec{y}$ as:
	- $\vec{y}=\vec{a_1}x_1+\vec{a_2}x_2+...\vec{a_n}x_n$
- From our understanding of basis vectors and subspaces we can see there is one solution if:
	- $\vec{y} \in span\{\vec{a_1},\vec{a_2},..,\vec{a_N}\} = colspan(A) = \cal{R}(A)$
![[Pasted image 20240911111549.png]]

- **Lemma (Zero Solutions)**: if $\vec{y} \not \in colspan(A)$ then $A\vec{x}=\vec{y}$ has no solution
- **Lemma (One Solution)**: if $\vec{y} \in colspan(A)$ and the columns of $A$ are linearly independent, then $A\vec{x} = \vec{y}$ has a unique solution
- **Lemma (Infinite many Solutions)**: If $\vec{y} \in colspan(A)$ and columns of $A$ are linearly dependent, then $A\vec{x} = \vec{y}$ has infinite many solutions

## Alternate View

- Consider $A\vec{x} =\vec{y}$ as a set of constraints in the space $X=\mathbb{R}^n$ or $\mathbb{C}^n$  where $\vec{x}$ lies
- Consider the 1st entry of $\vec{y}$ and the 1st row of $A$. We have the constraint:
	- $a_11x_1 + a_12x_2 + ... a_{1n} x_n = y_1$
- In general this constraint will be satisfied for all $\vec{x}$ that live along some $(n-1)$-dimensional `hyperplane` of $X=\mathbb{R}^n$ or $\mathbb{C}^n$
- A **hyperplane**, also known as a affine subspace, is just a linear subspace that has been translated so it might not pass through the origin 
- Lets call the hyperplane $H_1$. The orientation of $H_1$ will depend on $a_11,a_12,...a_{1n}$ and translation of $H_1$ will depend on $y_1$
	- if $y_1=0$ the hyperplane will pass through the origin and be a linear subspace
- Each of the $m$ entries of $\vec{y}$ constraints the solution $\vec{x}$ to live in some $(n-1)$-dimensional hyperplanes. Call these $H_1,H_2,...,H_n$
- A vector $\vec{x} \in X$ will satisfy $A\vec{x} = \vec{y}$ if it belongs to all $m$ of these hyperplanes
- If orthogonal:
	- $A\vec{x}=\vec{y}$ if $\vec{x} \in H_1 \cap H_2 \cap .... \cap H_m$
- 3 Possibilities of intersection of hyperplanes
	- if $H_1 \cap H_2 \cap .... \cap H_n = \vec{0}$ there is no  solutions for $\vec{x}$
	- if $H_1 \cap H_2 \cap ... \cap H_n$ contains a single point there is a unique solution $\vec{x}$
	- if $H_1 \cap H_2 \cap ... \cap H_n$ contains $\infty$ many points, there are $\infty$ many solutions $\vec{x}$

