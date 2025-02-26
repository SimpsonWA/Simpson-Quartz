# Definitions

- **Mapping**: The process of creating a representation of an unknown environment by collecting and organizing spatial data.
- **Mapping Representation**: The format or structure used to encode the mapped environment, such as point clouds, occupancy grids, or polygons.
- **Point Clouds**: A collection of data points in a 3D space, typically obtained from sensors like LiDAR or depth cameras, representing the geometry of an environment.
- **Polygons/Patches**: Simplified geometric representations of surfaces or objects in a map, often used to describe planar regions or boundaries in an environment.
- **Occupancy Grid**: A grid-based mapping representation where each cell stores a probability value indicating whether it is occupied, free, or unknown, enabling efficient spatial reasoning.
- **Semantic/Objects**: Mapping representations that include high-level information about the environment, such as the identification and categorization of objects (e.g., cars, trees, or buildings).
- **Metric**: A precise, quantitative representation of an environment focusing on spatial dimensions, distances, and coordinates to support accurate navigation and mapping.
- **Topological**: A representation that focuses on the connectivity and relationships between locations or landmarks, abstracting away precise metric details.
- **Localization**: The process of determining an agent's precise position and orientation (pose) within the environment, based on sensor data and map information.
- **Pose**: A combined representation of an agent's position (e.g., x, y, z) and orientation (e.g., roll, pitch, yaw) within a given frame of reference.
- **SLAM**: Simultaneous Localization and Mapping, a process where a robot builds a map of an environment while simultaneously localizing itself within it.
- **Factor Graph**: A mathematical framework for solving estimation/inference problems to ensure consistency.

---

# Notes

## SLAM Components

The standard SLAM pipeline consists of three key elements:
- **Sensors**
- **Front-End Algorithms**
- **Back-End Algorithms**

### Sensors

#### Proprioceptive (Internal State Perception)
- **IMU**: Measures acceleration and angular velocity (e.g., gyroscope, accelerometer, magnetometer).
- **Wheel Encoder**: Tracks wheel rotations to estimate distance traveled.

#### Exteroceptive (External Environment Perception)
- **Camera**: Captures visual data for feature tracking and 3D reconstruction.
- **LiDAR**: Provides high-resolution 3D point clouds of the environment.
- **Radar**: Measures object distance and velocity, effective in various weather conditions.
- **Sonar**: Uses sound waves to detect nearby objects or surfaces.
- **GPS**: Provides absolute positioning in global coordinates (when available).

---

### Front-End

The **Front-End** handles real-time, online processing, including:
- Sensor data processing.
- Feature extraction and tracking.
- Data association (matching sensor data to landmarks or map features).
- Initial trajectory/pose estimation (e.g., odometry).
- Initial map estimation.

---

### Back-End

The **Back-End** focuses on:
- **Optimization and Refinement**: Improving the accuracy of the map and the robot's trajectory.
- **Loop Closure**: Identifying and correcting drift by recognizing previously visited locations.

