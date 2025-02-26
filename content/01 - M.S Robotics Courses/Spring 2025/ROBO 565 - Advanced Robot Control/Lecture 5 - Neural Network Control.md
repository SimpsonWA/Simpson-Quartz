## Function Approximators

## Universal Approximators

## Generalization



## 5.1 NN Predictive Control (NNPC)

### **Overview**
Neural Network Predictive Control (NNPC), inspired by Model Predictive Control (MPC), uses a neural network to model a plant's nonlinear dynamics. The controller predicts future plant behavior over a finite horizon and computes control actions that optimize performance. This approach is versatile and suited for systems with dynamic and nonlinear characteristics.

**Process**:
1. **System Identification**: Train a neural network to model the plant's forward dynamics using historical input-output data.
2. **Prediction**: Use the neural network model to predict future plant states.
3. **Optimization**: An optimization algorithm (e.g., BFGS quasi-Newton) minimizes a cost function to compute the control input.

- **Key Features**:
  - Uses NN as a **plant model** to predict future responses.
  - Optimizes control signals by minimizing a performance criterion.
  - Requires **system identification** to train the NN on plant dynamics.

---

### **5.1.1 System Identification**

- The first step is to **train the neural network** to represent the plant's forward dynamics. This process is called **system identification**.
- Training data is collected by simulating or operating the plant, producing input-output pairs.

**Equation for the Plant Model**:
$$
y_m(k+1) = \hat{h}[y_p(k), \ldots, y_p(k-n+1), u(k), \ldots, u(k-m+1), \vec{x}]
$$
Where:
- $\hat{h}[\cdot, \vec{x}]$: Function implemented by the NN.
- $\vec{x}$: Vector containing the weights and biases of the network.
- $u(k)$: Control input.
- $y_p(k)$: Plant output at time step $k$.

---

### **5.1.2 Predictive Control**

Once trained, the NN model is used to predict the plant's response over a specific time horizon. These predictions are used to compute the control signal by minimizing the following **performance criterion**:

$$
J = \sum_{j=N_1}^{N_2} [y_r(k+j) - y_m(k+j)]^2 + \rho \sum_{j=1}^{N_u} [u'(k+j-1) - u'(k+j-2)]^2
$$

Where:
- $N_1, N_2, N_u$: Horizons for tracking error and control increments.
- $y_r(k+j)$: Desired response at future time step $k+j$.
- $y_m(k+j)$: Predicted plant response.
- $u'(k)$: Tentative control signal.
- $\rho$: Weighting factor penalizing large control changes.

---

## 5.2 NARMA-L2 Control

### **Overview**
The NARMA-L2 control approach aims to **linearize nonlinear system dynamics** using a Nonlinear Autoregressive Moving Average (NARMA) model. This allows the controller to simplify control tasks and compute the next control input directly.

- **Key Features**:
  - Transforms nonlinear dynamics into approximate linear forms.
  - Suited for systems that can be approximated by **companion form models**.
  - Efficient with low computational requirements but less flexible than NNPC.

---

### **5.2.1 Identification of the NARMA-L2 Model**

The **NARMA-L2 approximation model** is defined as:
$$
\hat{y}(k+1) = f[y(k), y(k-1), \ldots, y(k-n+1), u(k-1), \ldots, u(k-m+1)] + g[y(k), y(k-1), \ldots, y(k-n+1), u(k-1), \ldots, u(k-m+1)] \cdot u(k)
$$

Where:
- $f[\cdot]$: Represents the system's natural dynamics.
- $g[\cdot]$: Represents the nonlinear gain for control input $u(k)$.

The model uses **two sub-networks** to approximate the functions $f(\cdot)$ and $g(\cdot)$.

---

### **5.2.2 NARMA-L2 Controller**

Once the NARMA-L2 model is identified, the control input can be computed using the equation:
$$
u(k) = \frac{y_r(k+d) - f[\cdot]}{g[\cdot]}
$$
Where $y_r(k+d)$ is the desired plant output at a future time step $k+d$.

---

## 5.3 Model Reference Control

### **Overview**
Model Reference Control (MRC) uses **two neural networks**:
1. **Plant Model Network**: Trained to represent the plant's dynamics.
2. **Controller Network**: Trained to force the plant output to track the output of a **reference model**.

This architecture is particularly useful for general nonlinear systems, offering high flexibility. However, it requires computationally expensive **dynamic backpropagation** for training the controller.

---

### **Key Steps in Model Reference Control**

1. **Plant Model Identification**:
   - Train a neural network to approximate the plant using the NARMA model:
     $$
     \hat{y}(k+1) = f[y(k), \ldots, y(k-n+1), u(k-1), \ldots, u(k-m+1)] + g[\cdot] \cdot u(k)
     $$

2. **Controller Training**:
   - Train a second neural network (controller) to minimize the error between the plant output and the **reference model output**.

**Controller Equation**:
$$
e_c(k) = y_r(k) - y(k)
$$
Where:
- $e_c(k)$: Control error.
- $y_r(k)$: Reference model output.
- $y(k)$: Plant output.


### **Comparison of Controllers**

| Feature                 | NN Predictive Control (NNPC)  | NARMA-L2 Control               | Model Reference Control        |
|-------------------------|-------------------------------|--------------------------------|--------------------------------|
| **Computation**         | High (requires optimization) | Low (simple control law)       | Moderate (dynamic backpropagation) |
| **Flexibility**         | Broad (general nonlinear systems) | Limited (requires companion form) | Broad (general nonlinear systems)  |
| **Training Complexity** | Moderate                     | Low                           | High                          |
| **Online Complexity**   | High                         | Low                           | Low                           |

---
