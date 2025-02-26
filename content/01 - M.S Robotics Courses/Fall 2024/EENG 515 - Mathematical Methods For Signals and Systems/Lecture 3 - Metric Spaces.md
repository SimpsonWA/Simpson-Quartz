## Metric Spaces

- A metric space is a set $X$ together with a valid metric $d: X \times X \rightarrow \mathbb{R}$ which gives us a measurement of distance between points in a set $X$
- Suppose $X$ is a set. Then $d: X \times X \rightarrow \mathbb{R}$ is a valid metric for $X$ if the following properties are satisfied for all $x,y \in X$:
	- $d(x,y) = d(y,x)$ (**Symmetry Property**) : Distance is independent of direction
	- $d(x,y) \geq 0$ (**non-negative**)
	- $d(x,y) = 0$ if $x=y$ : The distance between x and y is 0 only if x=y
	- (**Triangle Inequality**)For all $x,y,z \in X$ :
		- $d(x,z) \leq d(x,y) + d(y,z)$
- Examples (Metrics for $\mathbb{R}^n$)
	- $l_1$ metric: 
		- $d(x,y) = \sum_{i=1}^{n} |x_i - y_i|$
	- $l_2$ metric ("**Euclidian**"):
		- $d(x,y) = (\sum_{i=1}^{n} |x_i - y_i|^2)^{1/2}$
	- $l_p$ metric for $1 \leq p \leq \infty$
		- $d(x,y) = (\sum_{i=1}^{n} |x_i - y_i|^p)^{\frac{1}{p}}$
	- $l_\infty$ metric:
		- $max_{i=1,2,....,n} |x_i - y_i|$

## Metrics for function Spaces 

- When $X$ is the set of real or complex functions $x(t)$ on the interval $t \in [a,b]$ a common choice is the $l_p$ metric for $1 \leq p \leq \infty$ :
$$
	d(x,y) = (\int_{a}^{b} |x(t) - y(t)|^p dt)^{\frac{1}{p}}
$$
- and for $p=\infty$ the $l_\infty$ metric:
$$
	d(x,y) = sup_{t \in [a,b]} |x(t)-y(t)|
$$
