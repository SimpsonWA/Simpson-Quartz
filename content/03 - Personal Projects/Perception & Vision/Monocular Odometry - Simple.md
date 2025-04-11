# WORK IN PROGRESS:
#Python

**Description**: Development and high level overview of a monocular odometry system using available OpenCV libraries, with a predefined dataset.

# Results: 



---

# Steps:

## 1 Camera Calibration

- Really the goal is to obtain the $K$ matrix with intrinsic parameters. 
- These intrinsic parameters are often provided in the dataset. In this case, we have the following values available:

$$
k = \begin{bmatrix}
458.654 & 0 & 367.215 \\
0 & 457.296 & 248.375 \\
0 & 0 & 1
\end{bmatrix}
$$

## 2. Frame Acquisition

In this step the only data we need to handle are the images which are stored in a specific folder. To sequentially load and process each image we can simply iterate through the files in the folder using the following code:

```python
for filename in sorted(os.listdir(folderPath)):
```

The image is loaded in using  `cv.imread()` in greyscale mode:
```python 
full_path = os.path.join(folderPath, filename)

img = cv.imread(full_path, cv.IMREAD_GRAYSCALE)
```

## 3 Feature Extraction

Using ORB to find the key point and the descriptors 
```python
kp1, des1 = orb.detectAndCompute(img1, None)`
```
- `kp1` is a list of **keypoints**, where each keypoint contains:
	- x,y coordinates
	- orientation angle
	- scale 
	- response

- `des1` is a NumPy array of **descriptors**, where each row corresponds to a keypoint and encodes the appearance of its surrounding region.

So ORB (Oriented FAST and Rotated BRIEF) is essentially a algorithm that finds keypoints using a FAST keypoint detector and BRIEF descriptors 

## 4 Feature Matching

- Match the points using hamming distance etc and use the ratio test to keep good matches
For the feature mapping I am using the `bf.knnMatch()` function call which does a 

The way this function works is 
```python
matches = bf.knnMatch(desc1,desc2, k=2)
```

- *Inputs*:
	- `desc1`: descriptors from the first image
	- `desc2`: descriptors from the second image
	- `k`: number of best matches to find peqqr descriptor
- **Ouput**:
	- The output is a list of lists where each element is a list of `k` `Dmatch` objects
So the output in this case is essentially a matrix with 2 columns for each descriptor match 
![[Pasted image 20250408183004.png]]


After getting the matches from the function I then apply Lowe's ratio (0.7) to discard any outliers. (Could use RANSAC Instead)

![[Pasted image 20250408183434.png]]

## 5 Estimating relative pose

After finding all of the corresponding matched points I feed them into a list of points for each image:
```python 
pts1 = np.array([kp1[m.queryIdx].pt for m in goodMatches1], dtype=np.float32)

pts2 = np.array([kp2[m.trainIdx].pt for m in goodMatches2], dtype=np.float32)
```

Next, we use OpenCV’s `cv.findEssentialMat()`to estimate the Essential Matrix ($E$) using the 8-point algorithm:

```python
E, mask = cv.findEssentialMat(pts1, pts2, k)
```

The Essential Matrix encodes the relative rotation and translation between the two camera positions.

After obtaining the Essential Matrix, we use `cv.recoverPose()` to recover the **relative rotation** and **translation** between the two images:

```python
_, R, t, mask = cv.recoverPose(E, pts1, pts2, k)
```

Once the relative pose is recovered it can be used to update the camera’s position relative to the previous frame, allowing us to track the movement and estimate the camera's current location in space.
