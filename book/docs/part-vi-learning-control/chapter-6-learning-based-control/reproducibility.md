# Reproducibility Guide for Chapter: Learning-Based Control

**Chapter Number**: Part VI - Chapter 6  
**Date Generated**: 2025-12-24  
**Purpose**: This document outlines the precise steps and environment configurations required to reproduce the hands-on exercises and code examples presented in Chapter 6. Adhering to these guidelines is crucial for replicating results and ensuring a consistent learning experience.

---

## 1. System Requirements

The following operating system and software versions are recommended for optimal reproducibility.

-   **Operating System**: Ubuntu LTS (e.g., Ubuntu 22.04 LTS)
-   **Python Version**: 3.10
-   **ROS / Simulator Version**: Not strictly required, but a basic simulated environment (e.g., OpenAI Gym) is used.
-   **Hardware Assumptions**: None

## 2. Setup Instructions

Follow these steps to prepare your development environment.

### 2.1. Operating System Setup

If not already running, set up a clean installation of **Ubuntu LTS (e.g., Ubuntu 22.04 LTS)**. Virtual machines (e.g., VirtualBox, VMware) or WSL2 (Windows Subsystem for Linux 2) are viable options if you are on a different host OS.

### 2.2. ROS 2 and Simulator Installation

ROS 2 is not strictly required for this chapter's practicals, but if you have it installed from previous chapters, it won't interfere. This chapter focuses on an RL environment.

**RL Environment Setup (OpenAI Gym example)**:
```bash
# OpenAI Gym is a toolkit for developing and comparing reinforcement learning algorithms.
# Install system dependencies for rendering if needed
sudo apt-get update
sudo apt-get install -y python3-dev libopenmpi-dev zlib1g-dev libgl1-mesa-glx
```

### 2.3. Python Environment Setup

Ensure the specified Python version is installed and set up. It's recommended to use a virtual environment to manage project dependencies.

```bash
# Example for Python 3.10
# (Assuming Python 3.10 and venv are set up from Chapter 3/4/5)
source ~/ch003_ros2_fundamentals_venv/bin/activate # Activate virtual environment from previous chapters
# If a new venv is preferred for this chapter:
# python3.10 -m venv ~/ch006_learning_control_venv
# source ~/ch006_learning_control_venv/bin/activate
```

### 2.4. Python Library Installation

Install the required Python libraries using `pip`.

```bash
source ~/ch003_ros2_fundamentals_venv/bin/activate # Activate if not already active
# Specific libraries for this chapter:
pip install gym[classic_control] numpy matplotlib # Example for CartPole environment
# If using a lightweight deep learning framework for policy networks (e.g., for PPO/SAC):
# pip install torch # or tensorflow
```

### 2.5. Additional Software/Dependencies

If there are any other specific software or dependencies required, list them here.

- None

## 3. Hands-On Exercise Setup

For each practical exercise (`PRAC-XX`), detailed setup steps are provided here. This may include cloning specific repositories, downloading datasets, or compiling custom ROS 2 packages.

### PRAC-01: Setting up an RL Environment

**Description**: Use a simple simulated environment (e.g., a cart-pole or simple robot in gym/MuJoCo).

**Steps**:
1.  Ensure `gym` is installed (see Section 2.4).
2.  Test environment creation:
    ```python
    import gym
    env = gym.make('CartPole-v1')
    env.reset()
    for _ in range(100):
        env.render()
        env.step(env.action_space.sample()) # take a random action
    env.close()
    ```

**Validation Steps**: A window should pop up showing a cart-pole simulation, performing random actions for 100 steps.

### PRAC-02: Implement a Simple RL Agent

**Description**: Implement a basic Q-learning or policy gradient agent.

**Steps**:
1.  Create a Python file, e.g., `q_learning_agent.py`.
2.  Implement the Q-learning algorithm as described in the chapter, using `gym` for the environment.
    ```python
    # Example structure for q_learning_agent.py
    import gym
    import numpy as np

    # ... Q-learning implementation details ...

    env = gym.make('CartPole-v1')
    # ... training loop ...
    env.close()
    ```

**Validation Steps**: The agent should run without errors, and print statements should show the Q-table updating or rewards accumulating.

### PRAC-03: Train a Policy in Simulation

**Description**: Train the implemented agent to perform a simple control task (e.g., balance a pole, move to a target).

**Steps**:
1.  Run the agent implementation from PRAC-02:
    ```bash
    python q_learning_agent.py
    ```

**Validation Steps**: Observe the agent's performance improve over episodes (e.g., pole stays balanced longer, rewards increase). Plotting the reward curves (part of PRAC-04) will also serve as validation.

### PRAC-04: Visualize Policy Performance

**Description**: Plot reward curves and visualize the learned behavior.

**Steps**:
1.  Integrate plotting code into your agent's training script or create a separate visualization script.
    ```python
    # Example plotting code
    import matplotlib.pyplot as plt
    # ... after training ...
    plt.plot(episode_rewards)
    plt.xlabel('Episode')
    plt.ylabel('Total Reward')
    plt.title('Agent Training Progress')
    plt.show()
    ```
2.  Run the trained agent (without training) to visualize its learned behavior:
    ```python
    # In q_learning_agent.py, add a mode to run a trained policy
    # ... load Q-table ...
    # ... run env.render() loop with learned policy ...
    ```

**Validation Steps**: A plot of increasing rewards over episodes should be visible. The visual simulation of the trained agent should demonstrate the desired behavior (e.g., balancing the pole).

## 4. Troubleshooting

-   **Common Issue 1**: `gym.make('CartPole-v1')` fails.
    -   **Solution**: Ensure `gym[classic_control]` is installed. If rendering issues, check `libgl1-mesa-glx` or specific display server setup.
-   **Common Issue 2**: Agent doesn't learn or behaves erratically.
    -   **Solution**: Double-check the reward function, state/action space discretization (for Q-learning), learning rate, and discount factor. Ensure exploration is sufficient.

---

**Note**: If you encounter issues not covered here, please refer to the official documentation of the respective tools or consult the community forums.