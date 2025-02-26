
- **Gram-Schmidt** algorithm 1 way to obtain an orthogonal basis
- Problem we want to solve:
	- Suppose we have a set of vectors $\vec{v_1},\vec{v_2},...,\vec{v_n}$ in an inner product space $S$. Assume the vectors are linearly independent.
- The goal is to construct a set of vectors $\vec{q_1},\vec{q_2},....,\vec{q_n}$ such that
$$
1. \quad span\{\vec{q_1},\vec{q_2},....,\vec{q_n}\} = span\{\vec{v_1},\vec{v_2},....,\vec{v_n}\}
$$
$$
1.  \quad <\vec{q_k},\vec{q_l}> = \begin{cases}
									1, k=l \\
									0, k \neq l
									\end{cases}
$$
- So 2 is saying that the vectors $\vec{q_1},\vec{q_2},....,\vec{q_n}$ are orthonormal
- In other words we want $\vec{q_1},\vec{q_2},....,\vec{q_n}$ to form an Orthobasis for n-dimension subset we spanned by $\vec{v_1},\vec{v_2},...,\vec{v_n}$

### Formulation:

1. We find a unit normal vector $\vec{q_1}$ such that $span\{\vec{q_1}\} = span\{\vec{v_1}\}$
2. We find a unit-norm vector $\vec{q_2}$ orthonormal to $\vec{q_1}$ such that $span\{\vec{q_1},\vec{q_2}\}  = span\{\vec{v_1},\vec{v_2}\}$ 
3. We find a unit-norm vector $\vec{q_3}$ orthonormal to $\vec{q_1}$ and $\vec{q_2}$ such that $span\{\vec{q_1},\vec{q_2},\vec{q_3}\}  = span\{\vec{v_1},\vec{v_2},\vec{v_3}\}$
4. So - on and so forth

$$
\vec{e_k} = \vec{v_k} - \sum_{l=1}^{k-1} <\vec{v_k},\vec{q_l}>\vec{q_l}
$$
- to get $\vec{q_k}$ normalize $\vec{e_k}$
$$
\vec{q_k} = \frac{\vec{e_k}}{||\vec{e_k}||}
$$
