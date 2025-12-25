# Chapter Specification: Capstone Projects

**Chapter Number**: Part X - Chapter 10
**Feature Branch**: `[###-chapter-10-capstone-projects]`
**Created**: 2025-12-23
**Status**: Draft
**Master Spec**: [Link to `specs/002-book-master-spec/spec.md`]

## 1. Chapter Purpose

This chapter provides a series of capstone projects that require learners to integrate knowledge and skills from across the entire textbook. The goal is to solve a complex, multi-faceted problem in physical AI, demonstrating holistic understanding and practical competence.

## 2. Learning Objectives (Measurable)

Upon completing this chapter, a learner must be able to:
- [LO-01]: Integrate perception, control, and planning into a cohesive robotic system.
- [LO-02]: Independently research and apply concepts not explicitly covered in detail in the textbook.
- [LO-03]: Manage a small-scale robotics project from conception to demonstration.
- [LO-04]: Document and present the design, implementation, and results of a complex robotics project.

## 3. Prerequisite Knowledge

- [PR-01]: Completion and thorough understanding of all preceding chapters (Chapters 1-9).

## 4. Conceptual Sections (Theory)

- [CON-01]: Systems Integration Strategy
  - Discussion on how to break down a large problem, develop interfaces between subsystems (nodes), and manage a complex software stack.
  - Key terms: systems engineering, interface control document (ICD), integration testing.
- [CON-02]: Project Management for Robotics
  - Introduction to basic project management concepts tailored for a robotics project.
  - Key terms: requirements gathering, task decomposition, milestone planning, demonstration.

## 5. Practical Sections (Hands-On)

This chapter is entirely practical, consisting of project options. For each project, a detailed description, goal, and set of minimum requirements will be provided.

- [PRAC-01]: Project Option 1: Autonomous Warehouse Assistant
  - Description: Develop a system for a simulated mobile manipulator (e.g., TurtleBot4 with an arm) to navigate a warehouse, find a specific object (using an AR tag), pick it up, and deliver it to a drop-off zone.
  - Expected outcome: A successful delivery demonstration in a simulated warehouse environment.
  - Required Concepts: Navigation, Manipulation, Perception (Vision), Systems Integration.
- [PRAC-02]: Project Option 2: Natural Language-Guided Robot
  - Description: Using the concepts from Chapter 8, create a system where a robot can be given a high-level command (e.g., "Tidy up the room") and it uses an LLM to break the task down and execute it. The "room" can be a simulated environment with a few known objects.
  - Expected outcome: The robot identifies and moves at least two objects to their correct "home" positions based on a single natural language command.
  - Required Concepts: LLMs & Multimodal Robotics, HRI, Manipulation, Navigation.
- [PRAC-03]: Project Option 3: Human-Following Robot
  - Description: Implement a system where a mobile robot visually identifies a person and follows them, maintaining a safe distance. This must be robust to temporary occlusions.
  - Expected outcome: The robot successfully follows a person for at least 30 seconds in a simulated environment with obstacles.
  - Required Concepts: Perception (Vision, person detection), Control, Safety, HRI.

## 6. Physical-World Constraints Addressed

- [PWC-01]: Resource Constraints: Projects will be scoped for a single developer and will require efficient use of simulation resources.
- [PWC-02]: System Complexity: These projects force learners to confront the challenges of managing multiple interacting software components, a key difficulty in real-world robotics.

## 7. Tools Introduced (with Justification)

- [TOOL-01]: Project Management Tools (e.g., GitHub Projects, Trello) (Justification: To encourage structured planning and execution of a complex project, a vital real-world skill).

## 8. Reproducibility Requirements

- OS: Ubuntu 22.04 LTS
- Python Version: 3.10
- ROS / Simulator Version: ROS 2 Humble / Gazebo Garden
- Hardware Assumptions: None. All projects are designed for simulation.
- Validation Steps: Each project has a clear, demonstrable goal that serves as the primary validation.

## 9. Exercises and Assessment Criteria

The projects themselves are the exercises.

- [EX-01]: Project 1 Assessment
  - Assessment Criteria: Successful object pickup and delivery; clear documentation of the system architecture; code quality.
- [EX-02]: Project 2 Assessment
  - Assessment Criteria: Correct interpretation and execution of the high-level command; robustness of the LLM interaction; clear documentation.
- [EX-03]: Project 3 Assessment
  - Assessment Criteria: Smooth and reliable following behavior; handling of occlusions; adherence to safety distance; clear documentation.

## 10. Review Checklist

- [ ] Content aligns with learning objectives.
- [ ] Prerequisite knowledge assumed correctly.
- [ ] Conceptual explanations are clear and accurate.
- [ ] Practical exercises are reproducible and effective.
- [ ] Physical-world constraints are adequately addressed.
- [ ] Tool introductions are justified and not overly complex.
- [ ] Reproducibility details are complete and verifiable.
- [ ] Exercises are well-defined with clear assessment criteria.
- [ ] Overall compliance with Master Spec and Constitution v1.1.0.

---

**Status**: Draft
**Applies To**: Chapter 10
**Governed By**: Master Specification, Constitution v1.1.0
