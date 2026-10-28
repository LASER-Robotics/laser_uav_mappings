# LASER UAV Mappings

Gitman collection of mapping packages for the LASER UAV stack, following the same
repository layout as `laser_uav_planners` and `laser_uav_lio-s`.

| Mapper | ROS package | Role |
| --- | --- | --- |
| ROG-Map | `rog_map` | Local occupancy, inflation and ESDF mapping used by SUPER |

The repository stores dependencies in `.gitman/` and exposes them through
`ros_packages/`. It is a repository-only collection, so colcon discovers the
underlying ROS packages directly.

## Install

From this repository:

```bash
gitman install
```

The ROG-Map checkout uses `stable`. The planners
collection is separate; SUPER continues to declare a ROS dependency on `rog_map`.

From the workspace root:

```bash
gitman install --root src/laser_uav_mappings
gitman install --root src/laser_uav_planners
colcon build --packages-up-to laser_uav_managers
source install/setup.bash
```

The mapping package keeps its own configuration and launch files. ROG-Map
transforms clouds into the odometry frame using timestamped TF. Its implementation
and interfaces are unchanged by this collection.
