**Idea**: A metric space is a set with a metric which is a rule that assigns a distance between any two points in the set.

Formal Definition: A metric space is a set $X$ together with a valid metric $d: X \times X \rightarrow \mathbb{R}$ which gives us a measurement of distance between points in a set $X$


## Properties

Suppose that $X$ is a set. Then $d: X \times X \rightarrow \mathbb{R}$ is a **valid metric** for $X$ if the following properties are satisfied for all $x,y \in X$:

**Symmetry Property**: Distance is independent of direction
$$
d(x,y) = d(y,x)
$$
**Non-Negativity**: Distance cant be negative
$$
d(x,y) \geq 0
$$
**Identity of Indiscernibles**: The Distance between $x$ and $y$ is $0$ only if $x=y$ :
$$
d(x,y) = 0 \ \text{if} \ x=y
$$
**Triangle Inequality**: For all $x,y,z \in X$ :
$$
d(x,z) \leq d(x,y) + d(y,z)
$$

---
## Examples: 

**L1 Metric** ("Manhattan distance") : 
$$d(x,y) = \sum_{i=1}^{n} |x_i - y_i|$$
**Euclidean (L2) Metric**: 
$$d(x,y) = (\sum_{i=1}^{n} |x_i - y_i|^2)^{1/2}$$
**$l_p$ metric**:
$$d(x,y) = (\sum_{i=1}^{n} |x_i - y_i|^p)^{\frac{1}{p}}$$

---
