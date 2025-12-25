---
sidebar_position: 8
---

# Chapter 8: LLMs & Multimodal Robotics

What happens when you give a robot the ability to understand language? In this chapter, we connect the world of Physical AI with the latest breakthroughs in Large Language Models (LLMs) and computer vision. We will explore how to build robots that you can talk to, that can describe what they see, and that can reason about high-level commands, creating a new, more intuitive era of human-robot interaction.

## What You Will Learn

- [LO-01]: Explain the concept of multimodal robotics and the role of LLMs.
- [LO-02]: Design a system to convert natural language commands into robotic actions using an LLM.
- [LO-03]: Implement a basic vision-language model (VLM) to describe a scene from a robot's camera feed.
- [LO-04]: Integrate an LLM with a ROS 2 navigation or manipulation stack for task execution.
- [LO-05]: Analyze the ethical implications and limitations of using LLMs in robotics.

## Before You Begin

- You should have a solid understanding of ROS 2 (Chapter 3).
- You should be familiar with robot vision concepts (Chapter 5).
- You should be comfortable with Python and making API calls.

---

## Multimodal Robotics

Robots, like humans, operate in a world rich with information. They see objects, hear sounds, and feel forces. **Multimodal Robotics** is an approach that aims to build robots that can process and understand information from multiple modalities—like vision, text, and audio—simultaneously.

The recent explosion in the capability of **Large Language Models (LLMs)** has opened a new frontier in this field. By combining vision and language, we can create robots that don't just follow pre-programmed instructions but can interpret ambiguous human commands and ground them in the physical world.

## Introduction to Vision-Language Models (VLMs)

At the heart of this new paradigm are **Vision-Language Models (VLMs)**. These are models trained on vast datasets of images and their corresponding text descriptions.

-   **Core Concept**: A VLM learns a shared **embedding** space, where a picture of a dog and the phrase "a picture of a dog" are represented by very similar vectors. This allows for powerful connections between what a robot sees and the language we use to describe it. A famous early example of this is **CLIP (Contrastive Language-Image Pre-Training)**.
-   **Cosine Similarity**: To compare an image embedding and a text embedding, we can calculate their **cosine similarity**. A high similarity (close to 1.0) means the image and text are a good match.
-   **Zero-Shot Classification**: Because of this shared embedding space, we can perform classification without any task-specific training. To find a "red cube," the robot can simply take an image, generate embeddings for different objects it sees, and find the one with the highest cosine similarity to the text embedding of "red cube."

## LLMs for Task Planning

An LLM's greatest strength is its ability to reason about language and structure. We can leverage this for high-level task planning.

-   **Decomposition**: An LLM can take a high-level goal, like "clean the kitchen," and decompose it into a sequence of concrete, achievable sub-tasks that a robot can execute (e.g., 1. find the sponge, 2. move to the counter, 3. wipe the counter).
-   **Prompt Engineering**: The key to using an LLM effectively is **prompt engineering**. The prompt must provide the LLM with a clear description of its goal, the robot's capabilities (e.g., `available_actions = [move_to(x,y), pick_up(object)]`), and the current **state representation** of the world.
-   **Chain-of-Thought**: By instructing the LLM to use **chain-of-thought** reasoning (i.e., to "think step-by-step"), we can encourage it to produce more logical and robust plans.

## Multimodal Grounding

The most difficult challenge is **grounding**—connecting the symbols of language (like the word "apple") to the physical reality of pixels and point clouds.
-   **Semantic Mapping**: Instead of building a map with just geometric coordinates, a robot can build a **semantic map** that labels different areas, such as "the kitchen" or "the charging dock." The LLM can then use these labels in its plans.
-   **Object Affordances**: This is the concept of what an object can be used for. An LLM, combined with a VLM, can reason about **affordances**. It can infer that a cup is "graspable" and can "contain liquid," while a wall is "not graspable."

---

## Tools Spotlight

-   **Hugging Face `transformers`**: The `transformers` library provides a unified, high-level API for accessing thousands of state-of-the-art pre-trained models, including VLMs like CLIP. It is an essential tool for any modern robotics engineer working with AI.
-   **LLM APIs**: For this chapter, we will assume the use of an external LLM API (like those from OpenAI or Google AI). This allows us to leverage the power of massive models without needing to run them locally, which is often infeasible.

---

## Hands-On: "Okay, Robot"

