# Definitions

- **Sonar** (Sound Navigation and Ranging): Acoustic sensing technology that uses sound waves to detect and measure objects.
- **Radar** (Radio Detection and Ranging): Sensors that use radio waves to detect and measure objects and their velocities.
- **LiDAR** (Light Detection and Ranging): An *exteroceptive sensor* that uses laser light to measure distances and create 3D maps.
- **IMU** (Inertial Measurement Unit): A *proprioceptive sensor* that measures motion and orientation.

---

# Notes

## Cameras

- **Mapping**: Cameras capture visual data to create a map of the environment.
- **Localization**: Cameras help determine the robot's position within the mapped environment.

### Camera Types:

1. **Stereo Cameras**:
   - Create a depth map of the scene for 3D modeling.
   - Rely on disparities between two images (stereo vision).
   - Some models use structured infrared (IR) light to measure distances in low-light or featureless environments.

2. **Thermal/IR Cameras**:
   - Capture infrared radiation emitted by objects, enabling thermal imaging.
   - Can be classified as:
     - **Cooled**: More sensitive but requires cooling.
     - **Uncooled**: Less sensitive but more compact and energy-efficient.

3. **Hyperspectral Cameras**:
   - Capture images across multiple narrow spectral bands, unlike standard RGB cameras which only have 3 bands.
   - Useful for detailed material or chemical analysis.

4. **Event Cameras**:
   - Detect changes or motion in a scene by capturing events rather than full frames.
   - Particularly effective in high-speed or dynamic environments.

---

## IMU (Inertial Measurement Unit)

- **Definition**: A *proprioceptive sensor* that measures motion and orientation.
- **Components**:
  - **Accelerometer**: Measures linear acceleration.
  - **Gyroscope**: Measures angular velocity (rotation rate).
  - **Magnetometer** (optional): Measures the strength and direction of the magnetic field for heading estimation.

---

## LiDAR (Light Detection and Ranging)

- **Definition**: An *exteroceptive* and *active sensor* that uses laser light to measure distances.
- **Working Principle**:
  - Emits laser beams and calculates the time taken for the beams to reflect back to the sensor.
  - Produces high-resolution 3D maps of the environment.

---

## Radar (Radio Detection and Ranging)

- **Definition**: Sensors that use radio waves to detect objects and measure their distance, velocity, and direction.
- **Characteristics**:
  - Works well in challenging weather conditions like rain or fog.
  - Suitable for detecting objects over longer distances.

---

## Sonar (Sound Navigation and Ranging)

- **Definition**: Acoustic sensing technology that uses sound waves to detect and measure objects.
- **Applications**:
  - Commonly used in underwater environments (e.g., submarines and robotic fish).
  - Effective for short-range object detection in air or water.

---
