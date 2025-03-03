We define the Hessian of a function $f: \mathbb{R}^n \rightarrow \mathbb{R}$ at a point $x$ as:  
$$ 
\nabla^2 f(x) = \begin{bmatrix}
\frac{\partial^2 f}{\partial x_1^2} & \frac{\partial^2 f}{\partial x_1 \partial x_2} & \cdots & \frac{\partial^2 f}{\partial x_1 \partial x_n} \\
\frac{\partial^2 f}{\partial x_2 \partial x_1} & \frac{\partial^2 f}{\partial x_2^2} & \cdots & \frac{\partial^2 f}{\partial x_2 \partial x_n} \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial^2 f}{\partial x_n \partial x_1} & \frac{\partial^2 f}{\partial x_n \partial x_2} & \cdots & \frac{\partial^2 f}{\partial x_n^2}
\end{bmatrix}.
$$  

The Hessian matrix $\nabla^2 f(x)$ contains all second-order partial derivatives of $f$ and provides critical information about the local curvature of $f$ at $x$. If $f$ is twice continuously differentiable, the Hessian is symmetric due to Clairaut’s theorem, which states that the order of differentiation does not affect the result:  
$$
\frac{\partial^2 f}{\partial x_i \partial x_j} = \frac{\partial^2 f}{\partial x_j \partial x_i}.
$$  

### Interpretation of the Hessian:
- **Curvature Information**: The Hessian generalizes the concept of concavity and convexity from single-variable calculus to higher dimensions.  
  - If $\nabla^2 f(x)$ is **positive definite**, $f$ has a local minimum at $x$.  
  - If $\nabla^2 f(x)$ is **negative definite**, $f$ has a local maximum at $x$.  
  - If $\nabla^2 f(x)$ has both positive and negative eigenvalues, $x$ is a **saddle point**.  
- **Gradient of the Gradient**: The Hessian can be seen as the Jacobian of $\nabla f(x)$, meaning it captures how the [[Gradient]] itself changes in different directions.  

In optimization and machine learning, the Hessian plays a key role in second-order methods like [[Newtons Method]] which uses Hessian information to improve convergence rates when finding minima or maxima.  
