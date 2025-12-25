# Reproducibility Guide for Chapter: ROS 2 Fundamentals

**Chapter Number**: Part III - Chapter 3  
**Date Generated**: 2025-12-24  
**Purpose**: This document outlines the precise steps and environment configurations required to reproduce the hands-on exercises and code examples presented in Chapter 3. Adhering to these guidelines is crucial for replicating results and ensuring a consistent learning experience.

---

## 1. System Requirements

The following operating system and software versions are recommended for optimal reproducibility.

-   **Operating System**: Ubuntu LTS (e.g., Ubuntu 22.04 LTS)
-   **Python Version**: 3.10
-   **ROS / Simulator Version**: ROS 2 Humble Hawksbill
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
sudo apt install software-properties-common
sudo add-apt-repository universe
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
sudo apt update
sudo apt upgrade -y
sudo apt install ros-humble-desktop -y
source /opt/ros/humble/setup.bash
```

**Simulator Not Applicable**:
```bash
# No specific simulator is introduced in this chapter.
```

### 2.3. Python Environment Setup

Ensure the specified Python version is installed and set up. It's recommended to use a virtual environment to manage project dependencies.

```bash
# Example for Python 3.10
sudo apt update
sudo apt install python3.10 python3.10-venv
# Create and activate a virtual environment
python3.10 -m venv ~/ch003_ros2_fundamentals_venv
source ~/ch003_ros2_fundamentals_venv/bin/activate
```

### 2.4. Python Library Installation

Install the required Python libraries using `pip`.

```bash
source ~/ch003_ros2_fundamentals_venv/bin/activate # Activate if not already active
# Specific libraries for this chapter:
# No specific Python libraries are mentioned in the spec beyond basic Python.
# If additional ROS 2 Python packages are needed, they would be installed here.
```

### 2.5. Additional Software/Dependencies

If there are any other specific software or dependencies required, list them here.

- None

## 3. Hands-On Exercise Setup

For each practical exercise (`PRAC-XX`), detailed setup steps are provided here. This may include cloning specific repositories, downloading datasets, or compiling custom ROS 2 packages.

### PRAC-01: Setting up a ROS 2 Workspace

**Description**: Create and build a basic ROS 2 workspace.

**Steps**:
1.  Create a new directory for your workspace:
    ```bash
    mkdir -p ~/ros2_ws/src
    cd ~/ros2_ws
    ```
2.  Build the empty workspace:
    ```bash
    colcon build
    ```
3.  Source the workspace:
    ```bash
    source install/setup.bash
    ```

**Validation Steps**: Successful compilation and sourcing of the workspace. You should be able to run `ros2 doctor` without major errors related to setup.

### PRAC-02: Creating Basic ROS 2 Nodes

**Description**: Develop simple publisher and subscriber nodes in Python.

**Steps**:
1.  Navigate to the `src` directory of your workspace:
    ```bash
    cd ~/ros2_ws/src
    ```
2.  Create a new ROS 2 package:
    ```bash
    ros2 pkg create --build-type ament_python my_ros_pkg --dependencies rclpy std_msgs
    ```
3.  Create `minimal_publisher.py` in `my_ros_pkg/my_ros_pkg/`:
    ```python
    # minimal_publisher.py content (as provided in Chapter 3)
    import rclpy
    from rclpy.node import Node
    from std_msgs.msg import String

    class MinimalPublisher(Node):

        def __init__(self):
            super().__init__('minimal_publisher')
            self.publisher_ = self.create_publisher(String, 'topic', 10)
            timer_period = 0.5  # seconds
            self.timer = self.create_timer(timer_period, self.timer_callback)
            self.i = 0

        def timer_callback(self):
            msg = String()
            msg.data = 'Hello World: %d' % self.i
            self.publisher_.publish(msg)
            self.get_logger().info('Publishing: "%s"' % msg.data)
            self.i += 1

    def main(args=None):
        rclpy.init(args=args)
        minimal_publisher = MinimalPublisher()
        rclpy.spin(minimal_publisher)
        minimal_publisher.destroy_node()
        rclpy.shutdown()

    if __name__ == '__main__':
        main()
    ```
4.  Create `minimal_subscriber.py` in `my_ros_pkg/my_ros_pkg/`:
    ```python
    # minimal_subscriber.py content (as provided in Chapter 3)
    import rclpy
    from rclpy.node import Node
    from std_msgs.msg import String

    class MinimalSubscriber(Node):

        def __init__(self):
            super().__init__('minimal_subscriber')
            self.subscription = self.create_subscription(
                String,
                'topic',
                self.listener_callback,
                10)
            self.subscription  # prevent unused variable warning

        def listener_callback(self, msg):
            self.get_logger().info('I heard: "%s"' % msg.data)

    def main(args=None):
        rclpy.init(args=args)
        minimal_subscriber = MinimalSubscriber()
        rclpy.spin(minimal_subscriber)
        minimal_subscriber.destroy_node()
        rclpy.shutdown()

    if __name__ == '__main__':
        main()
    ```
5.  Edit `~/ros2_ws/src/my_ros_pkg/setup.py` to include the executables:
    ```python
    # ... (existing content) ...
    entry_points={
        'console_scripts': [
            'talker = my_ros_pkg.minimal_publisher:main',
            'listener = my_ros_pkg.minimal_subscriber:main',
        ],
    },
    # ... (rest of the file) ...
    ```
6.  Build your workspace again:
    ```bash
    cd ~/ros2_ws
    colcon build
    source install/setup.bash
    ```

**Validation Steps**: No build errors. You can run `ros2 run my_ros_pkg talker` and `ros2 run my_ros_pkg listener` in separate terminals.

### PRAC-03: Publish/Subscribe Demo

**Description**: Run the publisher and subscriber nodes and observe communication using `ros2 topic echo`.

**Steps**:
1.  Open three separate terminals.
2.  In each terminal, source your ROS 2 environment:
    ```bash
    source ~/ros2_ws/install/setup.bash
    ```
3.  In Terminal 1, run the publisher:
    ```bash
    ros2 run my_ros_pkg talker
    ```
4.  In Terminal 2, run the subscriber:
    ```bash
    ros2 run my_ros_pkg listener
    ```
5.  In Terminal 3, echo the topic:
    ```bash
    ros2 topic echo /topic
    ```

**Validation Steps**: Messages should be continuously printed in both the subscriber terminal and the `ros2 topic echo` terminal.

### PRAC-04: Implementing a Simple Service

**Description**: Create a basic `add_two_ints` service and client.

**Steps**:
1.  Navigate to the `src` directory of your workspace:
    ```bash
    cd ~/ros2_ws/src
    ```
2.  Create a custom service definition. Inside `my_ros_pkg/srv/`, create `AddTwoInts.srv`:
    ```
    int64 a
    int64 b
    ---
    int64 sum
    ```
3.  Edit `~/ros2_ws/src/my_ros_pkg/package.xml` to include `rosidl_default_generators` and `rosidl_default_runtime`:
    ```xml
    <!-- ... (existing content) ... -->
    <build_depend>rosidl_default_generators</build_depend>
    <exec_depend>rosidl_default_runtime</exec_depend>
    <member_of_group>rosidl_interface_packages</member_of_group>
    <!-- ... (rest of the file) ... -->
    ```
4.  Edit `~/ros2_ws/src/my_ros_pkg/CMakeLists.txt` to add service generation:
    ```cmake
    # ... (existing content) ...
    find_package(rosidl_default_generators REQUIRED)
    rosidl_generate_interfaces(${PROJECT_NAME}
      "srv/AddTwoInts.srv"
    )
    # ... (rest of the file) ...
    ```
5.  Build your workspace again (this will generate service code):
    ```bash
    cd ~/ros2_ws
    colcon build
    source install/setup.bash
    ```
6.  Create `minimal_service.py` in `my_ros_pkg/my_ros_pkg/`:
    ```python
    # minimal_service.py content (as provided in Chapter 3)
    import rclpy
    from rclpy.node import Node
    from my_ros_pkg.srv import AddTwoInts # Custom service import

    class MinimalService(Node):

        def __init__(self):
            super().__init__('minimal_service')
            self.srv = self.create_service(AddTwoInts, 'add_two_ints', self.add_two_ints_callback)

        def add_two_ints_callback(self, request, response):
            response.sum = request.a + request.b
            self.get_logger().info('Incoming request: a: %d b: %d' % (request.a, request.b))
            self.get_logger().info('Sending back response: [%d]' % response.sum)
            return response

    def main(args=None):
        rclpy.init(args=args)
        minimal_service = MinimalService()
        rclpy.spin(minimal_service)
        minimal_service.destroy_node()
        rclpy.shutdown()

    if __name__ == '__main__':
        main()
    ```
7.  Create `minimal_client.py` in `my_ros_pkg/my_ros_pkg/`:
    ```python
    # minimal_client.py content (as provided in Chapter 3)
    import sys
    import rclpy
    from rclpy.node import Node
    from my_ros_pkg.srv import AddTwoInts # Custom service import

    class MinimalClientAsync(Node):

        def __init__(self):
            super().__init__('minimal_client_async')
            self.cli = self.create_client(AddTwoInts, 'add_two_ints')
            while not self.cli.wait_for_service(timeout_sec=1.0):
                self.get_logger().info('service not available, waiting again...')
            self.req = AddTwoInts.Request()

        def send_request(self, a, b):
            self.req.a = a
            self.req.b = b
            self.future = self.cli.call_async(self.req)
            rclpy.spin_until_future_complete(self, self.future)
            return self.future.result()

    def main(args=None):
        rclpy.init(args=args)
        minimal_client = MinimalClientAsync()
        response = minimal_client.send_request(int(sys.argv[1]), int(sys.argv[2]))
        minimal_client.get_logger().info(
            'Result of add_two_ints: for %d + %d = %d' %
            (int(sys.argv[1]), int(sys.argv[2]), response.sum))
        minimal_client.destroy_node()
        rclpy.shutdown()

    if __name__ == '__main__':
        main()
    ```
8.  Edit `~/ros2_ws/src/my_ros_pkg/setup.py` to include the service executables:
    ```python
    # ... (existing content) ...
    entry_points={
        'console_scripts': [
            'talker = my_ros_pkg.minimal_publisher:main',
            'listener = my_ros_pkg.minimal_subscriber:main',
            'service = my_ros_pkg.minimal_service:main',
            'client = my_ros_pkg.minimal_client:main',
        ],
    },
    # ... (rest of the file) ...
    ```
9.  Build your workspace again:
    ```bash
    cd ~/ros2_ws
    colcon build
    source install/setup.bash
    ```

**Validation Steps**: No build errors. You can run `ros2 run my_ros_pkg service` in one terminal and `ros2 run my_ros_pkg client 5 3` in another, observing the correct sum.

## 4. Troubleshooting

-   **Common Issue 1**: `colcon build` fails.
    -   **Solution**: Ensure all dependencies are installed (`rosdep install --from-paths src --ignore-src -y`), and that you have sourced your main ROS 2 installation. Check compiler errors for specific missing packages.
-   **Common Issue 2**: `ros2 run` command not found.
    -   **Solution**: Ensure you have sourced your ROS 2 workspace (`source install/setup.bash`) after building.

---

**Note**: If you encounter issues not covered here, please refer to the official documentation of the respective tools or consult the community forums.