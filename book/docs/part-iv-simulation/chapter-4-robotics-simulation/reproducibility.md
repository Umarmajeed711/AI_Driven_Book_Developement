# Reproducibility Guide for Chapter: Robotics Simulation

**Chapter Number**: Part IV - Chapter 4  
**Date Generated**: 2025-12-24  
**Purpose**: This document outlines the precise steps and environment configurations required to reproduce the hands-on exercises and code examples presented in Chapter 4. Adhering to these guidelines is crucial for replicating results and ensuring a consistent learning experience.

---

## 1. System Requirements

The following operating system and software versions are recommended for optimal reproducibility.

-   **Operating System**: Ubuntu LTS (e.g., Ubuntu 22.04 LTS)
-   **Python Version**: As required by the ROS 2 distribution (e.g., 3.10)
-   **ROS / Simulator Version**: ROS 2 Humble Hawksbill / Gazebo Garden
-   **Hardware Assumptions**: None

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
# (Assuming ROS 2 is already installed from Chapter 3 setup)
source /opt/ros/humble/setup.bash
```

**Simulator Gazebo Garden**:
```bash
# Example for Gazebo Garden
# Follow official Gazebo Garden installation guide:
# https://classic.gazebosim.org/tutorials?tut=install_ubuntu&cat=install
sudo apt update
sudo apt install gazebo
# For ROS 2 integration, typically install ros-humble-gazebo-ros-pkgs
sudo apt install ros-humble-gazebo-ros-pkgs
```

### 2.3. Python Environment Setup

Ensure the specified Python version is installed and set up. It's recommended to use a virtual environment to manage project dependencies.

```bash
# Example for Python 3.10
# (Assuming Python 3.10 and venv are set up from Chapter 3)
source ~/ch003_ros2_fundamentals_venv/bin/activate # Activate virtual environment from Chapter 3
# If a new venv is preferred for this chapter:
# python3.10 -m venv ~/ch004_robotics_simulation_venv
# source ~/ch004_robotics_simulation_venv/bin/activate
```

### 2.4. Python Library Installation

Install the required Python libraries using `pip`.

```bash
source ~/ch003_ros2_fundamentals_venv/bin/activate # Activate if not already active
# Specific libraries for this chapter:
# No additional Python libraries beyond ROS 2 Python packages mentioned in spec.
```

### 2.5. Additional Software/Dependencies

If there are any other specific software or dependencies required, list them here.

- URDF model files (e.g., for a simple robot, often available in ROS 2 example packages or from community).

## 3. Hands-On Exercise Setup

For each practical exercise (`PRAC-XX`), detailed setup steps are provided here. This may include cloning specific repositories, downloading datasets, or compiling custom ROS 2 packages.

### PRAC-01: Simulator Setup

**Description**: Installation and basic configuration of a chosen simulator (e.g., Gazebo).

**Steps**:
1.  Follow the instructions in Section 2.2 for installing Gazebo.
2.  Launch Gazebo:
    ```bash
    gazebo
    ```
    or for an empty world with ROS 2 integration:
    ```bash
    ros2 launch gazebo_ros gazebo.launch.py
    ```

**Validation Steps**: Gazebo GUI launches successfully, showing an empty world.

### PRAC-02: Load and Run a Simple Robot Model

**Description**: Load a pre-existing URDF (Unified Robot Description Format) model into the simulator.

**Steps**:
1.  Ensure Gazebo and ROS 2 environment are sourced.
2.  Launch Gazebo with a simple robot model (e.g., from `gazebo_ros_pkgs` or a custom package):
    ```bash
    ros2 launch gazebo_ros_pkgs diff_drive_robot.launch.py # Example for a differential drive robot
    ```
    (Note: Specific launch file will depend on the robot model chosen for the chapter content).

**Validation Steps**: The robot model appears in the Gazebo simulation environment. You should be able to interact with its joints (e.g., via `ros2 topic pub` commands or a GUI plugin).

### PRAC-03: Basic Environment Interaction

**Description**: Add simple objects to the simulation environment and observe interactions.

**Steps**:
1.  With Gazebo and your robot model running (from PRAC-02), use the Gazebo GUI to insert simple shapes (e.g., cubes, spheres) into the world.
2.  Observe how the robot and objects interact (e.g., collision, pushing).
3.  Alternatively, use ROS 2 commands to spawn models into Gazebo (requires `ros_gz_sim` bridge or similar).
    ```bash
    ros2 run gazebo_ros spawn_entity.py -entity my_box -file /path/to/my_box.urdf
    ```

**Validation Steps**: Objects can be added to the simulation and interact physically with the robot and environment.

## 4. Troubleshooting

-   **Common Issue 1**: Gazebo fails to launch or crashes.
    -   **Solution**: Check your graphics drivers. Ensure `gazebo` and `ros-humble-gazebo-ros-pkgs` (or your chosen ROS 2-Gazebo bridge) are correctly installed. Try launching with `gazebo --verbose` for more debug information.
-   **Common Issue 2**: Robot model does not appear in Gazebo.
    -   **Solution**: Verify the URDF path is correct in the launch file. Ensure `ros-humble-xacro` is installed if using `.xacro` files. Check for error messages in the terminal where Gazebo was launched.

---

**Note**: If you encounter issues not covered here, please refer to the official documentation of the respective tools or consult the community forums.