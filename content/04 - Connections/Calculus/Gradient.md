 **Definition**: The gradient of a function at a point is a vector that points in the direction of the greatest rate of increase of the function.

If $f$ is differentiable at $x$, we call the corresponding $g$ vector the gradient of $f$ at $x$. It is denoted as $\nabla f(x) \in \mathbb{R}^n$ and given by:
$$
\nabla f(x) = \begin{pmatrix} \frac{\partial f}{\partial x_1} \\ \frac{\partial f}{\partial x_2} \\ \vdots \\ \frac{\partial f}{\partial x_n} \end{pmatrix} \in \mathbb{R}^n
$$

Example of a vector field of a 3d function: 
![[Gradient Image.png]]

## Example:

Given the function:  
$$
f(x,y,z) = 2x + 3y^2 - \sin(z)
$$  
The gradient is determined by taking the partial derivative with respect to each variable:  
$$
\begin{align}
\frac{\partial f}{\partial x} &= \frac{\partial}{\partial x} (2x + 3y^2 - \sin(z)) = 2, \\
\frac{\partial f}{\partial y} &= \frac{\partial}{\partial y} (2x + 3y^2 - \sin(z)) = 6y, \\
\frac{\partial f}{\partial z} &= \frac{\partial}{\partial z} (2x + 3y^2 - \sin(z)) = -\cos(z).
\end{align}
$$  
Thus, the gradient of $f(x,y,z)$ is:  
$$
\nabla f(x,y,z) = \begin{bmatrix}
2 \\
6y \\
-\cos(z)
\end{bmatrix}.
$$  
