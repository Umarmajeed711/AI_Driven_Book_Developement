# Chapter Specification: ROS 2 Fundamentals

**Chapter Number**: Part III - Chapter 3  
**Feature Branch**: `ch003-ros2-fundamentals`  
**Created**: 2025-12-22  
**Status**: Draft  
**Master Spec**: `specs/002-book-master-spec/spec.md`

## 1. Chapter Purpose

Introduce ROS 2 (Robot Operating System 2) as a widely used robotics middleware, explaining its core concepts and architecture to enable learners to develop basic robotic applications.

## 2. Learning Objectives (Measurable)

Upon completing this chapter, a learner must be able to:
- [LO-01]: Understand the fundamental architecture and components of ROS 2.
- [LO-02]: Effectively use ROS 2 nodes, topics, and services for inter-process communication.
- [LO-03]: Explain the necessity and benefits of robotics middleware like ROS 2.
- [LO-04]: Create, compile, and run basic ROS 2 packages and executables.

## 3. Prerequisite Knowledge

Python basics (for creating ROS 2 nodes).

## 4. Conceptual Sections (Theory)

- [CON-01]: **Introduction to ROS 2**: What is ROS 2, its history, and key advantages over ROS 1.
- [CON-02]: **ROS 2 Architecture**:
  - Client Libraries (rclpy, rclcpp).
  - DDS (Data Distribution Service) as the middleware.
  - ROS 2 Graph (nodes, topics, services, actions).
- [CON-03]: **Nodes**: The basic computational unit in ROS 2.
- [CON-04]: **Topics**: Publish/Subscribe communication pattern.
  - Message types, QoS (Quality of Service) settings.
- [CON-05]: **Services**: Request/Reply communication pattern.
- [CON-06]: **Actions**: Long-running goal-oriented tasks.
- [CON-07]: **Why Middleware?**: Benefits for modularity, reusability, and distributed systems.

## 5. Practical Sections (Hands-On)

- [PRAC-01]: **Setting up a ROS 2 Workspace**: Create and build a basic ROS 2 workspace.
- [PRAC-02]: **Creating Basic ROS 2 Nodes**: Develop simple publisher and subscriber nodes in Python.
  - Code Examples: `minimal_publisher.py`, `minimal_subscriber.py`.
- [PRAC-03]: **Publish/Subscribe Demo**: Run the publisher and subscriber nodes and observe communication using `ros2 topic echo`.
- [PRAC-04]: **Implementing a Simple Service**: Create a basic `add_two_ints` service and client.

## 6. Physical-World Constraints Addressed

This chapter implicitly addresses the need for robust communication and coordination in physically embodied systems.
- [PWC-01]: Reliability of communication (addressed by DDS QoS).
- [PWC-02]: Synchronization of data between distributed components.

## 7. Tools Introduced (with Justification)

- **ROS 2**: Justified as it is the industry-standard middleware for robotics development, providing a robust framework for building complex robotic systems.
- **Python**: Used for creating ROS 2 nodes, leveraging its ease of use for rapid prototyping.

## 8. Reproducibility Requirements

- OS: Ubuntu LTS (e.g., Ubuntu 22.04 LTS)
- ROS 2 Version: Specific ROS 2 distribution (e.g., Humble Hawksbill)
- Python Version: As required by the ROS 2 distribution (e.g., 3.10)
- Validation Steps: Installation of ROS 2, setup of workspace, successful compilation and execution of example nodes.

## 9. Exercises and Assessment Criteria

- [EX-01]: **Build a Simple Communication System**: Create a ROS 2 node that publishes a string message and another node that subscribes and prints it, adding a timestamp.
  - Assessment Criteria: Correct node creation, topic publication/subscription, timestamping.
- [EX-02]: **Modify a Service**: Extend the `add_two_ints` service to `multiply_two_ints`.
  - Assessment Criteria: Correct service definition, client implementation, and mathematical operation.
- [EX-03]: **Conceptual Questions**: Explain the difference between ROS 2 topics and services, and when to use each.
  - Assessment Criteria: Clear and accurate explanation of communication patterns.

## 10. Review Checklist

- [ ] Content aligns with learning objectives.
- [ ] Prerequisite knowledge assumed correctly (Python basics).
- [ ] Conceptual explanations of ROS 2 architecture and communication patterns are clear and accurate.
- [ ] Practical exercises are reproducible and effective for basic ROS 2 operations.
- [ ] Physical-world constraints related to middleware are addressed.
- [ ] Tool introductions (ROS 2, Python) are justified.
- [ ] Reproducibility details are complete and verifiable for ROS 2 setup.
- [ ] Exercises are well-defined with clear assessment criteria.
- [ ] Overall compliance with Master Spec and Constitution v1.1.0.

---

**Status**: Draft  
**Applies To**: ROS 2 Fundamentals  
**Governed By**: Master Specification, Constitution v1.1.0