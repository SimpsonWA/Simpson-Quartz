
At each iteration of the gradient descent algorithm, we take a step in the direction of the negative gradient:  
$$
x_{k+1} = x_k - \alpha_k \nabla f(x_k) \quad k = 0, 1, 2, \ldots
$$  

Where $\alpha_k > 0$ is the step size, and:  
$$
x_{k+1}, x_k \in \mathbb{R}^n, \quad \nabla f(x_k) \in \mathbb{R}^n, \quad \alpha_k \in \mathbb{R}
$$  

Since the algorithm moves in the direction of the negative gradient, it is also known as the **steepest descent algorithm**.

![[content/04 - Connections/Numeric Optimization/001 - Images/GradientDescentFigure.png]]