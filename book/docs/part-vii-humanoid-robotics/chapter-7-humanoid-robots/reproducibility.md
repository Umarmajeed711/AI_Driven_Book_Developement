# Reproducibility Guide for Chapter: Humanoid Robots

**Chapter Number**: Part VII - Chapter 7  
**Date Generated**: 2025-12-23  
**Purpose**: This document outlines the precise steps and environment configurations required to reproduce the hands-on exercises and code examples presented in Chapter Part VII - Chapter 7. Adhering to these guidelines is crucial for replicating results and ensuring a consistent learning experience.

---

## 1. System Requirements

The following operating system and software versions are recommended for optimal reproducibility.

-   **Operating System**: Ubuntu LTS (e.g., Ubuntu 22.04 LTS)
-   **Python Version**: 3.10
-   **ROS / Simulator Version**: Specific ROS 2 distribution (e.g., Humble Hawksbill) / Gazebo version compatible with ROS 2 (e.g., Gazebo Garden)
-   **Hardware Assumptions**: None explicitly mentioned.

## 2. Setup Instructions

Follow these steps to prepare your development environment.

### 2.1. Operating System Setup

If not already running, set up a clean installation of **Ubuntu LTS (e.g., Ubuntu 22.04 LTS)**. Virtual machines (e.g., VirtualBox, VMware) or WSL2 (Windows Subsystem for Linux 2) are viable options if you are on a different host OS.

### 2.2. ROS 2 and Simulator Installation

Install the specified ROS 2 distribution and simulator. Refer to the official documentation for the most up-to-date instructions.

**ROS 2 Humble Hawksbill**:
```bash
# Example for Ubuntu 22.04 LTS (Humble Hawksbill)
# Follow official ROS 2 Humble installation guide:
# https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html
# ... (insert specific commands from official docs) ...
source /opt/ros/humble/setup.bash
```

**Simulator Gazebo Garden**:
```bash
# Follow official Gazebo Garden installation guide:
# https://gazebosim.org/docs/garden/install_ubuntu
# Or install via ROS 2 if using `ros-humble-desktop` as it typically includes Gazebo.
```

### 2.3. Python Environment Setup

Ensure Python 3.10 is installed and set up. It's recommended to use a virtual environment to manage project dependencies.

```bash
# Example for Python 3.10
sudo apt update
sudo apt install python3.10 python3.10-venv
# Create and activate a virtual environment
python3.10 -m venv ~/chapter-7-humanoid-robots_venv
source ~/chapter-7-humanoid-robots_venv/bin/activate
```

### 2.4. Python Library Installation

Install the required Python libraries using `pip`.

```bash
source ~/chapter-7-humanoid-robots_venv/bin/activate # Activate if not already active
# Specific libraries for this chapter:
pip install numpy matplotlib
# You will also need ROS 2 Python client libraries (rclpy) which comes with ROS 2 installation.
# And potentially specific ROS 2 packages for humanoid models (e.g., `ros-humble-humanoid-robot-description`).
```

### 2.5. Additional Software/Dependencies

-   **ROS 2 Humanoid Model Packages**: Install relevant ROS 2 packages that provide URDFs and Gazebo simulation setups for humanoid robots (e.g., `ros-humble-humanoid-robot-description` or specific robot packages).

## 3. Hands-On Exercise Setup

For each practical exercise (`PRAC-XX`), detailed setup steps are provided here. This may include cloning specific repositories, downloading datasets, or compiling custom ROS 2 packages.

### PRAC-01: Humanoid Model in Simulation

**Description**: Load a humanoid robot model (e.g., a simple biped) into a simulator like Gazebo. Command individual joints to observe kinematics and initial balance challenges.

**Steps**:
1.  **Install ROS 2 and Gazebo**: Follow instructions in Section 2.2.
2.  **Install Humanoid Robot Package**: Install a ROS 2 package that provides a humanoid model for Gazebo. For example, search for `ros-humble-humanoid-robot-description` or a similar package that provides a simple bipedal model.
    ```bash
    sudo apt install ros-humble-humanoid-robot-description # Example package
    ```
3.  **Launch Humanoid in Gazebo**: Use the appropriate launch file provided by the package.
    ```bash
    ros2 launch humanoid_robot_description display_humanoid.launch.py # Example launch
    ```
    (Note: Specific launch commands will depend on the chosen humanoid package.)
4.  **Command Joints**: Use `ros2 control` commands or a simple ROS 2 Python node to publish joint commands and observe the robot's kinematics.

**Validation Steps**: Successful loading and visualization of humanoid model in Gazebo, and ability to command its joints.

### PRAC-02: Simple Balance Control (Conceptual/Visualization)

**Description**: Implement a basic script to visualize the ZMP and CoM for a humanoid model in simulation. Demonstrate a simple reactive balance controller (e.g., shifting weight based on lean angle).

**Steps**:
1.  **Ensure PRAC-01 setup is complete**.
2.  **Develop Python Script**: Write a Python script (ROS 2 node) that:
    *   Subscribes to joint state data from the simulated humanoid.
    *   Calculates the Center of Mass (CoM) based on link masses and current joint positions (simplified).
    *   Calculates the Zero Moment Point (ZMP) (simplified, based on foot contact points and CoM projection).
    *   Publishes visualization markers (e.g., `visualization_msgs/MarkerArray`) to `rviz` to show CoM and ZMP.
    *   For a simple reactive controller, publish small joint position adjustments based on CoM/ZMP deviation from the center of the support polygon.

**Validation Steps**: Visualization of CoM and ZMP in `rviz`, and the simulated humanoid demonstrating basic reactive balance control.

## 4. Troubleshooting

-   **Common Issue 1**: Humanoid model not loading or appearing incorrectly in Gazebo.
    -   **Solution**: Verify the installation of the humanoid robot description package. Check the launch file for correct paths and configurations. Ensure ROS 2 environment is sourced.
-   **Common Issue 2**: `ros2 control` commands not working for the humanoid.
    -   **Solution**: Ensure the `ros2_control` framework is properly set up for the humanoid model and that the controllers are loaded and active. Consult the documentation for the specific humanoid model you are using.
-   **Common Issue 3**: Python scripts for CoM/ZMP visualization or balance control are not working.
    -   **Solution**: Check for correct ROS 2 topic subscriptions and publications. Verify the mathematical calculations for CoM and ZMP. Ensure `rclpy` and `numpy` are correctly imported and used.

---

**Note**: If you encounter issues not covered here, please refer to the official documentation of the respective tools or consult the community forums.
