# ROS 2 Navigation FAST-LIO GPL Derivatives

This repository publishes the complete source used for the two GPL-2.0-only
FAST-LIO runtime units required by the LimX ROS 2 navigation integration:

- `FAST_LIO`: ROS 2 mapping/LIO derivative;
- `FAST_LIO_LOCALIZATION2`: ROS 2 map-localization derivative.

Both directories include their embedded `ikd-Tree` source, package build files,
GPLv2 license text, upstream attribution, baseline commit, and local modification
notice. No license in this repository is changed to Apache or BSD.

## Source snapshot

This is the complete source snapshot expected by the companion LimX ROS 2
navigation integration. The public upstream commits document its provenance,
but they are not drop-in replacements for these ROS 2 Humble and RoboSense
derivatives.

See [RELEASE_INFO.md](RELEASE_INFO.md), [FAST_LIO/NOTICE](FAST_LIO/NOTICE), and
[FAST_LIO_LOCALIZATION2/NOTICE](FAST_LIO_LOCALIZATION2/NOTICE) for exact
provenance and modification scope.

## Build

Prerequisites are ROS 2 Humble, `colcon`, PCL, Eigen, and the dependencies named
in both package manifests. On Ubuntu 22.04 aarch64, source ROS and build into an
independent GPL install prefix:

```bash
source /opt/ros/humble/setup.bash
colcon build \
  --base-paths FAST_LIO FAST_LIO_LOCALIZATION2 \
  --packages-select fast_lio fast_lio_localization \
  --build-base build \
  --install-base install \
  --merge-install \
  --symlink-install \
  --cmake-force-configure \
  --cmake-args -DCMAKE_BUILD_TYPE=Release
```

For RoboSense RSFAIRY operation, build and source the separately licensed
RSLIDAR packages before runtime. The expected standard ROS 2 interfaces are
`/rslidar_points` (`sensor_msgs/PointCloud2`) and `/rslidar_imu_data`
(`sensor_msgs/Imu`). Site calibration, maps, robot credentials, generated
binaries, and install prefixes are intentionally absent.

## Integration boundary

The full navigation system checks out this GPL repository separately from the
permissive integration repository and builds it into a separate prefix. Runtime
communication with RSLIDAR, PCT, and SCAN uses ROS 2/DDS messages and TF. This
engineering boundary does not alter GPL obligations or determine a legal
aggregation/derivative-work question.

Companion repositories:

- <https://github.com/limxdynamics/tron2-navigation-ros2>
- <https://github.com/1392559136a-jpg/tron2-navigation-pct-gpl>

## License

The derivative programs are distributed under GNU GPL version 2 only. Read the
root [LICENSE](LICENSE), each component's `LICENSE`, and both `NOTICE` files.
The software is provided without warranty.
