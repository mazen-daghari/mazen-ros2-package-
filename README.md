# mazen-ros2-package-
4-wheeled robot project using ROS 2 Foxy, LiDAR, camera sensors, SLAM, AMCL, Nav2, and YOLO for object recognition

> Autonomous 4-wheeled robot powered by ROS 2 Foxy, featuring SLAM, navigation, obstacle avoidance, and YOLO-based real-time object recognition.

---

## 📦 Features

- 🔁 **4-Wheel Drive Mobility** (CAN or skid steering)
- 🧭 **SLAM Toolbox**: Real-time map building
- 🧠 **Nav2**: Path planning and autonomous navigation
- 🎯 **AMCL**: Localization within known maps
- 🌐 **LiDAR**: 2D environment scanning (RPLidar, Hokuyo, etc.)
- 🎥 **RGB Camera**: Object detection via YOLOv8
- 📡 **TF Tree**: Full static and dynamic transforms
- 🕹️ **Teleop**: Keyboard or joystick control
- 📊 **RViz 2**: Visualization of robot state and sensor data

---

## 🖼️ System Architecture

```text
             +--------------------------+
             |      Teleop Input        |
             +------------+-------------+
                          |
                          v
               +----------+----------+
               |      /cmd_vel       |
               +----------+----------+
                          |
                          v
+-----------------+   +----------------+   +------------------+
| robot_state_pub |-->| joint_states   |-->| TF: base -> wheels|
+-----------------+   +----------------+   +------------------+
                          |
                          v
+------------+   +------------+   +--------------+
| LiDAR Node |   | Camera Node|   | YOLOv8 Node  |
+------------+   +------------+   +--------------+
     |                 |                  |
     v                 v                  v
 /scan          /image_raw        /inference_result
     |                 |                  |
     +-----------------+------------------+
                          |
                          v
                  +---------------+
                  |   SLAM / AMCL |
                  +---------------+
                          |
                          v
                  +---------------+
                  |     Nav2      |
                  +---------------+
🧰 Requirements
Ubuntu 20.04

ROS 2 Foxy

slam_toolbox

nav2_bringup

robot_state_publisher

joint_state_publisher

rplidar_ros or your preferred LiDAR driver

usb_cam / custom camera node

yolov8_ros or YOLO custom wrapper (integrated using cv_bridge + image_transport)


1. Clone the Repo

mkdir -p ~/mazen_ws/src
cd ~/mazen_ws/src
git clone https://github.com/mazen-daghari/mazen-ros2-package-.git
cd ..
colcon build
source install/setup.bash
2. Launch SLAM Mode

ros2 launch slam_toolbox online_async_launch.py use_sim_time:=True

3. Launch NAV2 (Navigation) Mode

ros2 launch nav2_bringup navigation_launch.py use_sim_time:=True

4. Start YOLO Inference

ros2 launch yolobot_recognition launch_yolov8.launch.py


📂 Project Structure

nomade_rover/
├── launch/
│   ├── bringup_slam.launch.py
│   ├── bringup_nav.launch.py
│   ├── yolov8_inference.launch.py
│   └── robot_state.launch.py
├── urdf/
│   └── nomade_robot.urdf.xacro
├── config/
│   ├── nav2_params.yaml
│   ├── slam_toolbox.yaml
│   └── amcl.yaml
├── scripts/
│   └── yolov8_node.py
├── maps/
│   └── map.yaml
├── rviz/
│   └── navigation.rviz
└── README.md



🛠️ TODO
 Add joystick teleop support

 Integrate depth camera for better obstacle awareness

 Multi-robot exploration

 Web interface for remote monitoring

🤖 Example Video
📹 Coming soon!

🧑‍💻 Maintainers
Mazen Daghari
LinkedIn | GitHub
📧 dagmazen@gmail.com

📝 License
This project is licensed under the MIT License.
