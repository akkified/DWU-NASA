# Robotics & Inverse Kinematics (IK)

### 1. Pixel to Camera Frame
We convert the pixel coordinates $(u, v)$ from the YOLO bounding box to a normalized camera frame using the intrinsic matrix $K$:

$$\begin{bmatrix} x_c \\ y_c \\ z_c \end{bmatrix} = K^{-1} \begin{bmatrix} u \\ v \\ 1 \end{bmatrix} \times Z$$

### 2. 2-DOF Inverse Kinematics
For a 2-Degree of Freedom (DOF) gimbal or arm, we calculate the joint angles ($\theta_1, \theta_2$) to reach the target $(x, y)$ using the Law of Cosines:

$$\theta_2 = \arccos\left(\frac{x^2 + y^2 - L_1^2 - L_2^2}{2 L_1 L_2}\right)$$
$$\theta_1 = \arctan2(y, x) - \arctan2(L_2 \sin\theta_2, L_1 + L_2 \cos\theta_2)$$

Where:
- $L_1, L_2$: Length of the arm segments.
- $x, y$: Target coordinates in the robot's base frame.