*(Note: These examples are illustrative and require an internet connection and API keys for an LLM service. See `reproducibility.md` for full setup.)*

### [PRAC-01] Voice Command to Action

Let's create a system that takes a spoken command, uses an LLM to interpret it, and makes a simulated robot move.

1.  **System Setup**: We need a speech-to-text service to get the user's command as a string.
2.  **LLM Prompt**: We send the text command to an LLM with a carefully engineered prompt.
    ```
    You are a helpful robot assistant. Your only goal is to translate user commands into robot velocity commands.
    The user said: "{user_command}"
    You must respond with only a JSON object of the form:
    {"linear": {"x": <value>, "y": <value>, "z": 0}, "angular": {"x": 0, "y": 0, "z": <value>}}
    Positive linear x is forward. Positive angular z is left. Do not respond with any other text.
    ```
3.  **ROS 2 Node**: A Python script subscribes to the text command, calls the LLM API, parses the JSON response, and publishes it as a `geometry_msgs/Twist` message.

**Expected Outcome**: When you say "move forward," the script sends this to the LLM, gets back `{"linear": {"x": 0.5, ...}, ...}`, and publishes a `Twist` message that makes the TurtleBot3 move forward in Gazebo.

### [PRAC-02] Scene Description with a VLM

Let's use a VLM to describe what a robot sees.

```python
import rclpy
from rclpy.node import Node
from sensor_msgs.msg import Image
from std_msgs.msg import String
from transformers import pipeline
from cv_bridge import CvBridge
import cv2

class VLMNode(Node):
    def __init__(self):
        super().__init__('vlm_node')
        self.bridge = CvBridge()
        self.captioner = pipeline("image-to-text", model="Salesforce/blip-image-captioning-base")
        self.subscription = self.create_subscription(
            Image, '/camera/image_raw', self.image_callback, 10)
        self.publisher = self.create_publisher(String, '/image_description', 10)

    def image_callback(self, msg):
        cv_image = self.bridge.imgmsg_to_cv2(msg, "bgr8")
        description = self.captioner(cv_image)[0]['generated_text']
        self.get_logger().info(f"VLM sees: {description}")
        self.publisher.publish(String(data=description))
```
**Expected Outcome**: This ROS 2 node listens for images, uses a pre-trained model from Hugging Face to generate a caption (e.g., "a red cube on a wooden table"), and publishes this description to a string topic.

---

## Connecting to the Physical World

-   **[PWC-01] Ambiguity in Language**: What does "go over there" mean? An LLM-based robot must be able to recognize ambiguity. A robust system might respond with a clarifying question, such as "Do you mean near the red cube?" This requires a dialogue management system.
-   **[PWC-02] Latency**: Making an API call to an LLM takes time. For a robot moving in a dynamic environment, this **latency** can be a serious issue. The robot cannot be "thinking" for several seconds while the world changes around it. This is a major driver of research into smaller, faster, locally-run models for robotics.

## Ethical Considerations

Using LLMs in robotics comes with significant ethical responsibilities. These models can sometimes produce biased, incorrect, or harmful responses based on the data they were trained on. A robot that misunderstands a command or describes a scene incorrectly could have serious consequences. Developers must be aware of these limitations and build safety guards into their systems.

---

## Exercises

1.  **[EX-01] Extend the Voice Command System**:
    -   Modify the voice command system to handle a more complex command like "turn left." Your LLM prompt will need to be updated to handle this new case. How would you handle a command like "drive in a circle"?
    -   *Assessment Criteria*: The robot should successfully turn left in the simulator. Your answer should discuss how the prompt needs to change to extract different parameters.

2.  **[EX-02] Visual Question Answering (VQA)**:
    -   Using a VQA model from Hugging Face `transformers`, build a system where a user can ask a question about the robot's camera feed (e.g., "What color is the cube?"). The system should combine the image and the text question to generate an answer.
    -   *Assessment Criteria*: The system should provide accurate text answers to at least 3 different questions about a simulated scene.

---

## Conclusion

In this chapter, you have connected the high-level reasoning of Large Language Models with the physical embodiment of robotics. You have learned how Vision-Language Models can ground language in sensor data and how LLMs can be used for high-level task planning. You have also grappled with the real-world constraints of latency and ambiguity and considered the ethical implications of this powerful technology.

In the next chapter, we will explore the critical topics of safety and ethics in more detail, focusing on how we can build robotic systems that are not only capable but also trustworthy and reliable.