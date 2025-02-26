## Transformations

**Def:** a transformation $T$ is a coordinate-changing operation $p' = T(p)$

- For linear transformations $T$ as a matrix:
$$
\begin{bmatrix}
x' \\
y'
\end{bmatrix}
= T
\begin{bmatrix}
x \\
y
\end{bmatrix}
$$

- Common transformations:
  - Translation
  - Rotation
  - Scaling
  - Affine
  - Perspective

## Scaling

- Scaling a coordinate means multiplying each of its components by a scalar:
  - **Uniform scaling**: the scaling is the same for all components (x, y, z, etc.)
  - **Non-uniform scaling**: different scalars for components (ex: $1.5x, 0.5y$)

- Scaling operation:
  - $x' = ax$
  - $y' = by$

- Or in matrix form:
$$
\begin{bmatrix}
x' \\
y'
\end{bmatrix}
=
\begin{bmatrix}
a & 0 \\
0 & b
\end{bmatrix}
\begin{bmatrix}
x \\
y
\end{bmatrix}
\Rightarrow
\begin{bmatrix}
a & 0 \\
0 & b
\end{bmatrix}
= S
$$
# Basic 2D Transformations

**Scale:**
$$
\begin{bmatrix}
x' \\
y'
\end{bmatrix}
=
\begin{bmatrix}
S_x & 0 \\
0 & S_y
\end{bmatrix}
\begin{bmatrix}
x \\
y
\end{bmatrix}
$$

**Shear:**
$$
\begin{bmatrix}
x' \\
y'
\end{bmatrix}
=
\begin{bmatrix}
1 & \alpha_x \\
\alpha_y & 1
\end{bmatrix}
\begin{bmatrix}
x \\
y
\end{bmatrix}
$$

**Rotate:**
$$
\begin{bmatrix}
x' \\
y'
\end{bmatrix}
=
\begin{bmatrix}
\cos \theta & -\sin \theta \\
\sin \theta & \cos \theta
\end{bmatrix}
\begin{bmatrix}
x \\
y
\end{bmatrix}
$$

**Translate:**
$$
\begin{bmatrix}
x' \\
y'
\end{bmatrix}
=
\begin{bmatrix}
1 & 0 & t_x \\
0 & 1 & t_y
\end{bmatrix}
\begin{bmatrix}
x \\
y \\
1
\end{bmatrix}
$$

**Affine:**
$$
\begin{bmatrix}
x' \\
y'
\end{bmatrix}
=
\begin{bmatrix}
a & b & c \\
d & e & f
\end{bmatrix}
\begin{bmatrix}
x \\
y \\
1
\end{bmatrix}
$$

# Affine Transformations

- Affine transformations are combinations of:
  - Linear transformations
  - Translations

- Properties of affine transforms:
  - Lines map to lines
  - Parallel lines remain parallel
  - Ratios are preserved
  - Closed under composition

=**copy table from: slide 17**

### Projective Transformations

- Combinations of Affine transformations and projective warps
- Some properties as Affine and:
  - Parallel lines don't remain parallel
  - Ratios are not preserved
  - Projective matrix is defined up to a scale

$$
\begin{bmatrix}
x' \\
y' \\
w'
\end{bmatrix}
=
\begin{bmatrix}
a & b & c \\
d & e & f \\
g & h & i
\end{bmatrix}
\begin{bmatrix}
x \\
y \\
w
\end{bmatrix}
$$

### Homogeneous Coordinates

- Converting to homogeneous coordinates:
  - 2D image: $(x, y) \Rightarrow \begin{bmatrix} x \\ y \\ 1 \end{bmatrix}$
  - 3D coordinates: $(x, y, z) \Rightarrow \begin{bmatrix} x \\ y \\ z \\ 1 \end{bmatrix}$

- Converting from homogeneous coordinates:
  - 2D coordinates: $\begin{bmatrix} x \\ y \\ w \end{bmatrix} \Rightarrow \left( \frac{x}{w}, \frac{y}{w} \right)$
  - 3D coordinates: $\begin{bmatrix} x \\ y \\ z \\ w \end{bmatrix} \Rightarrow \left( \frac{x}{w}, \frac{y}{w}, \frac{z}{w} \right)$

