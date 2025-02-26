

## Features as Image Corners

### What is a good feature? (Requirements)
- **Repeatability** (to be invariant/robust to transformation and noise)
- **Distinctiveness** (to be easy to distinguish or match)
- **Locality** (due to occlusion)
- **Quantity** (sufficient number), **accuracy** (localization), **efficiency** (computing time), ...


---

## Harris Corner (1988)

### Key idea: Sliding window

#### Formulation
$$I(x + \Delta x, y + \Delta y) \approx I(x, y) + I_x(x, y) \Delta x + I_y(x, y) \Delta y$$
where:
- $I_x = \frac{\partial I}{\partial x}$, $I_y = \frac{\partial I}{\partial y}$
- $$D(\Delta x, \Delta y) = \sum_{(x,y) \in W} \sigma_{xx} I(x + \Delta x, y + \Delta y) - I(x, y) \approx \begin{bmatrix} \Delta x & \Delta y \end{bmatrix} M \begin{bmatrix} \Delta x \\ \Delta y \end{bmatrix}$$

where $M$ is:
$$M = \sum_{(x,y) \in W} \begin{bmatrix} I_x^2 & I_x I_y \\ I_x I_y & I_y^2 \end{bmatrix}$$

#### Harris Corner Response
$$R = \det(M) - k \cdot (\text{trace}(M))^2$$
where:
- $\det(M) = \lambda_1 \lambda_2$
- $\text{trace}(M) = \lambda_1 + \lambda_2$
- $k \in [0.04, 0.06]$

#### Good-Feature-to-Track (Shi-Tomasi, 1994)
$$R = \min(\lambda_1, \lambda_2)$$

**Properties:**
- Invariant to translation, rotation, and intensity shift $I \rightarrow I + b$
- Variant to image scaling

---

## SIFT (Scale-Invariant Feature Transform; 1999)

### Key idea: Scale-space (~ image pyramid) and DoG (difference of Gaussian)

#### Gaussian Scale-Space
$$L(x, y, \sigma) = G(x, y, \sigma) * I(x, y)$$

#### DoG Scale-Space
$$D(x, y, \sigma) = L(x, y, k\sigma) - L(x, y, \sigma)$$

### Part #1) Feature Point Detection
1. Find local extrema (minima and maxima) in DoG scale-space.
2. Localize their position accurately using a 3D quadratic function.
3. Eliminate low-contrast candidates, $|D(x)| < \tau$.
4. Eliminate candidates on edges:
$$\frac{\text{trace}(H)^2}{\det(H)} < \frac{(r+1)^2}{r}$$
where:
$$H = \begin{bmatrix} D_{xx} & D_{xy} \\ D_{xy} & D_{yy} \end{bmatrix}$$

### Part #2) Orientation Assignment
1. Compute magnitude and orientation of gradient:
$$m(x, y) = \sqrt{(L(x+1, y) - L(x-1, y))^2 + (L(x, y+1) - L(x, y-1))^2}$$
$$\theta(x, y) = \tan^{-1}\left(\frac{L(x, y+1) - L(x, y-1)}{L(x+1, y) - L(x-1, y)}\right)$$
2. Find the strongest orientation using histogram voting (36 bins).

### Part #3) Feature Descriptor Extraction
1. Build a 4x4 gradient histogram (8 bins each) from a 16x16 patch.
2. Encode into a 128-dimensional vector and normalize it.

*Note: The SIFT patent expired on March 6, 2020.*

---

## SURF (Speeded-Up Robust Features; 2006)

### Key idea: Approximation of SIFT
- Uses Haar-like features and integral images to approximate DoG.

---

## FAST (Features from Accelerated Segment Test; 2006)

### Key idea: Intensity check of continuous arc of $n$ pixels
- A point $p$ is a corner if a segment of $n$ pixels is either all brighter or all darker than $I_p \pm t$.
- **FAST-9** (n=9), **FAST-12** (n=12), FAST-ER (enhanced repeatability via decision trees).

---

## BRIEF (Binary Robust Independent Elementary Features; 2010)

### Key idea: Intensity comparison of random pixel pairs
- **Patch size**: 31 × 31 pixels
- **Descriptor size**: 128 tests (128 bits = 16 bytes)
- **Versions**: BRIEF-32, BRIEF-64, BRIEF-128, BRIEF-256, BRIEF-512

**Combinations:**
- SIFT feature points + BRIEF descriptors
- FAST feature points + BRIEF descriptors

---

## ORB (Oriented FAST and Rotated BRIEF; 2011)

### Key idea: Adding rotation invariance to BRIEF

#### Oriented FAST
1. Generate scale pyramid for scale invariance.
2. Detect FAST-9 points (filtered using Harris corner response).
3. Compute feature orientation using the intensity centroid:
$$C = \left( \sum x I(x, y), \sum y I(x, y) \right)$$
$$\theta = \tan^{-1}\left( \frac{m_{01}}{m_{10}} \right)$$

#### Rotation-aware BRIEF
- Extract BRIEF descriptors w.r.t. the known orientation.

---

