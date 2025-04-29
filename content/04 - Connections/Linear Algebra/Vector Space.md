**Idea**: While [[Metric Space]] gives us a notion of closeness between elements of a set, a **vector space** adds a full geometric structure, allowing us to define operations like addition and scalar multiplication on the set.

General Definition: 
A **Vector Space** $S$ is composed of a set of elements (called "vectors") and members of a field $R$ (called "Scalars") :
	- Roughly Vectors are objects that can be added together and multiplied by numbers (namely scalars)
	- A field is a set of numbers for which addition and multiplication are well defined we will typically use $R = \mathbb{R}$ or $R = \mathbb{C}$

---

# Vector Addition

Vector addition : associates any 2 vectors $\vec{x},\vec{y} \in S$ the sum $\vec{x} + \vec{y}$ which also belongs to $S$.

## Vector Addition Rules

1. **Commutativity**:
$$\vec{x} + \vec{y} = \vec{y} + \vec{x} \forall \vec{x},\vec{y} \in S$$
2. **Associativity**:
$$\vec{x} + (\vec{y} + \vec{z}) = (\vec{x} + \vec{y}) + \vec{z} \quad \forall \vec{x},\vec{y},\vec{z} \in S$$
3. There is a unique zero vector $\vec{0} \in S$ such that:
$$\vec{x} + \vec{0} = \vec{x} \quad \forall \ \vec{x} \in S$$
4. For each $\vec{x} \in S$ there is a vector $-\vec{x} \in S$ such that:
$$\vec{x} + (-\vec{x}) = \vec{0}$$
 ---
# Scalar Multiplication

Scalar Multiplication: associates any vector $\vec{x} \in S$ and any scalar $a \in R$ the scalar multiple of $\vec{x}$ by $a$, denoted by $a\vec{x}$ which belong to $S$.

## Scalar Multiplication Rules

1. **Distributivity**:
$$a(\vec{x} + \vec{y}) = a\vec{x} + a\vec{y}$$
	and 
	$$(a+b) \vec{x} = a\vec{x} + b\vec{x} \quad \forall \vec{x},\vec{y} \in S$$
	 and $a,b \in R$
2. **Associativity**: 
$$(ab)\vec{x} = a(b\vec{x}) \forall \vec{x} \in S$$
	and $a,b \in R$
3. For the multiplicative identity $R$ (denoted by scalar $1 \in R$) we have $1*\vec{x} = \vec{x} \in S$
4. For the additive identity in $R$ (denoted by the scalar $0 \in R$) we have $0* \vec{x} = \vec{0} \in S$

---
