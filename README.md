# RealSense D435 + End-Effector Mount Assets

This folder contains the standalone assets for the Intel RealSense D435 camera and its specific end-effector mount (compatible with xArm Lite6 and similar robot arms).

## Contents

- `meshes/visual/`: Contains the high-quality STL of the camera and mount.
- `meshes/collision/`: Contains the collision model for the camera and mount.
- `urdf/realsense_d435.xacro`: The Xacro macro to include the camera in your robot description.

## How to use in your project

### 1. File Structure
Add these files to your ROS 2 package. It is recommended to keep the `meshes` and `urdf` subfolders.

### 2. Xacro Integration
In your main robot Xacro file, include and call the macro:

```xml
<!-- 1. Include the macro -->
<xacro:include filename="$(find your_package_name)/urdf/realsense_d435.xacro" />

<!-- 2. Call the macro -->
<xacro:realsense_d435 
  prefix="" 
  parent="link6" 
  origin_xyz="0 0 0" 
  origin_rpy="0 0 0" 
  use_gazebo_plugin="true" />
```

### 3. Parameters
- `prefix`: Add a prefix to all links and joints (useful for multi-robot setups).
- `parent`: The link you want to attach the mount to (e.g., `link6`, `end_effector_link`).
- `origin_xyz` / `origin_rpy`: Offset from the parent link to the mount base.
- `use_gazebo_plugin`: Set to `true` to enable the RGBD camera sensor for Gazebo Sim (Ignition).

### 4. Important Coordinate Frames
The macro creates the standard RealSense frames:
- `camera_link`: Base frame of the camera.
- `camera_color_optical_frame`: The frame used for image data (Z-forward).
- `camera_depth_optical_frame`: The frame used for depth data.

## Note on Meshes
The mesh `d435_with_cam_stand.stl` includes both the D435 camera body and the L-shaped mounting bracket
