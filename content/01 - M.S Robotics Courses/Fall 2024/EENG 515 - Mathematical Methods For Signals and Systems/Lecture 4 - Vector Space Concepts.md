## Vector Spaces:

- A metric merely gives us a notion of closeness between elements of a set. With vector spaces we will get more geometric structure, including the ability to talk about the "size" of elements in a set, subspaces, bases, dimensions, etc
- A **Vector Space** $S$ is composed of a set of elements (called "vectors") and members of a field $R$ (called "Scalars")
	- Roughly Vectors are objects that can be added together and multiplied by numbers (namely scalars)
	- A field is a set of numbers for which addition and multiplication are well defined we will typically use $R = \mathbb{R}$ or $R = \mathbb{C}$
- In a vector space there are 2 rules for combining vectors and scalars
	1. Vector addition : associates any 2 vectors $\vec{x},\vec{y} \in S$ the sum $\vec{x} + \vec{y}$ which also belongs to $S$ Vector addition operation must obey these 4 rules
		1. (**Commutativity**): $\vec{x} + \vec{y} = \vec{y} + \vec{x} \forall \vec{x},\vec{y} \in S$
		2. (**Associativity**): $\vec{x} + (\vec{y} + \vec{z}) = (\vec{x} + \vec{y}) + \vec{z} \forall \vec{x},\vec{y},\vec{z} \in S$
		3. There is a unique *zero vector* $\vec{0} \in S$ such that $\vec{x} + \vec{0} = \vec{x} \forall \vec{x} \in S$
		4. For each $\vec{x} \in S$ there is a vector $-\vec{x} \in S$ such that $\vec{x} + (-\vec{x}) = \vec{0}$
	2. Vector Multiplication: associates any vector $\vec{x} \in S$ and any scalar $a \in R$ the scalar multiple of $\vec{x}$ by $a$, denoted by $a\vec{x}$ which belong to $S$. Vector multiplication operation must obey these 4 rules:
		5. (**Distributivity**): $a(\vec{x} + \vec{y}) = a\vec{x} + a\vec{y}$ and $(a+b) \vec{x} = a\vec{x} + b\vec{x} \forall \vec{x},\vec{y} \in S$ and $a,b \in R$
		6. (**Associativity**): $(ab)\vec{x} = a(b\vec{x}) \forall \vec{x} \in S$ and $a,b \in R$
		7. For the multiplicative identity $R$ (denoted by scalar $1 \in R$) we have $1*\vec{x} = \vec{x} \in S$
		8. For the additive identity in $R$ (denoted by the scalar $0 \in R$) we have $0* \vec{x} = \vec{0} \in S$
- **Infinite Sequence**: an infinite sequence of real numbers has the form $\vec{x} = (x_1,x_2,....)$ with each $x_k \in \mathbb{R}$
- **Bounded Infinite Sequence**: an infinite sequence of real numbers is said to be bounded if there exists a constant $M$ such that $|x_k| < M$ for all $k = 1,2,.....$
- **Cartesian Product**: Suppose $X$ and $Y$ are 2 vector spaces with the same scalar field $R$. The cartesian product $X$ and $Y$, is the set of all ordered pairs $(\vec{x},\vec{y})$ with $\vec{x} \in X$ and $\vec{y} \in Y$. With the scalar field $R$ and definitions of vector addition and multiplication below, $X \times Y$ is a valid vector space:
	- Addition on $X \times Y$ is defined component wise: 
$$
	(\vec{x_1},\vec{y_1}) + (\vec{x_2},\vec{y_2}) = (\vec{x_1}+\vec{x_2},\vec{y_1}+\vec{y_2})
$$
	- Scalar Multiplication on $X \times Y$ is defined by:
$$
	a(\vec{x},\vec{y}) = (a\vec{x},a\vec{y})
$$
## Linear Subspaces:

- **Linear Subspace**: a nonempty subset $T$ of a vector space $S$ (with scalar field $R$) is called a subspace (or linear subspace) of $S$ if it contains a $\vec{0}$ and $a\vec{x} + b\vec{y} \in T$ for all $\vec{x},\vec{y} \in T$ and all $a,b\in R$ (i.e $T$ is closed under weighted vector addition)
	- $T$ must contain $\vec{0}$
	- Any linear subspace $T$ meets all the properties of a vector space
	- Any vector space $S$ is a linear subspace of itself

## Linear Combinations:

- Linear combinations are used to build new vectors as a weighted sum of other vectors
- **Linear Combination**: let $M = \{\vec{v_1},\vec{v_2},.....,\vec{v_m}\}$ be a collection of vectors in a vector space $S$.
	- A linear combination of vectors $M$ is a sum of the form:
$$
	\sum_{i=1}^{n} a_i \vec{v_i} = a_1\vec{v_1}+a_2\vec{v_2}+...+a_n\vec{v_n}
$$
	- for some $a_1,a_2,...,a_n \in R$
- **Span**: Let $M = \{\vec{v_1},\vec{v_2},.....,\vec{v_m}\}$ be a finite collection of vectors in the vector space $S$. The span of $M$, denoted by $span(M)$ or $span\{\vec{v_1},\vec{v_2},.....,\vec{v_m}\}$ is the set of all linear combinations of vectors in $M$:
	- That is:
$$
	span(M) = \{ \sum_{i=1}^{n} a_i \vec{v_i} : a_i \in R \}
$$

## Linear Dependence and Linear Independence 

- **Linear Dependence**: A finite set of vectors $\vec{v_1},\vec{v_2},.....,\vec{v_n}$ in a vector space $S$ is said to be linearly dependent if there exists scalars $a_1,a_2,...,a_n \in R$ not all equal to zero such that:
$$
a_1\vec{v_1} + a_2\vec{v_2} +... + a_n\vec{v_n} = \vec{0}
$$
- **Linear Independence**: A finite set of vectors $\vec{v_1},\vec{v_2},.....,\vec{v_n}$  in a vector space $S$ is linearly independent if 
$$
a_1\vec{v_1} + a_2\vec{v_2} +... + a_n\vec{v_n} = \vec{0}
$$
	- only when all $a_k = 0$
	- Every vector in a span of a linearly independent set of vectors has a unique expansion in terms of those vectors:
		- Suppose $\vec{v_1},\vec{v_2},.....,\vec{v_n}$ are linearly independent and suppose:
$$
		\vec{x} = a_1\vec{v_1}+a_2\vec{v_2}+...+a_n\vec{v_n} = b_1\vec{v_1}+b_2\vec{v_2}+...+b_n\vec{v_n}
$$
		- for some scalars $a_1,a_2,...,a_n \in R$ and $b_1,b_2,...,b_n \in R$ then $a_k = b_k$ for $k=1,2,...,n$
## Bases and Dimensions:

- **Basis**: A finite set of vectors $\vec{v_1},\vec{v_2},.....,\vec{v_n}$ in a vector space $S$ is said to be a basis for $S$ if the following are true:
	1. $\vec{v_1},\vec{v_2},.....,\vec{v_n}$ are linearly independent
	2. $span\{\vec{v_1},\vec{v_2},.....,\vec{v_n}\} = S$ 
	- a vector space with a finite basis is said to be finite-dimensional 
- Any 2 bases for a finite-dimensional vector space contain the same number of elements. This leads to the def of Dimension
- **Dimension**: For a vector space $S$ that can be spanned using a finite set of basis vectors , the dimension of $S$ is the number of vectors required in any basis for $S$
- For a vector space $S$ that cannot be spanned using a finite set of basis vectors, the dimension $S$ is said to be infinite. 


