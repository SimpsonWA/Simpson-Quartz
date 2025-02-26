## Condition Number;

- Return to the case when $A\vec{x}=\vec{y}$ has an exact solution
- We will also assume $A$  is square $(n \times n)$ and invertible
- Question of interest: How badly could errors in $\vec{y}$ affect the recovered soltuion $A^{-1}\vec{y}$
- **Setup**:
	- let $A$ be $n \times n$ and invertible
	- let $\vec{y}$ be the **noise free observations** for some original vector $\vec{x}$
	- Let $\vec{y}' = \vec{y} +\triangle \vec{y}$ be the **corrupted observations**
	- Let $\vec{x}' = A^{-1}\vec{y}$ be the recovered solution using corrupted obsrevations
	- writing $\vec{x}' = \vec{x} + \triangle \vec{x}$ we have:
		- $\vec{x} + \triangle \vec{x} = A^{-1}(\vec{y}+ \triangle \vec{y}) = A^{-1}\vec{y}+A^{-1} \triangle \vec{y}$
	- Since $\vec{x} = A^{-1}\vec{y}$ then we will have $\triangle \vec{x} = A^{-1} \triangle \vec{y}$
	- 1 interesting question is how does the relative error in the observations $\frac{|||\triangle \vec{y}|}{|||\vec{y}|}$ compare to $\frac{|||\triangle \vec{x}|}{|||\vec{x}|}$

## Condition Number Derivation:

- **Condition Number**: The condition number of a $n \times n$ invertible matrix $A$ is defined to be the following quantity:
	- $\kappa(A):= ||A||||A^{-1}||$
	- When an $l_p$ norm is used, the condition number is somtimes denoted:
		- $\kappa(A):= ||A||_p||A^{-1}||_p$
- Properties:
![[Pasted image 20240912164634.png]]

