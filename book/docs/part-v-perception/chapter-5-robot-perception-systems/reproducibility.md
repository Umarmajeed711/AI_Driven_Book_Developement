# Reproducibility Guide for Chapter: Robot Perception Systems

**Chapter Number**: Part V - Chapter 5  
**Date Generated**: 2025-12-24  
**Purpose**: This document outlines the precise steps and environment configurations required to reproduce the hands-on exercises and code examples presented in Chapter 5. Adhering to these guidelines is crucial for replicating results and ensuring a consistent learning experience.

---

## 1. System Requirements

The following operating system and software versions are recommended for optimal reproducibility.

-   **Operating System**: Ubuntu LTS (e.g., Ubuntu 22.04 LTS)
-   **Python Version**: 3.10
-   **ROS / Simulator Version**: ROS 2 Humble Hawksbill (for rviz visualization, if used)
-   **Hardware Assumptions**: None (all exercises can be done with pre-recorded datasets)

## 2. Setup Instructions

Follow these steps to prepare your development environment.

### 2.1. Operating System Setup

If not already running, set up a clean installation of **Ubuntu LTS (e.g., Ubuntu 22.04 LTS)**. Virtual machines (e.g., VirtualBox, VMware) or WSL2 (Windows Subsystem for Linux 2) are viable options if you are on a different host OS.

### 2.2. ROS 2 and Simulator Installation

Install the specified ROS 2 distribution if `rviz` or other ROS 2 visualization tools are to be used. Otherwise, it's optional for this chapter's Python-focused practicals.

**ROS 2 Humble Hawksbill (Optional)**:
```bash
# Example for Ubuntu 22.04 LTS (Humble Hawksbill)
# Follow official ROS 2 Humble installation guide:
# https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html
# (If not installed in previous chapters)
sudo apt install ros-humble-desktop -y # Installs rviz2
source /opt/ros/humble/setup.bash
```

**Simulator Not Applicable**:
```bash
# No specific simulator is required, as this chapter uses pre-recorded data.
```

### 2.3. Python Environment Setup

Ensure the specified Python version is installed and set up. It's recommended to use a virtual environment to manage project dependencies.

```bash
# Example for Python 3.10
# (Assuming Python 3.10 and venv are set up from Chapter 3/4)
source ~/ch003_ros2_fundamentals_venv/bin/activate # Activate virtual environment from Chapter 3
# If a new venv is preferred for this chapter:
# python3.10 -m venv ~/ch005_robot_perception_venv
# source ~/ch005_robot_perception_venv/bin/activate
```

### 2.4. Python Library Installation

Install the required Python libraries using `pip`.

```bash
source ~/ch003_ros2_fundamentals_venv/bin/activate # Activate if not already active
# Specific libraries for this chapter:
pip install opencv-python numpy matplotlib
```

### 2.5. Additional Software/Dependencies

If there are any other specific software or dependencies required, list them here.

- Fixed Dataset: Download the chapter's specific pre-recorded sensor datasets from [URL TO DATASET - Placeholder].

## 3. Hands-On Exercise Setup

For each practical exercise (`PRAC-XX`), detailed setup steps are provided here. This may include cloning specific repositories, downloading datasets, or compiling custom ROS 2 packages.

### PRAC-01: Sensor Data Visualization

**Description**: Use simple tools (e.g., Python scripts with Matplotlib, or ROS 2 visualization tools like `rviz`) to load and visualize example data from cameras, LiDAR, and IMUs (pre-recorded datasets).

**Steps**:
1.  Download the provided fixed dataset (see Section 2.5).
2.  Navigate to the chapter's code directory:
    ```bash
    cd ~/robot_perception_chapter_code/
    ```
3.  Run the Python visualization scripts:
    ```bash
    python visualize_camera.py --data_path /path/to/downloaded/camera_data.bag
    python visualize_lidar.py --data_path /path/to/downloaded/lidar_data.csv
    python visualize_imu.py --data_path /path/to/downloaded/imu_data.csv
    ```
    (Note: Replace script names and data paths with actual ones provided in chapter content)
4.  Alternatively, if using ROS 2, launch `rviz2` and load the configuration file provided:
    ```bash
    source /opt/ros/humble/setup.bash
    rviz2 -d path/to/chapter_config.rviz
    ```
    Then, play back the ROS 2 bag file containing the recorded sensor data.

**Validation Steps**: Camera images, LiDAR plots, and IMU orientation graphs are displayed correctly. `rviz2` shows the sensor data as expected.

### PRAC-02: Basic Image Processing with OpenCV

**Description**: Load an image, apply basic filters (grayscale, blur), detect edges. (Using pre-recorded images).

**Steps**:
1.  Ensure OpenCV is installed (see Section 2.4).
2.  Navigate to the chapter's code directory.
3.  Run the image processing script:
    ```bash
    python basic_image_processing.py --image_path /path/to/downloaded/example_image.png
    ```
    (Note: Replace script name and image path with actual ones provided in chapter content).

**Validation Steps**: Processed images (grayscale, blurred, edge-detected) are displayed or saved correctly.

## 4. Troubleshooting

-   **Common Issue 1**: `ModuleNotFoundError` for Python packages.
    -   **Solution**: Ensure you have activated your virtual environment and installed all required packages (`pip install opencv-python numpy matplotlib`).
-   **Common Issue 2**: `rviz2` does not show data or crashes.
    -   **Solution**: Check that the ROS 2 environment is sourced. Verify that the ROS 2 bag file is being played correctly and that the topics are correctly configured in `rviz2`.

---

**Note**: If you encounter issues not covered here, please refer to the official documentation of the respective tools or consult the community forums.