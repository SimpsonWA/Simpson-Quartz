# Definitions:

**Neural Networks**: A type of machine learning model inspired by the structure and function of the human brain, composed of layers of interconnected nodes (neurons). Neural networks process data to identify patterns and make predictions or decisions.

**Supervised Learning**: A machine learning paradigm where a model is trained on a labeled dataset, learning to map inputs to their corresponding outputs. Examples include classification and regression tasks.

**Reinforcement Learning**: A type of machine learning where an agent learns by interacting with an environment, receiving feedback in the form of rewards or penalties to improve its decision-making over time.

**Unsupervised Learning**: A machine learning approach where the model learns patterns and structures in data without labeled outputs. Common tasks include clustering and dimensionality reduction.

**Classification**: A supervised learning task where the goal is to categorize data into predefined classes or labels. Examples include spam detection and image recognition.

**Regression**: A supervised learning task focused on predicting continuous numerical values based on input data. Examples include predicting house prices or stock market trends.

**Gradient Descent**: An optimization algorithm used to minimize a loss function by iteratively adjusting model parameters in the direction of the steepest descent of the gradient. It's widely used in training neural networks and other machine learning models.

# Notes:

- **Sigmoid Functions**: Smooth differentiable and monotonically increasing
	- The Logistic Function:
$$
sigmoid(x) = \frac{1}{1+e^{-x}}
$$
- Hyperbolic Tangent:
$$
tanh\left(\frac{x}{2}\right)= \frac{1-e^{-x}}{1+e^{-x}}
$$
- **Piecewise-Linear Functions**: Approximations of a sigmoid function:
$$
f(x) = \begin{cases} 1  & if \ x\geq 0.5 \\
x+0.5  & if \ -0.5\leq x \leq 0.5 \\
0  & if \ x \leq 0.5\end{cases}
$$
## Single Layer Feed Forward Networks: Training:

- Error on pattern $n$:
$$
e^{n}= t^{n}-y^ n
$$
- Mean Square error:
$$
E = \frac{1}{2} \sum\limits_{n=1}^{N}(e^{n})^{2}
$$
- Least Mean Square algorithm:
$$
\frac{\partial E}{\partial w} = e^{n}\frac{\partial e^{n}}{\partial w}
$$
- Gradient Descent: 
$$
\Delta w = - \eta \frac{\partial E}{\partial w}
$$
- Linear activation function:
$$
\frac{\partial E}{\partial w_{i,j}} = e_{i}^{n}\frac{\partial e_{i}^{n}}{\partial w_{i,j}} = -e_{i}^{n}x_{j}^{n}
$$
- Weight update:
$$
\Delta w_{i,j}= - \eta \frac{\partial E}{\partial w_{i,j}} = \eta e_{i}x_{j}
$$