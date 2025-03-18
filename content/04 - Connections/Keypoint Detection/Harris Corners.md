
The **Harris Corner Detection** algorithm is a widely used method in computer vision to identify corners within an image. Corners are points where the intensity of the image changes significantly in multiple directions,.

## Mathematical Foundation

The core idea behind the Harris Corner Detector is to analyze the change in intensity for a small window shifted by $(u, v)$ in both $x$ and $y$ directions. This change is represented by the function $E(u, v)$:

$$
E(u, v) = \sum_{x, y} w(x, y) \left[ I(x + u, y + v) - I(x, y) \right]^2
$$

Here:

- $I(x, y)$ denotes the intensity at pixel $(x, y)$.
- $w(x, y)$ is a window function, commonly a Gaussian, that assigns weights to the pixels in the window.
- $(u, v)$ represents the shift in the $x$ and $y$ directions.

Expanding $I(x + u, y + v)$ using a Taylor series approximation, we get:

$$
I(x + u, y + v) \approx I(x, y) + u I_x(x, y) + v I_y(x, y)
$$

where $I_x$ and $I_y$ are the partial derivatives of the intensity in the $x$ and $y$ directions, respectively.

Substituting this approximation into the expression for $E(u, v)$:

$$
E(u, v) \approx \sum_{x, y} w(x, y) \left[ u I_x(x, y) + v I_y(x, y) \right]^2
$$

This can be rewritten in matrix form:

$$
E(u, v) \approx \begin{bmatrix} u & v \end{bmatrix}
\begin{bmatrix}
A & C \\
C & B
\end{bmatrix}
\begin{bmatrix}
u \\
v
\end{bmatrix}
$$

where:

$$
A = \sum_{x, y} w(x, y) I_x^2(x, y)
$$

$$
B = \sum_{x, y} w(x, y) I_y^2(x, y)
$$

$$
C = \sum_{x, y} w(x, y) I_x(x, y) I_y(x, y)
$$

The matrix:

$$
M = \begin{bmatrix}
A & C \\
C & B
\end{bmatrix}
$$

is known as the **structure tensor** or **second-moment matrix**.
## Corner Response Function

To determine the presence of a corner, the eigenvalues $\lambda_1$ and $\lambda_2$ of the matrix $M$ are analyzed:

- If both eigenvalues are large, the region is a corner.
- If one eigenvalue is large and the other is small, the region is an edge.
- If both eigenvalues are small, the region is flat.

Instead of computing the eigenvalues directly, the Harris Corner Detector uses the following **corner response function** $R$:

$$
R = \det(M) - k \cdot (\text{trace}(M))^2
$$

where:

- $\det(M) = AB - C^2$ is the determinant of $M$.
- $\text{trace}(M) = A + B$ is the trace of $M$.
- $k$ is an empirical constant, typically in the range $[0.04, 0.06]$.

A large positive value of $R$ indicates a corner, a negative value indicates an edge, and a value close to zero indicates a flat region.

# Pseudocode

```pseudo
\begin{algorithm}
	\caption{Harris Corner Detection}
	\begin{algorithmic}
	\REQUIRE Grayscale image $I$, window function $w(x, y)$, threshold $T$
	\ENSURE Set of detected corner points $\mathcal{C}$
		\STATE Compute image gradients: 
		\STATE $I_x = \frac{\partial I}{\partial x}, I_y = \frac{\partial I}{\partial y}$
		\STATE Compute products of derivatives: $I_x^2, I_y^2, I_x I_y$
		\STATE Apply Gaussian filter to obtain $A, B, C$:
		\STATE $A = w(x, y) * I_x^2$, $\quad$ $B = w(x, y) * I_y^2$, $\quad$ $C = w(x, y) * I_x I_y$
		\STATE Compute Harris response:
		\STATE $R = (AB - C^2) - k(A + B)^2$
		\STATE Threshold $R$ to retain only strong corner responses:
		\STATE $\mathcal{C} = \{(x, y) \mid R(x, y) > T\}$
		\STATE Apply non-maximum suppression to find local maxima
		\RETURN $\mathcal{C}$
	\end{algorithmic}
\end{algorithm}
```
# Example (OpenCV):

```python 

```