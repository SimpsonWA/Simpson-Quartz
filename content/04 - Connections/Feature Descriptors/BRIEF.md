
**BRIEF**: Binary Robust Independent Elementary Features

BRIEF is a binary descriptor which means it aim is to generate a small binary strings that are easy to compute and compare

In BRIEF each keypoint is described by a feature vector which is 128-512 bits string

The BRIEF algorithm uses a Gaussian Kernel for smoothing the image to reduce the sensitivity which allows for increased stability and reliability of the descriptor

After smoothing the image patch $p$ we then create a binary feature vector of the binary test($\tau$) responses given as: 

$$
\tau (p;x,y) = \begin{cases}
1 : p(x) < p(y) \\
0 :p(x) \geq p(y)
\end{cases}
$$

- $p(x)$ is the intensity value of p at a point  $x$

We then choose a set of $n(x,y)$ location pairs as a set of binary tests, where $n$ is the length of the binary feature vector which can be (128,256, and 512)


Here are the 5 sampling approches for the (x,y) pairs:
1. Uniform (GI): Both x and y pixels in the random pair is drawn from a Uniform distribution or spread of $\frac{S}{2}$ around keypoint. The pair can lie close to the patch border 

https://medium.com/@deepanshut041/introduction-to-brief-binary-robust-independent-elementary-features-436f4a31a0e6 : Reference