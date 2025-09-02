# Week 2 Task: ROS2 Topics & Teleoperation with TurtleBot3

## 🙋 Submitted By

- **Name:** Fatin Najihah Binti Mat Ali  
- **Student ID:** 2024853488

## 📁 Repository Structure

/week2_task_ros2/
├── README.md
├── img/
│ ├── gazebo.png
│ ├── teleop.png
│ ├── topic_list.png
│ ├── odom_echo.png
│ ├── scan_hz.png
│ ├── rviz.png
│ └── bag_replay.png
├── ros2_bag_info.txt
├── reflection.pdf
└── video/
└── teleop_demo.mp4

---

## 🛠 Requirements

- Ubuntu **22.04 LTS**
- ROS2 **Humble** (desktop install)
- TurtleBot3 packages installed
- **Gazebo Classic** + **RViz2**
- **Screen Recorder**: OBS Studio or Ubuntu built-in (`Ctrl+Alt+Shift+R`)

---

## 🧪 ROS2 Communication Overview (Mobile Robot Example)

- **Nodes** (components):
  - `teleop_keyboard`: sends velocity commands
  - `gazebo_ros`: simulates physics
  - `robot_state_publisher`: publishes transforms
  - `lidar`: scans environment
  - `rviz2`: visualizes data

- **Topics** (communication channels):
  - `/cmd_vel`: velocity commands → controls wheels
  - `/odom`: robot position & orientation
  - `/scan`: LIDAR scan of surroundings

- **Messages**:
  - `/cmd_vel`: `geometry_msgs/msg/Twist`
  - `/odom`: `nav_msgs/msg/Odometry`
  - `/scan`: `sensor_msgs/msg/LaserScan`

**Example Flow:**

> Press `W` → `teleop_keyboard` node publishes `/cmd_vel` → Gazebo simulates motion → Odometry updates `/odom` → LIDAR scans `/scan` → RViz2 visualizes everything.

---

## 📋 Step-by-Step Instructions

### 1️⃣ Launch Simulation in Gazebo

```bash
export TURTLEBOT3_MODEL=burger
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```


### 2️⃣ Teleoperate the Robot (New Terminal)

```bash
ros2 run turtlebot3_teleop teleop_keyboard
```

Use keys W, A, S, D, and X to move the robot.

### 3️⃣ Explore Topics

```bash
ros2 topic list
ros2 topic info /cmd_vel
ros2 topic echo /odom --once
ros2 topic hz /scan
```

### 4️⃣ Inspect Message Types

```bash
ros2 interface show geometry_msgs/msg/Twist
ros2 interface show sensor_msgs/msg/LaserScan
```

### 5️⃣ Visualize in RViz2 (New Terminal)

```bash
rviz2
```

Add these displays in RViz2:

TF

RobotModel

LaserScan → Topic: /scan

Odometry → Topic: /odom


### 6️⃣ Record & Replay Data (New Terminal)

🔴 Record:

```bash
ros2 bag record /scan /odom /cmd_vel
```

Use the teleop window to move the robot for about 2 minutes.

Press Ctrl + C to stop recording.

▶️ Replay:

```bash
ros2 bag play rosbag2_2025_09_02-11_02_33
```

Make sure Gazebo is running while playing the bag.

If playback is slow, try increasing the rate:

```bash
ros2 bag play rosbag2_2025_09_02-11_02_33 --rate 2.0 --read-ahead-queue-size 1000
```

📄 View Bag Info:

```bash
ros2 bag info rosbag2_2025_09_02-11_02_33
```
