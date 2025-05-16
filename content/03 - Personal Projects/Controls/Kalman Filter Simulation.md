**Description**: I wanted to deepen my understanding of how [[Kalman Filter]]s work, so I implemented a simple simulation in Python. The main idea is to estimate the current state of an object in 2D space using a Kalman Filter. The object's state is defined by its $(x, y)$ coordinates, and it moves with control velocities $v_x$ and $v_y$.

I predefined a trajectory using control inputs that guide the object along a circular path. At each time step, I track three key positions: the true position, the estimated position from the Kalman Filter, and a noisy measurement of the position. This setup demonstrates how Kalman Filters can significantly improve state estimation in the presence of noisy sensor data.
## Setup

### State

Here we know the state at each iteration which is:
$$
\mu_t = \begin{bmatrix}
x_t \\
y_t
\end{bmatrix}
$$
### Actions

We also know the controllable actions we can take as: 
$$
u_t = \begin{bmatrix}
v_{x,t}\\
v_{y,t}
\end{bmatrix}
$$
Where we have the velocity in both $x$ and $y$ directions at time $t$


### Motion Model

We can derive the linear model for the system where our state should be :
$$
\begin{align}
x_t = x_{t-1} + v_{x,t} \cdot \Delta t  \\
y_t = y_{t-1} + v_{y,t} \cdot \Delta t 
\end{align}
$$
This can be written in matrix form with process noise $w_t$ as:
$$
\mu_t = A_t \mu_{t-1} + B_t u_t + w_t
$$
where $w_t \sim \mathcal{N}(0, R)$ represents Gaussian process noise with covariance $R$.
### State Transition Matrix

The **state transition matrix** $A_t$​, which defines how the state evolves in the absence of control input, is:
$$
A_t = \begin{bmatrix}
1 & 0 \\
0 & 1
\end{bmatrix}
$$

### Control Input Matrix
The **control input matrix** $B_t$​, which maps control inputs to changes in state, is:
$$
B_t = \begin{bmatrix}
\Delta t & 0 \\
0 & \Delta t
\end{bmatrix}
$$

### Measurement

The measurement model assumes we observe the position directly, with some additive noise:
$$
z_t = C_t \mu_t + Q
$$
where: 
- $z_t$ is the observed (noisy) measurement
- $C_t$ : is the observation matrix in this case an Identity matrix
- $Q$: is the observation noise a matrix with a Gaussian noise distribution 

---

## Results
![[kalman_output.png]]


---

## Video (Manim)

![[KalmanFilter.mp4]]

---

## Code

```python 
import numpy as np
import matplotlib.pyplot as plt

  

def circle_control_inputs(samples=50, radius=1.0, timestep=1.0):
	angles = np.linspace(0, 2 * np.pi, samples, endpoint=False)
	angular_velocity = 2 * np.pi / (samples * timestep)
	linear_speed = radius * angular_velocity
	velocities = linear_speed * np.vstack((-np.sin(angles), np.cos(angles))).T
	return velocities

timeStep = 0.1

# Intal state and covaraince
mu = np.array([[0.0],
[0.0]])

sigma = np.array([[1.0 , 0],
[0, 1.0]])

  

# System matrices
A = np.array([[1,0],
[0,1]])

B = np.array([[timeStep, 0],
[0, timeStep]])

C = np.array([[1,0],
[0,1]])

  

# Noise Covariances

R = np.array([[0.00001, 0],
[0, 0.00001]]) # Process noise

Q = np.array([[0.1, 0],
[0, 0.1]]) # Measurement noise

pos_real = []
measurements = []
estimates = []

np.random.seed(42)

# Circle Control input
u_t = circle_control_inputs(samples = 100, radius=10, timestep=timeStep)

for i in range(100):

	theta = 2 * np.pi * i / 100 # N = number of steps
	u_vec = u_t[i].reshape(2, 1)
	
	# Simulate the real position wit noisy measurement
	process_noise = np.random.multivariate_normal([0,0],R).reshape(2,1)
	true_pos = A @ mu + B @ u_vec + process_noise
	measurement_noise = np.random.multivariate_normal([0,0],Q).reshape(2,1)
	z_t = C @ true_pos + measurement_noise
	
	# Prediction
	mu_bar = A @ mu + B @ u_vec
	sigma_bar = A @ sigma @ A.transpose() + R
	
	# Update step
	K_t = sigma_bar @ C.transpose() @ np.linalg.inv(C @ sigma_bar @ C.transpose() + Q)
	mu = mu_bar + K_t@(z_t - C @ mu_bar)
	sigma = (np.eye(2) - K_t @ C) @ sigma_bar
		
	pos_real.append(true_pos.flatten())
	measurements.append(z_t.flatten())
	estimates.append(mu.flatten())

  

# Plotting

true_positions = np.array(pos_real)
measurements = np.array(measurements)
estimates = np.array(estimates)

  

plt.figure(figsize=(10, 6))
plt.plot(true_positions[:, 0], true_positions[:, 1], 'k-', label='True Position')
plt.plot(measurements[:, 0], measurements[:, 1], 'rx', label='Measurements')
plt.plot(estimates[:, 0], estimates[:, 1], 'b--', label='Kalman Estimate')
plt.xlabel("X Position")
plt.ylabel("Y Position")
plt.legend()
plt.axis('equal')
plt.grid(True)
plt.savefig("kalman_output.png")

  

# Error predicted
rmse_predicted = np.sqrt(np.mean((estimates-true_positions)**2))
print(rmse_predicted)

  

# Error measurement
rmse_measurements = np.sqrt(np.mean((measurements-true_positions)**2))
print(rmse_measurements)
```
