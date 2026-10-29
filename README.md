# LASER UAV Mappings

`laser_uav_mappings` collects the mapping packages used by the LASER UAV System (LUS). ROG-Map builds local occupancy maps, inflates obstacles and can compute distance fields for planning.

This repository manages the ROG-Map checkout through Gitman. The `rog_map` package provides the mapping library, ROS 2 component, launch files and configuration.

## Components

| Mapper | ROS package | Role |
| --- | --- | --- |
| [ROG-Map](https://github.com/LASER-Robotics/rog_map) | `rog_map` | Local occupancy, obstacle inflation, frontier extraction and optional ESDF mapping used by SUPER. |

## Install and build

For a complete LUS setup, follow the [system installation guide](https://github.com/LASER-Robotics/laser_uav_system). To fetch ROG-Map from this repository directly:

```bash
gitman install
```

Gitman stores the checkout in `.gitman/` and links it under `ros_packages/`. The dependency revision is set in [.gitman.yml](.gitman.yml).

From a ROS 2 workspace containing the component package and its dependencies:

```bash
colcon build --packages-up-to rog_map
source install/setup.bash
```

## Use

To run ROG-Map independently:

```bash
ros2 launch rog_map run_rog_map.launch.py uav_name:=uav1 use_sim_time:=true
```

Provide odometry and a point cloud, with TF connecting the cloud frame to the odometry frame. The selected YAML configures sensor topics, map dimensions, resolution and visualization.

SUPER embeds the `rog_map_lib` library, so its planning process already contains the map. The standalone component is useful when running mapping independently.

See the [ROG-Map README](https://github.com/LASER-Robotics/rog_map) for launch arguments, parameters and ROS interfaces. This collection has no node or runtime parameters of its own.