- These coordinates are scale invariant in projected space

$$
\left( \begin{array}{c}
x \\
y \\
w \\
\end{array} \right) 
\rightarrow 
\left( \begin{array}{c}
kx \\
ky \\
kw \\
\end{array} \right) 
= 
\left( \begin{array}{c}
\frac{kx}{kw} \\
\frac{ky}{kw} \\
\end{array} \right) 
\rightarrow 
\left( \begin{array}{c}
\frac{x}{w} \\
\frac{y}{w} \\
\end{array} \right)
$$

**Camera Matrix**

- Camera as just a mapping from the 3D world to a 2D image
$$
x = PX
$$
	- Where $x$ : 2d image point
	- $P$: Camera matrix
	- $X$: 3D world Point
- Camera as a coordinate transformation:

$$
\left( \begin{array}{c}
x \\
y \\
z \\
\end{array} \right) 
= 
\left( \begin{array}{ccc}
p_1 & p_2 & p_3 \\
p_5 & p_6 & p_7 \\
p_9 & p_{10} & p_{11} \\
\end{array} \right) 
\left( \begin{array}{c}
x \\
y \\
z \\
1 \\
\end{array} \right)
$$

Homogeneous image coords

Homogeneous world coordinates

- Camera matrix: $\mathbf{P}$

- Camera matrix decomposed:

$$
\mathbf{P} = 
\left( \begin{array}{ccc}
f & 0 & p_x \\
0 & f & p_y \\
0 & 0 & 1 \\
\end{array} \right) 
\left( \begin{array}{ccc}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1 \\
\end{array} \right)
$$

$$
\mathbf{P} = \mathbf{K} \left[ \mathbf{I} | \mathbf{0} \right] 
\quad \text{where} \quad 
\mathbf{K} = 
\left( \begin{array}{ccc}
f & 0 & p_x \\
0 & f & p_y \\
0 & 0 & 1 \\
\end{array} \right)
$$

- $f$: Focal length
- $p_x$ Principal point coordinates
- $p_y$ Principal point coordinates

We can write everything into a single projection!

$$
x = P X_w
$$

$$
P = \begin{bmatrix}
f & 0 & p_x \\
0 & f & p_y \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
I & 0
\end{bmatrix}
\begin{bmatrix}
R & -RC \\
0 & 1
\end{bmatrix}
$$

$$
\begin{bmatrix}
f & 0 & p_x \\
0 & f & p_y \\
0 & 0 & 1
\end{bmatrix}
$$
: Intrinsic parameters: which refer to the camera internal parameters

$$
\begin{bmatrix}
I & 0
\end{bmatrix}
$$
: Perspective projection (3x4): maps 3D to 2D points (camera-to-image)

$$
\begin{bmatrix}
R & -RC \\
0 & 1
\end{bmatrix}
$$
: Extrinsic parameters (4x4): correspond to camera extrinsics (world to camera)

In general $P$ can be written as:

$$
P = K [R | t] = \begin{bmatrix}
f & 0 & p_x \\
0 & f & p_y \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
v_1 & v_2 & v_3 & t_1 \\
v_4 & v_5 & v_6 & t_2 \\
v_7 & v_8 & v_9 & t_3
\end{bmatrix}
$$

$$
R = \begin{bmatrix}
v_1 & v_2 & v_3 \\
v_4 & v_5 & v_6 \\
v_7 & v_8 & v_9
\end{bmatrix}
$$
: 3D rotation

$$
t = \begin{bmatrix}
t_1 \\
t_2 \\
t_3
\end{bmatrix}
$$
: 3D translation

$$
t = -RC
$$

Intrinsic parameters in camera matrix $K$:
- focal length, principle point, skew, distortion, etc.

Extrinsic parameters in point parameterization $R$ and $t$:
- rotation, translation

# Notecards

#CSCI598-FlashCards 


