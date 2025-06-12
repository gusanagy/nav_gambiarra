# nav_gambiarra
# Robot Navigation with Obstacle Avoidance

This ROS2 Python package implements a robot navigation system that can move through multiple waypoints while avoiding obstacles using laser scan data. The robot intelligently decides which direction to turn when avoiding obstacles based on the target position.

### Video

[project video on youtube](https://youtu.be/RBJtWjWMlUI)


## Features

- Waypoint navigation with configurable target positions
- Intelligent obstacle avoidance that considers target direction
- Real-time visualization of robot position and targets
- Smooth movement and turning behaviors
- Configurable parameters for navigation behavior

## Prerequisites

- ROS2 Humble (or newer)
- `stage_ros2` package for simulation
- Python 3.8+
- Required Python packages: `rclpy`, `numpy`, `matplotlib`

## Installation

1. Clone this repository into your ROS2 workspace `src` folder
2. Build the package:
   ```bash
   colcon build && source ~/.bashrc
   ```

## Usage

1. In one terminal, launch the Stage simulator:
   ```bash
   ros2 launch stage_ros2 stage.launch.py world:=new_cave use_stamped_velocity:=false
   ```

2. In another terminal, run the navigation node:
   ```bash
   ros2 run my_py_pkg nav_no_map
   ```

## Behavior Description

The robot will:
1. Navigate through predefined waypoints in sequence
2. Avoid obstacles by:
   - Checking laser scan data in front (30° left to 30° right)
   - Choosing the best escape direction based on target position
   - Backing up if an obstacle is too close
   - Turning in the optimal direction while moving away
3. Display real-time position and status in a matplotlib window
4. Stop when reaching the final waypoint

## Configuration

Key parameters can be adjusted in the `Navigation` class:
- `target_threshold`: Distance to consider target reached (0.5m)
- `obstacle_distance`: Minimum distance to trigger avoidance (0.6m)
- `escape_distance`: Safe distance before resuming navigation (1.0m)
- Waypoints can be modified in the `target_positions` list

## Visualization

The matplotlib window shows:
- Robot position (blue dot)
- Current target (green X)
- Completed targets (gray X)
- Final target (red/gold X)
- Robot orientation (blue arrow)
- Navigation status text

## Troubleshooting

If you encounter issues:
- Verify all packages are properly sourced
- Check that the simulator is publishing on `/odom` and `/base_scan`
- Ensure matplotlib can create windows (may need X11 forwarding if remote)