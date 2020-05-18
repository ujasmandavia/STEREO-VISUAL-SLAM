# Stereo Visual SLAM on KITTI

## Overview

This is a code-base for visual slam written by # Shangzhou Ye and it is working well for me with a ROS wrapper and I'm planning to use it to add loop closure, landmark based optimization and parallel thread to this code-base

Here is the link to the original code by Shangzhou Ye
https://github.com/shangzhouye/stereo-visual-slam.git

This project built a stereo visual SLAM system from scratch. It has feature-based visual odometry using ORB features, and a keyframe-based map management and optimization backend. The system is integrated with ROS.

The system has six major components:

- Initialization
- Feature Detection/Matching
- Motion Estimation
- Map Management
- Bundle Adjustment
- Visualization Module

## File Structure

### Folders

* [cmake_module/](cmake_module/): cmake modules.
* [config/](config/): config files.
* [include/](include/): c++ header files.
* [src/](src/): ROS node and C++ source code.
* [launch/](launch/): launch file.

### Structure

```
config/
├── kitti_config.rviz
└── kitti_param.yaml
include/
└── stereo_visual_slam_main
    ├── library_include.hpp
    ├── map.hpp
    ├── optimization.hpp
    ├── types_def.hpp
    ├── visual_odometry.hpp
    └── visualization.hpp
launch/
└── run_vslam.launch
src/
├── stereo_visual_slam_main
    ├── map.cpp
    ├── optimization.cpp
    ├── types_def.cpp
    ├── visual_odometry.cpp
    └── visualization.cpp
└── run_vslam.cpp
```

- `config/kitti_param.yaml` contains the path to the dataset
- `library_include.hpp` include libraries that are commonly used in the package
- `map.hpp` definition of map management module
- `optimization.hpp` implementation of non-linear optimization using G2O
- `types_def.hpp` definition of frame, landmark, feature struct
- `visual_odometry.hpp` functions for the stereo visual odometry
- `visualization.hpp` the visualization module
- `run_vslam.cpp` is the ROS node for running this system

## Dependency

- **ROS Melodic** ([Link](http://wiki.ros.org/melodic/Installation/Ubuntu))
- **OpenCV** (Version 3.2)
- **Eigen** ([Official Site](http://eigen.tuxfamily.org/))
- **Sophus**: Lie Groups Library ([Link](https://github.com/strasdat/Sophus))
- **G20**: Graph Optimization Framework ([Link](https://openslam-org.github.io/g2o.html))

## Quick Start guide

- Install all the dependencies
- `fork` this repository, then `git clone` or build using `wstool`
- Build the package `catkin_make -DCMAKE_BUILD_TYPE=Release` in release mode
- Modify the path to KITTI dataset on your computer in `config/kitti_param.yaml`
- To download KITTI dataset, go to [this link](http://www.cvlibs.net/datasets/kitti/eval_odometry.php).
- If Rviz visualization is needed, set `if_rviz` to true in `config/kitti_param.yaml`
- If writing estimated trajectory to file is needed, set `if_write_pose` to true in `config/kitti_param.yaml`
- To launch the system, do `source devel/setup.bash` and `roslaunch stereo_visual_slam_main run_vslam.launch`

