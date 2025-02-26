### Rotations in 2D:

$$
\begin{pmatrix}
x \\
y
\end{pmatrix}
=
\begin{pmatrix}
\cos \theta & -\sin \theta \\
\sin \theta & \cos \theta
\end{pmatrix}
\begin{pmatrix}
x' \\
y'
\end{pmatrix}
$$

$$
\begin{pmatrix}
x \\
y
\end{pmatrix}
= R
\begin{pmatrix}
x' \\
y'
\end{pmatrix}
$$

$$
\begin{pmatrix}
x' \\
y'
\end{pmatrix}
= R^T
\begin{pmatrix}
x \\
y
\end{pmatrix}
$$

### Homogeneous Coordinates

Points can be represented in homogeneous coord. which just means appending 1 as an extra element:

$$
\begin{pmatrix}
x \\
y \\
1
\end{pmatrix}
=
\begin{pmatrix}
x' \\
y' \\
s
\end{pmatrix}
$$

So we can do transform eqs as:

$$
\begin{pmatrix}
x' \\
y'
\end{pmatrix}
= R
\begin{pmatrix}
x \\
y
\end{pmatrix}
+ 
\begin{pmatrix}
t_x \\
t_y
\end{pmatrix}
\Rightarrow
x' = Rx + t
$$

Using homogeneous coordinates this transform eq becomes:

$$
\begin{pmatrix}
x' \\
y' \\
1
\end{pmatrix}
=
\begin{pmatrix}
R & t \\
0 & 1
\end{pmatrix}
\begin{pmatrix}
x \\
y \\
1
\end{pmatrix}
$$

$$
\tilde{X}' = H \tilde{X}
$$

- Conv $H$ is $\mathbb{R}^{3 \times 3}$

## Other 2D transforms:

### Scaled (Similarity) transform:
- Preserves angles but not distances.

$$
\begin{pmatrix}
x_B \\
y_B \\
1
\end{pmatrix}
=
\begin{pmatrix}
s & 0 & 0 \\
0 & s & 0 \\
0 & 0 & 1
\end{pmatrix}
\begin{pmatrix}
\cos \theta & -\sin \theta & t_x \\
\sin \theta & \cos \theta & t_y \\
0 & 0 & 1
\end{pmatrix}
\begin{pmatrix}
x_A \\
y_A \\
1
\end{pmatrix}
$$

### Affine transform

$$
\begin{pmatrix}
x_B \\
y_B \\
1
\end{pmatrix}
=
\begin{pmatrix}
a_{11} & a_{12} & t_x \\
a_{21} & a_{22} & t_y \\
0 & 0 & 1
\end{pmatrix}
\begin{pmatrix}
x_A \\
y_A \\
1
\end{pmatrix}
$$

### Projective Transform (Homography)
- $H$ is an arbitrary $3 \times 3$ matrix:

$$
\begin{pmatrix}
x_2 \\
y_2 \\
1
\end{pmatrix}
=
\begin{pmatrix}
h_{11} & h_{12} & h_{13} \\
h_{21} & h_{22} & h_{23} \\
h_{31} & h_{32} & h_{33}
\end{pmatrix}
\begin{pmatrix}
x \\
y \\
1
\end{pmatrix}
=
\mathbf{y} = H \mathbf{x}
$$

- Still need to divide by the 3rd element:

$$
\begin{pmatrix}
x' \\
y' \\
1
\end{pmatrix}
=
\begin{pmatrix}
x_1 / x_3 \\
x_2 / x_3 \\
1
\end{pmatrix}
$$

## 3D coordinate system

### Coordinate Names:
- Denoted as $\{A\}$, $\{B\}$, $\{C\}$, ... etc.
- Remember the order of rotation operations matters.

### XYZ Angles

**Rotation around the $Z$ axis:**

$$
\begin{pmatrix}
B_x \\
B_y \\
B_z
\end{pmatrix}
=
\begin{pmatrix}
\cos \theta_z & -\sin \theta_z & 0 \\
\sin \theta_z & \cos \theta_z & 0 \\
0 & 0 & 1
\end{pmatrix}
\begin{pmatrix}
A_x \\
A_y \\
A_z
\end{pmatrix}
$$

**Rotation around the $X$ axis:**

$$
\begin{pmatrix}
B_x \\
B_y \\
B_z
\end{pmatrix}
=
\begin{pmatrix}
1 & 0 & 0 \\
0 & \cos \theta_x & -\sin \theta_x \\
0 & \sin \theta_x & \cos \theta_x
\end{pmatrix}
\begin{pmatrix}
A_x \\
A_y \\
A_z
\end{pmatrix}
$$

**Rotation around the $Y$ axis:**

$$
\begin{pmatrix}
B_x \\
B_y \\
B_z
\end{pmatrix}
=
\begin{pmatrix}
\cos \theta_y & 0 & \sin \theta_y \\
0 & 1 & 0 \\
-\sin \theta_y & 0 & \cos \theta_y
\end{pmatrix}
\begin{pmatrix}
A_x \\
A_y \\
A_z
\end{pmatrix}
$$

We can concatenate the 3 rotations to yield a $3 \times 3$ rotation matrix:

$$
R_{xyz}(\theta_x, \theta_y, \theta_z) = R_z(\theta_z) R_y(\theta_y) R_x(\theta_x)
$$

$$
=
\begin{pmatrix}
c_z & -s_z & 0 \\
s_z & c_z & 0 \\
0 & 0 & 1
\end{pmatrix}
\begin{pmatrix}
c_y & 0 & s_y \\
0 & 1 & 0 \\
-s_y & 0 & c_y
\end{pmatrix}
\begin{pmatrix}
1 & 0 & 0 \\
0 & c_x & -s_x \\
0 & s_x & c_x
\end{pmatrix}
$$

- This is specifically around $x$ 1st, $y$ 2nd, $z$ 3rd

* $R$ can represent a rotational transformation from one frame to another

$$
^A_BR = \begin{pmatrix}
v_{11} & v_{12} & v_{13} \\
v_{21} & v_{22} & v_{23} \\
v_{31} & v_{32} & v_{33}
\end{pmatrix}
$$

* We can rotate a vector represented in frame $A$ to obtain its representation in frame $B$:

$$
^B\mathbf{v} = ^B_AR ^A\mathbf{v}
$$

* As in 2D, rotation matrices are orthonormal so the inverse of a rotation matrix is its transpose:

$$
(^A_BR)^{-1} = (^A_BR)^T = ^B_AR
$$

**Transforming a point**

* We can use $R, t$ to transform a point from coordinate frame $\{B\}$ to frame $\{A\}$:

$$
^A\mathbf{p} = ^A_BR ^B\mathbf{p} + t
$$

**Homogeneous coordinates**

* We can write the entire transformation with a single matrix as:

$$
^A\mathbf{p} = \begin{pmatrix}
x \\
y \\
z \\
1
\end{pmatrix} = \begin{pmatrix}
sx \\
sy \\
sz \\
s
\end{pmatrix}
$$

* Then:

$$
^A\mathbf{p} = ^A_BH ^B\mathbf{p} \text{ where } ^A_BH = \begin{bmatrix}
^A_BR & ^A\mathbf{t}_B \\
0 & 0 & 0 & 1
\end{bmatrix}
$$
# Matrix Inverses and Transposes

- The matrix inverse of the transformation is:
$$
A(BH) = (BH)^{-1}
$$

- Note that the inverse is not equal to the transpose in this case:
$$
A(BH) \neq (BH)^{T}
$$
