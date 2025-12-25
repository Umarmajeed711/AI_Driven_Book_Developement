---
sidebar_position: 10
---

# Chapter 10: Capstone Projects

Welcome to the final chapter. You have journeyed through the core components of modern robotics—from the mathematics of motion and the principles of perception to the complexities of control, learning, and human interaction. It is now time to put it all together. This chapter provides a series of capstone projects designed to challenge you to integrate these concepts to solve a complex problem, demonstrating your competence as a budding robotics engineer.

## What You Will Learn

- [LO-01]: Integrate perception, control, and planning into a cohesive robotic system.
- [LO-02]: Independently research and apply concepts not explicitly covered in detail in the textbook.
- [LO-03]: Manage a small-scale robotics project from conception to demonstration.
- [LO-04]: Document and present the design, implementation, and results of a complex robotics project.

## Before You Begin

You should have a thorough understanding of the concepts from all preceding chapters. These projects will require you to draw on everything you have learned so far.

---

## Systems Integration Strategy

Real-world robotics is all about **systems integration**. A robot is not a single program; it is a complex collection of hardware and software components that must work together seamlessly. Before diving into a project, it's crucial to have a strategy.

-   **Problem Decomposition**: Break the large, complex problem down into smaller, manageable sub-problems. For example, a delivery robot project can be decomposed into: (1) Navigation, (2) Perception, (3) Manipulation, and (4) a main controller.
-   **Interface Design**: Define the "contracts" between your subsystems. In ROS 2, this means defining the topics, services, and action interfaces that each node will use to communicate. A simple **Interface Control Document (ICD)**, even just a table in a README, can be invaluable for keeping your system organized.
-   **Integration Testing**: Test each subsystem independently first. Can your navigation stack receive a goal and compute a path? Can your perception module identify the target object? Once the components work in isolation, begin **integration testing** by combining them one by one to ensure they work together as expected.

## Project Management for Robotics

Even a small robotics project can have many moving parts. Applying basic project management principles will help you stay on track.

-   **Requirements Gathering**: Clearly define what "done" looks like. What are the specific, measurable goals of your project?
-   **Task Decomposition**: Break the project down into concrete coding tasks. A tool like GitHub Projects or Trello can be extremely helpful for tracking what needs to be done, what is in progress, and what is complete.
-   **Milestone Planning**: Set intermediate goals. For example, "Milestone 1: Robot can navigate to the correct room. Milestone 2: Robot can identify the object. Milestone 3: Robot can pick up the object." This provides a clear path to your final goal and allows you to demonstrate progress.
-   **Demonstration**: Your final goal is a successful demonstration that meets your initial requirements.

---

## Project Options

Choose one of the following three projects. Each is designed to be achievable in simulation by a single person, but they are open-ended enough to be expanded upon.

### [PRAC-01] Project Option 1: Autonomous Warehouse Assistant

-   **Goal**: Develop a system for a simulated mobile manipulator (e.g., TurtleBot4 with an arm) to navigate a warehouse, find a specific object marked with an AR tag, pick it up, and deliver it to a pre-defined drop-off zone.
-   **Description**: This project is a classic integration challenge. You will need to use the ROS 2 navigation stack (Nav2) to move the robot, a perception package to detect the AR tag, and a manipulation library (like MoveIt2) to control the arm. A central state machine or behavior tree will be needed to coordinate all the actions.
-   **Minimum Requirements**:
    1.  Robot successfully navigates from a start point to a search area.
    2.  Robot successfully identifies the AR tag associated with the target object.
    3.  Robot successfully picks up the object.
    4.  Robot successfully navigates to the drop-off zone and places the object.
-   **Concepts Applied**: Navigation, Manipulation, Perception (Vision), Systems Integration.

### [PRAC-02] Project Option 2: Natural Language-Guided Robot

-   **Goal**: Create a "tidy up" robot that can interpret a high-level natural language command, perceive objects in a room, and move them to their correct "home" locations.
-   **Description**: This project builds directly on the concepts from Chapter 8. You will create a simulated room with several objects (e.g., a "red cube" and a "blue sphere"). You will define "home" locations for these objects. The user will issue a command like, "Okay robot, tidy up the room." Your system will use a VLM to identify the objects and their locations, an LLM to generate a plan (e.g., "1. Pick up red cube. 2. Go to red home location. 3. Place red cube..."), and then execute this plan using the navigation and manipulation stacks.
-   **Minimum Requirements**:
    1.  System correctly identifies at least two different objects and their positions using vision.
    2.  LLM correctly generates a valid, multi-step plan.
    3.  Robot successfully picks, carries, and places both objects in their correct home locations.
-   **Concepts Applied**: LLMs & Multimodal Robotics, HRI, Manipulation, Navigation.

### [PRAC-03] Project Option 3: Human-Following Robot

-   **Goal**: Implement a robust person-following system on a simulated mobile robot. The robot should be able to find a person in its camera view and follow them, maintaining a safe distance.
-   **Description**: This project focuses on the tight loop between perception and control. You will need a person-detection model (e.g., YOLO, or a pre-existing ROS 2 package) to find the person in the robot's camera feed. A control node will then take the person's location in the image (e.g., their bounding box) and use it to generate velocity commands to keep the person centered and at a set distance.
-   **Minimum Requirements**:
    1.  Robot can find and orient towards a person in its view.
    2.  Robot maintains a safe following distance (+/- 0.5 meters of a target distance).
    3.  Robot stops if the person stops.
    4.  Robot can handle a temporary occlusion (e.g., the person is briefly hidden behind a pillar) and resume following if the person reappears within a few seconds.
-   **Concepts Applied**: Perception (Vision, Person Detection), Control, Safety, HRI.

---

## Assessment and Documentation

The primary assessment for this chapter is the successful demonstration of your chosen project. In addition to the demonstration, you must provide clear documentation covering:

1.  **System Architecture**: A diagram (like a ROS 2 graph) showing your nodes and the topics/services they use to communicate.
2.  **Design Choices**: A brief write-up explaining the key design decisions you made and why.
3.  **Launch and Usage Instructions**: A clear `README.md` that explains how to install any dependencies, launch your system, and run the demonstration.

---

## Conclusion

Congratulations! By completing one of these projects, you have demonstrated a holistic understanding of robotics. You have moved beyond individual components and have successfully integrated them into a complete system that perceives, plans, and acts to achieve a complex goal. The skills you have honed—in systems thinking, integration, and independent problem-solving—are the most valuable assets you can have as a robotics engineer.

The world of Physical AI is just beginning. The foundations you have built in this book will serve you well as you continue to learn, explore, and build the intelligent robots of the future. The journey ahead is long and challenging, but you are now well-equipped to begin. Good luck!