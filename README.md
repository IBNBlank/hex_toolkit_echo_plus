
# **hex_toolkit_echo_plus**

## **Overview**

The **hex_toolkit_echo_plus** package provides a suite of tools for **Echo Plus**, including URDF models and a simple MPC (Model Predictive Control) demo.

### **Maintainer**

**Dong Zhaorui**: [847235539@qq.com](mailto:847235539@qq.com)

### **Verified Platforms**

- [x] **x64**
- [ ] **Jetson Orin Nano**
- [x] **Jetson Orin NX**
- [ ] **Jetson AGX Orin**
- [ ] **Horizon RDK X5**
- [ ] **Rockchip RK3588**

### **Verified ROS Versions**

- [x] **Noetic**
- [x] **Humble**
- [ ] **Jazzy**

---

## **Getting Started**

### **Dependencies**

For **Hex Chassis** users, we highly recommend using this package within our **Hex Docker Images** to ensure compatibility and an optimized setup experience.

If you choose to set up manually, please install the following dependencies:

1. **ROS/ROS2**  
   Follow the official [ROS Installation Guide](http://wiki.ros.org/ROS/Installation) or the [ROS2 Installation Guide](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html).

2. **hex_toolkit_general_chassis**  
   Follow the official [Installation Guide](https://github.com/hexfellow/hex_toolkit_general_chassis.git).

3. **acados**  
   Follow the official [Installation Guide](https://docs.acados.org/installation/index.html).

### **Installation**

1. Create a ROS workspace and navigate to the `src` directory:

   ```bash
   mkdir -p catkin_ws/src
   cd catkin_ws/src
   ```

2. Clone the required repositories:

   ```bash
   git clone https://github.com/hexfellow/hex_toolkit_general_chassis.git
   git clone https://github.com/hexfellow/hex_toolkit_echo_plus.git
   ```

3. Build the workspace:

   - **ROS 1**:

     ```bash
     cd ../
     catkin_make
     ```

   - **ROS 2**:

     ```bash
     cd ../
     colcon build
     ```

### **Pre-Execution Steps**

Source the appropriate setup file based on your ROS version:

- **ROS 1**:

  ```bash
  source devel/setup.bash --extend
  ```

- **ROS 2**:

  ```bash
  source install/setup.bash --extend
  ```

---

## **Nodes**

The package provides the following nodes:

- **Mpc Track**: Using MPC to follow target pose.

---

### **Mpc Track**

The **Mpc Track** node employs Model Predictive Control to track target poses.

#### **Published Topics**

| Topic Name     | Message Type                 | Description                                    |
| -------------- | ---------------------------- | ---------------------------------------------- |
| `/unsafe_ctrl` | `geometry_msgs/Twist`        | Publishes `twist` commands without timestamps. |
| `/vel_ctrl`    | `geometry_msgs/TwistStamped` | Publishes `twist` commands with timestamps.    |

#### **Subscribed Topics**

| Topic Name      | Message Type                | Description                         |
| --------------- | --------------------------- | ----------------------------------- |
| `/chassis_odom` | `nav_msgs/Odometry`         | Subscribes to chassis odometry.     |
| `/target_pose`  | `geometry_msgs/PoseStamped` | Subscribes to target poses.         |

#### **Parameters**

| Parameter Name      | Data Type        | Description                                   |
| ------------------- | ---------------- | --------------------------------------------- |
| `rate_ros`          | `double`         | Execution rate of the ROS node (Hz).          |
| `rate_odom`         | `double`         | Odometry rate of the chassis driver (Hz).     |
| `rate_mpc`          | `double`         | Execution rate of the MPC (Hz).               |
| `model_base`        | `string`         | Frame ID of the chassis base.                 |
| `model_odom`        | `string`         | Frame ID of the odometry.                     |
| `model_track_width` | `double`         | Track width of the chassis (m).               |
| `limit_vel`         | `vector<double>` | Velocity limits of the chassis (m/s).         |
| `limit_acc`         | `vector<double>` | Acceleration limits of the chassis (m/s²).    |
| `obs_weights`       | `double`         | State observer weights.                       |
| `mpc_window`        | `int`            | MPC window size.                              |
| `mpc_vel`           | `vector<double>` | MPC wheel velocity limits (m/s).              |
| `mpc_ctrl`          | `vector<double>` | MPC wheel acceleration limits (m/s²).         |
| `mpc_mid_wt`        | `vector<double>` | Weights for MPC mid-points.                   |
| `mpc_end_wt`        | `vector<double>` | Weights for MPC end-points.                   |

---

## **Launch Files**

The package provides the following launch files:

- **Bringup**: **Echo Plus** driver.
- **Joy Ctrl**: **Echo Plus** driver with gamepad control.
- **Key Ctrl**: **Echo Plus** driver with keyboard control.
- **MPC Track**: **Echo Plus** driver with MPC for trajectory following.

---

### **Bringup**

#### **Introduction**

Bringup **Echo Plus**.

#### **Usage**

- **ROS 1**:

  ```bash
  roslaunch hex_toolkit_echo_plus bringup.launch
  ```

- **ROS 2**:

  ```bash
  ros2 launch hex_toolkit_echo_plus bringup.launch.py
  ```

---

### **Joy Ctrl**

#### **Introduction**

Bringup **Echo Plus** and control the chassis using a gamepad.

#### **Usage**

- **ROS 1**:

  ```bash
  roslaunch hex_toolkit_echo_plus joy_ctrl.launch
  ```

- **ROS 2**:

  ```bash
  ros2 launch hex_toolkit_echo_plus joy_ctrl.launch.py
  ```

---

### **Key Ctrl**

#### **Introduction**

Bringup **Echo Plus** and control the chassis using the keyboard.

#### **Usage**

- **ROS 1**:

  ```bash
  roslaunch hex_toolkit_echo_plus key_ctrl.launch
  ```

- **ROS 2**:

  ```bash
  ros2 launch hex_toolkit_echo_plus key_ctrl.launch.py
  ```

---

### **Mpc Track**

#### **Introduction**

Bringup **Echo Plus** and use MPC to follow a trajectory for testing.

#### **Usage**

- **ROS 1**:

  ```bash
  roslaunch hex_toolkit_echo_plus mpc_track.launch
  ```

- **ROS 2**:

  ```bash
  ros2 launch hex_toolkit_echo_plus mpc_track.launch.py
  ```