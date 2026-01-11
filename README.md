

---

```markdown
# Custom Mobile Robot Simulation (ROS 2 & Gazebo)

This project simulates a differential drive mobile robot using **ROS 2 Jazzy** and **Gazebo**. It consists of a custom robot description (URDF/Xacro) and a bringup package that handles the simulation environment, physics bridges, and sensor data.

## 📂 Project Structure

* **`my_robot_description`**: Contains the URDF, Xacro files, and meshes defining the robot's physical structure, collision geometry, and Gazebo plugins.
* **`my_robot_bringup`**: Contains launch files, simulation world (`.sdf`), and configuration files for the ROS-Gazebo bridge.

## ⚙️ Prerequisites

* **OS:** Ubuntu 24.04 (Noble Numbat)
* **ROS 2 Distro:** Jazzy Jalisco
* **Simulator:** Gazebo (Garden/Harmony)

### Required Packages
Ensure you have the necessary dependencies installed:

```bash
sudo apt update
sudo apt install ros-jazzy-ros-gz \
                 ros-jazzy-teleop-twist-keyboard \
                 ros-jazzy-robot-state-publisher \
                 ros-jazzy-joint-state-publisher \
                 ros-jazzy-xacro

```

## 🛠️ Installation & Build

1. **Create a Workspace (if you haven't already):**
```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src

```


2. **Clone this Repository:**
```bash
git clone <YOUR_REPO_URL_HERE> .

```


3. **Build the Packages:**
```bash
cd ~/ros2_ws
colcon build --symlink-install

```


4. **Source the Workspace:**
```bash
source install/setup.bash

```



## 🚀 Usage

### 1. Setup Environment Variables

Gazebo needs to know where to look for your custom meshes. Run this command in your terminal before launching (or add it to your `~/.bashrc`):

```bash
export GZ_SIM_RESOURCE_PATH=$GZ_SIM_RESOURCE_PATH:$(ros2 pkg prefix my_robot_description)/share

```

### 2. Launch the Simulation

This command launches Gazebo, spawns the robot, starts the `robot_state_publisher`, and sets up the ROS-Gazebo bridge.

```bash
ros2 launch my_robot_bringup my_robot_gazebo.launch.xml

```

*Note: If the robot does not appear immediately, ensure the simulation is not paused in Gazebo (press the Play button in the bottom left).*

### 3. Control the Robot (Teleop)

To drive the robot, open a **new terminal** window and run the teleoperation node:

```bash
source ~/ros2_ws/install/setup.bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard

```

**Controls:**

* **`i`**: Move Forward
* **`,`**: Move Backward
* **`j`**: Turn Left
* **`l`**: Turn Right
* **`k`**: Stop
* **`q` / `z**`: Increase / Decrease Max Speed

## 🔧 Troubleshooting

* **"Mesh not found" or "URI not resolved":**
Ensure you ran the `export GZ_SIM_RESOURCE_PATH` command mentioned in step 1.
* **Robot is not moving:**
* Check that the simulation is playing (not paused).
* Ensure the `teleop_twist_keyboard` terminal is active/focused.
* Verify that your speed is not set to 0.0 (check the teleop terminal output).


* **RViz errors (No Transform):**
Ensure `robot_state_publisher` is running and that the Gazebo bridge is successfully publishing to `/joint_states` and `/tf`.

```

```
