# Reproducibility Guide for Chapter: {{CHAPTER_TITLE}}

**Chapter Number**: {{CHAPTER_NUMBER}}  
**Date Generated**: {{DATE_ISO}}  
**Purpose**: This document outlines the precise steps and environment configurations required to reproduce the hands-on exercises and code examples presented in Chapter {{CHAPTER_NUMBER}}. Adhering to these guidelines is crucial for replicating results and ensuring a consistent learning experience.

---

## 1. System Requirements

The following operating system and software versions are recommended for optimal reproducibility.

-   **Operating System**: {{OS_VERSION}}
-   **Python Version**: {{PYTHON_VERSION}}
-   **ROS / Simulator Version**: {{ROS_SIMULATOR_VERSION}}
-   **Hardware Assumptions**: {{HARDWARE_ASSUMPTIONS}}

## 2. Setup Instructions

Follow these steps to prepare your development environment.

### 2.1. Operating System Setup

If not already running, set up a clean installation of **{{OS_VERSION}}**. Virtual machines (e.g., VirtualBox, VMware) or WSL2 (Windows Subsystem for Linux 2) are viable options if you are on a different host OS.

### 2.2. ROS 2 and Simulator Installation

Install the specified ROS 2 distribution and simulator. Refer to the official documentation for the most up-to-date instructions.

**ROS 2 {{ROS_VERSION}}**:
```bash
# Example for Ubuntu 22.04 LTS (Humble Hawksbill)
# Follow official ROS 2 Humble installation guide:
# https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html
# ... (insert specific commands from official docs) ...
source /opt/ros/{{ROS_VERSION_LOWERCASE}}/setup.bash
```

**Simulator {{SIMULATOR_VERSION}}**:
```bash
# Example for Gazebo Garden
# Follow official Gazebo Garden installation guide:
# https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Configuring-ROS2-Environment.html
# ... (insert specific commands from official docs) ...
```

### 2.3. Python Environment Setup

Ensure the specified Python version is installed and set up. It's recommended to use a virtual environment to manage project dependencies.

```bash
# Example for Python 3.10
sudo apt update
sudo apt install python{{PYTHON_VERSION_MAJOR_MINOR}} python{{PYTHON_VERSION_MAJOR_MINOR}}-venv
# Create and activate a virtual environment
python{{PYTHON_VERSION_MAJOR_MINOR}} -m venv ~/{{CHAPTER_SLUG}}_venv
source ~/{{CHAPTER_SLUG}}_venv/bin/activate
```

### 2.4. Python Library Installation

Install the required Python libraries using `pip`.

```bash
source ~/{{CHAPTER_SLUG}}_venv/bin/activate # Activate if not already active
# Specific libraries for this chapter:
pip install {{PYTHON_LIBRARIES}}
```

### 2.5. Additional Software/Dependencies

If there are any other specific software or dependencies required, list them here.

- {{ADDITIONAL_SOFTWARE}}

## 3. Hands-On Exercise Setup

For each practical exercise (`PRAC-XX`), detailed setup steps are provided here. This may include cloning specific repositories, downloading datasets, or compiling custom ROS 2 packages.

### PRAC-XX: {{PRACTICAL_EXERCISE_TITLE}}

**Description**: {{PRACTICAL_EXERCISE_DESCRIPTION}}

**Steps**:
1.  {{STEP_1}}
2.  {{STEP_2}}
3.  ...

**Validation Steps**: {{VALIDATION_STEPS}}

## 4. Troubleshooting

-   **Common Issue 1**: {{ISSUE_DESCRIPTION}}
    -   **Solution**: {{SOLUTION_DESCRIPTION}}
-   **Common Issue 2**: {{ISSUE_DESCRIPTION}}
    -   **Solution**: {{SOLUTION_DESCRIPTION}}

---

**Note**: If you encounter issues not covered here, please refer to the official documentation of the respective tools or consult the community forums.
