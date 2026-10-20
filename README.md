# linux_docker

Docker configurations for Linux development.

## ROS 2 Development Environment

`ros2-rviz/` provides ROS 2 Humble with RViz, MoveIt, Joint State Publisher, Gazebo ROS integration, and Controller Manager.

### Setup

Requires Docker Compose and an X11-compatible desktop session. Set `DISPLAY` and `XAUTHORITY` to your current session values, and update the host workspace path in `compose.yaml` if needed (default: `/home/harry/dobot_ws/src`).

```bash
cd ros2-rviz
docker compose up -d --build
docker compose exec rviz bash
```

Launch RViz inside the container:

```bash
source /opt/ros/humble/setup.bash
rviz2
```

### Workspace

(This is just for test the environment by a moveit demo)
https://github.com/harryshi0920/dobot_ws
Source files are mounted read-only at `/workspaces/dobot_ws/src`; edit them on the host. Build, install, and log directories persist in Docker volumes.

```bash
# Inside the container
cd /workspaces/dobot_ws
source /opt/ros/humble/setup.bash
colcon build --symlink-install
source install/setup.bash
```

Stop the environment with `docker compose down` from `ros2-rviz/`.

**Note:** The image is currently tagged `ros2-rviz:jazzy`, but the Dockerfile uses **Humble**. Software rendering is enabled by default.
