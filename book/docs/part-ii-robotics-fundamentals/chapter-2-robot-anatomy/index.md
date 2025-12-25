---
sidebar_position: 2
---

# Chapter 2: Robot Anatomy, Kinematics & Dynamics

Now that we understand the concept of Physical AI, it's time to dive into the "physical" aspect of our intelligent systems. This chapter introduces the fundamental mechanical and mathematical concepts that govern how robots are built and how they move. We'll explore the components that make up a robot and the mathematical models we use to describe their motion.

## What You Will Learn

- [LO-01]: Understand basic robot structure, including links, joints, and end-effectors.
- [LO-02]: Explain the difference between forward and inverse kinematics.
- [LO-03]: Interpret basic joint/link models and degrees of freedom.
- [LO-04]: Differentiate between kinematics (motion description) and dynamics (motion causation).

## Before You Begin

You should have a basic understanding of algebra, trigonometry, and vectors.

---

## Robot Anatomy

A robot, at its most basic, is a collection of rigid bodies connected by joints.

-   **Links**: The rigid bodies that make up the skeleton of a robot are called **links**.
-   **Joints**: **Joints** are the connections between links that allow relative motion. The two most common types are:
    -   **Revolute (R)**: A rotating joint, like an elbow or a hinge.
    -   **Prismatic (P)**: A sliding or linear joint, like a piston.
-   **End-Effectors**: This is the "business end" of the robot—the tool attached to the final link that interacts with the world. Examples include a gripper, a welding torch, a camera, or a drill.
-   **Base Frame**: A fixed coordinate system, usually at the base of the robot, that serves as a reference for all other positions and movements.
-   **Tool Frame**: A coordinate system attached to the end-effector.

```mermaid
graph TD
    A(Base Frame) --> B(Link 1);
    B --> C{Joint 1 (Revolute)};
    C --> D(Link 2);
    D --> E{Joint 2 (Revolute)};
    E --> F(End-Effector);
    F --> G(Tool Frame);
```

## Degrees of Freedom (DOF)

The **Degrees of Freedom (DOF)** of a robot is the number of independent parameters required to completely define its configuration. In simpler terms, it's the number of ways a robot can move. For a simple robotic arm, the DOF is typically equal to the number of joints. A robot with 6 DOF (like the human arm, approximately) can reach any position and orientation in 3D space.

## Forward Kinematics

**Forward Kinematics** is the process of calculating the position and orientation of the robot's end-effector given the values of its joint parameters (e.g., the angles of its revolute joints). It answers the question: "If I set my joints to these specific angles, where will my hand be?"

To solve this, robotics engineers use mathematical tools like **Homogeneous Transformation Matrices**, which are 4x4 matrices that can represent both rotation and translation in a single operation. A common convention for assigning coordinate frames to links and calculating these matrices is the **Denavit-Hartenberg (DH) Parameters** method. For now, it's enough to understand that forward kinematics is a direct calculation that maps joint states to an end-effector pose.

## Inverse Kinematics

**Inverse Kinematics** is the reverse problem: given a desired position and orientation for the end-effector, what are the joint parameters needed to achieve it? This is a much harder problem than forward kinematics.

Consider trying to touch a specific spot on a wall. Your brain must solve an inverse kinematics problem to figure out the correct angles for your shoulder, elbow, and wrist. The challenges include:
-   **Multiple Solutions**: There might be several different ways to reach the same point (e.g., "elbow up" vs. "elbow down").
-   **No Solution**: The desired pose might be outside the robot's reachable workspace.

Solutions can be **Analytical** (finding a direct mathematical formula, possible for simple robots) or **Numerical** (using iterative algorithms to get closer and closer to the desired pose, which is more common for complex robots).

## Introduction to Robot Dynamics

While kinematics describes the *geometry* of motion, **dynamics** describes the *causes* of motion. It answers the question: "What forces and torques do I need to apply at each joint to achieve this desired motion?"

-   **Kinematics vs. Dynamics**: Kinematics deals with position, velocity, and acceleration. Dynamics deals with the **forces**, **torques**, and **inertia** that cause that motion.
-   **Equations of Motion**: These are the mathematical equations (typically based on Lagrangian or Newton-Euler formulations) that describe the relationship between the joint torques, and the resulting positions, velocities, and accelerations of the robot's links. We will not derive these in detail, but it is important to understand their role in controlling a robot.

---

## Hands-On: Paper-based Reasoning Exercises on Kinematics

This chapter's exercises are conceptual and can be done with pen and paper to build intuition.

-   **[PRAC-01]**: Imagine a simple "2R" robot arm, which has two revolute joints in a plane.
    1.  Sketch the arm with both joint angles at 0 degrees.
    2.  Now, sketch the arm's configuration if the first joint is at 45 degrees and the second is at -90 degrees. This is an exercise in **forward kinematics intuition**.
    3.  Pick a point in front of the robot. Can you sketch two different ways the arm could reach that point? This is an exercise in **inverse kinematics intuition**.

---

## Connecting to the Physical World

The mathematical models we've discussed are the first step in bridging the gap between an ideal robot and a real one.

-   **[PWC-01] Gravity**: In the real world, **gravity** is a force that constantly acts on a robot's links. The robot's motors must apply a continuous torque just to hold the arm in place against gravity. This is a key part of the robot's dynamic model.
-   **[PWC-02] Friction**: The joints of a real robot have **friction**, which opposes motion. This means more torque is needed to start moving, and the robot's behavior might not perfectly match the ideal equations.
-   **[PWC-03] Torque Limits**: Every motor has a **torque limit**. The robot's controller must respect these limits, which constrains the accelerations and payloads the robot can handle.

## Exercises

1.  **[EX-01] DOF Calculation**:
    - A standard car has 3 degrees of freedom (position on a 2D plane and orientation). A simple planar robot arm with 3 revolute joints has how many DOF?
    - *Assessment Criteria*: Correct application of the concept of degrees of freedom.

2.  **[EX-02] Kinematics Interpretation**:
    - Look at a diagram of a simple 2R robot arm. If the first link has length L1 and the second has length L2, and both joint angles are 0, what is the (x, y) position of the end-effector? What if the first joint is at 90 degrees and the second is at 0?
    - *Assessment Criteria*: Your answer should demonstrate a qualitative understanding of how joint angles determine the end-effector's position.

3.  **[EX-03] Dynamics Conceptualization**:
    - Imagine a robot arm lifting a 1kg weight. Now imagine it lifting a 5kg weight. How would the torques required at the joints differ? What if the arm were performing the same motion on the Moon, where gravity is much weaker?
    - *Assessment Criteria*: Your description should correctly identify that higher forces/torques are needed for heavier objects and that gravity is a major factor in robot dynamics.

---

## Conclusion

In this chapter, you've learned the basic vocabulary of robotics, from links and joints to the fundamental difference between kinematics and dynamics. You now understand that forward kinematics tells you where the robot is, while inverse kinematics figures out how to get it there. You've also seen that dynamics accounts for the forces and torques that create motion, connecting the mathematical models to physical realities like gravity and friction.

In the next chapter, we will move from the physical and mathematical foundations to the software that brings it all to life: the Robot Operating System 2 (ROS 2).