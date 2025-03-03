## Camera matrix:
$$
P = \begin{bmatrix}
f & 0 & px \\
0 & f & py \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
r1 & r2 & r3 & t1 \\
r4 & r5 & r6 & t2 \\
r7 & r8 & r9 & t3
\end{bmatrix}
$$

- 1st matrix: intrinsic parameters
- 2nd matrix: extrinsic parameters
- $f$: focal length of the camera (in mm or px)
- $px$ and $py$: locations of the principal/optical point (in mm or px)

For camera calibration, the extrinsic parameters are unknown.

Many different ways to calibrate a camera:
- Radiometric calibration
- Color calibration
- Geometric calibration
- Noise calibration
- Lens (or aberration) calibration

## Geometric distortion models
- Camera lens generates geometric distortion which can be approximated as a non-linear function $f_d$.
- Camera projection with geometric distortion: $\tilde{x} = proj(x, K, R, t, f_d)$ where $d$ is a set of distortion coefficients.

$$
\mathbf{X} = \begin{bmatrix} X \\ Y \\ Z \end{bmatrix} \rightarrow \mathbf{X}' = R\mathbf{X} + t \rightarrow \hat{\mathbf{x}} = \begin{bmatrix} \hat{x} \\ \hat{y} \end{bmatrix} = \begin{bmatrix} \frac{X'}{Z'} \\ \frac{Y'}{Z'} \end{bmatrix}
$$

3D point (world frame) $\rightarrow$ 3D point (camera frame) $\rightarrow$ normalized image plane

$$
\mathbf{x}_d = f_d(\hat{\mathbf{X}})
$$

geometric distortion

$$
\mathbf{X} = \begin{bmatrix} x \\ y \end{bmatrix} = \begin{bmatrix} f_x \hat{x} + c_x \\ f_y \hat{y} + c_y \end{bmatrix}
$$

pinhole camera calibration

Polynomial distortion model (geometric distortion):

$$
\begin{bmatrix} x_d \\ y_d \end{bmatrix} = (1 + k_1 r^2 + k_2 r^4 + \ldots) \begin{bmatrix} \hat{x} \\ \hat{y} \end{bmatrix} + \begin{bmatrix} 2p_1 \hat{x} \hat{y} + p_2 (r^2 + 2\hat{x}^2) \\ 2p_2 \hat{x} \hat{y} + p_1 (r^2 + 2\hat{y}^2) \end{bmatrix}
$$

where $r^2 = \hat{x}^2 + \hat{y}^2$

Fish-eye lens model:

$$
\begin{bmatrix} x_d \\ y_d \end{bmatrix} = (1 + k_1 \theta^2 + k_2 \theta^4 + \ldots) \frac{\theta}{r} \begin{bmatrix} \hat{x} \\ \hat{y} \end{bmatrix}
$$

where $r^2 = \hat{x}^2 + \hat{y}^2$ and $\theta = \tan^{-1}(r)$

