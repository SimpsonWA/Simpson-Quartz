## Image Features

- Visual Features:
	- **Keypoint** is a locally distinct location in an object
	- The feature **descriptor** summarizes the local structure around the keypoint
- We can find distinct keypoints using:
	- **Harris corners**
	- **Shi- Tomasi corner detector**
	- **Difference of Gaussians**
- Corners and Edges:
	- Corners are highly distinct points
	- Corners are invariant to translation, rotation , and illumination
	- Corner = 2 edges in roughly orthogonal directions
	- Edge = a sudden  brightness change


# Keypoint Detection Methods: Harris Corners, Shi-Tomasi, and Difference of Gaussians

## 1. Harris Corners
The **Harris Corner Detector** identifies points in an image where the intensity changes significantly in all directions. It is commonly used for detecting corners and relies on local gradient analysis.

### How It Works:
1. **Gradient Calculation:** The gradients $(I_x)$ and $(I_y)$ of the image are calculated using Sobel filters.
2. **Structure Tensor:** A second-moment matrix (also called the structure tensor) is constructed at each pixel:
   $$
   M = \begin{bmatrix}
   I_x^2 & I_x I_y \\
   I_x I_y & I_y^2
   \end{bmatrix}
   $$
3. **Corner Response Function (R):**
   Using the structure tensor, a corner response value \( R \) is calculated for each pixel:
   $$
   R = \text{det}(M) - k \cdot (\text{trace}(M))^2
   $$
   - **det(M):** Determinant of \( M \), related to the product of eigenvalues.
   - **trace(M):** Sum of eigenvalues of \( M \).
   - \( k \): A sensitivity parameter (typically 0.04–0.06).
4. **Thresholding:** Pixels with \( R > \text{threshold} \) are considered corners.

### Characteristics:
- Detects corners but may struggle with flat or edge-like regions.
- Sensitive to rotation and slightly scale-dependent.
- Effective for finding high-curvature points.

---

## 2. Shi-Tomasi Corner Detector
The **Shi-Tomasi Corner Detector** is an improvement over Harris Corners. Instead of using the corner response \( R \), it directly uses the smallest eigenvalue of the structure tensor to evaluate corners.

### How It Works:
1. **Gradient Calculation:** Similar to Harris, it calculates \( I_x \) and \( I_y \) and builds the structure tensor \( M \).
2. **Eigenvalues:** The eigenvalues (\( \lambda_1 \) and \( \lambda_2 \)) of \( M \) are computed.
3. **Corner Quality Measure:**
   A point is considered a corner if the smaller eigenvalue (\( \text{min}(\lambda_1, \lambda_2) \)) is greater than a certain threshold.
4. **Thresholding:** The smallest eigenvalue is compared to a threshold to determine if the point is a corner.

### Characteristics:
- Simpler and more robust than Harris Corners.
- Focuses only on eigenvalues, avoiding the \( R \)-value approximation.
- Ideal for computational efficiency and accuracy.

---

## 3. Difference of Gaussians (DoG)
The **Difference of Gaussians** is primarily used in blob and keypoint detection and is an integral part of algorithms like SIFT (Scale-Invariant Feature Transform).

### How It Works:
1. **Gaussian Smoothing:** The image is blurred with Gaussian kernels of different standard deviations (\( \sigma_1 \) and \( \sigma_2 \)):
   $$
   G(x, y, \sigma) = \frac{1}{2 \pi \sigma^2} e^{-\frac{x^2 + y^2}{2 \sigma^2}}
   $$
2. **Difference of Gaussians:** The blurred images are subtracted:
   $$
   D(x, y, \sigma) = G(x, y, \sigma_1) - G(x, y, \sigma_2)
   $$
   This acts as a band-pass filter, highlighting regions with specific frequency components.
3. **Keypoint Detection:** Local extrema (minima and maxima) in the DoG images are found by comparing each pixel with its neighbors across scale and space. These extrema correspond to potential keypoints.

### Characteristics:
- Used in scale-invariant algorithms like SIFT.
- Detects blobs or distinct structures, not just corners.
- Inherently multi-scale, allowing for detection of features at different sizes.

---

## Comparison Table

| Feature             | Harris Corners         | Shi-Tomasi Corner Detector | Difference of Gaussians (DoG) |
|---------------------|------------------------|----------------------------|--------------------------------|
| **Purpose**         | Corner detection       | Improved corner detection  | Keypoint and blob detection   |
| **Key Criterion**   | Corner response \( R \)| Minimum eigenvalue         | Local extrema in scale space  |
| **Scale Invariant** | No                     | No                         | Yes                           |
| **Applications**    | General feature detection | General feature detection | Scale-invariant keypoint detection (e.g., SIFT) |
# **Feature Descriptors**

![[Keypoint Descriptor.png]]

- Each keypoint has a surrounding region of pixels that can be used to describe and match keypoints across different images.
- Feature descriptors aim to provide a unique and robust representation of these keypoints, making them invariant to transformations like scaling, rotation, and illumination changes.

## **1.) SIFT (Scale-Invariant Feature Transform)**

- Introduced by David Lowe, SIFT detects and describes keypoints in an image using a multi-scale approach.
- It computes keypoint descriptors by analyzing gradients in the local neighborhood around a keypoint.
- Each descriptor consists of a 128-dimensional vector capturing the gradient orientations.
- **Advantages:**
    - Scale and rotation invariant.
    - Robust to changes in illumination and viewpoint.
- **Lowe's Ratio Test for Matching:**
    - When matching descriptors, the nearest neighbor distance ratio (NNDR) is used.
    - If the ratio of the closest match to the second-closest match is below a threshold (e.g., 0.75), the match is considered reliable, helping remove outliers.

## **2.) BRIEF (Binary Robust Independent Elementary Features)**

- A lightweight descriptor designed for speed, replacing floating-point representations with binary strings.
- Works by selecting pairs of pixels in a keypoint neighborhood and comparing their intensity values.
- The descriptor is stored as a binary vector, where each bit represents the outcome of a pixel intensity comparison.
- **Advantages:**
    - Extremely fast due to binary representation.
    - Low memory footprint.
- **Limitations:**
    - Not inherently scale or rotation invariant.
    - Sensitive to noise and viewpoint changes.

## **3.) ORB (Oriented FAST and Rotated BRIEF)**

- An extension of BRIEF that introduces orientation information, making it more robust.
- Uses the **FAST (Features from Accelerated Segment Test)** detector to find keypoints and then applies BRIEF with rotation invariance.
- Instead of simple pixel comparisons, it assigns a dominant orientation to each keypoint using intensity centroids.
- **Advantages:**
    - Fast and efficient, suitable for real-time applications.
    - Rotation-invariant, improving upon BRIEF’s limitations.
    - Open-source alternative to SIFT and SURF (free of patent restrictions).
- **Limitations:**
    - Still less robust than SIFT in extreme transformations.

---
