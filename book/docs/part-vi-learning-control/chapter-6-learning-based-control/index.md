---
sidebar_position: 6
---

# Chapter 6: Learning-Based Control

So far, we have discussed how to model robots and write explicit programs to control them. But what if the robot's environment is too complex or unpredictable to model perfectly? What if the task is too difficult to hand-code? In this chapter, we will explore how robots can *learn* to perform tasks on their own through trial and error, using the powerful paradigm of learning-based control.

## What You Will Learn

- [LO-01]: Explain the basic principles of Reinforcement Learning (RL) and its application to robotics.
- [LO-02]: Compare and contrast classical control methods with learning-based control approaches.
- [LO-03]: Understand the concept of policy learning and common policy optimization techniques.
- [LO-04]: Implement and train a simple RL policy in a simulated environment.

## Before You Begin

A conceptual understanding of basic machine learning concepts (e.g., what a model is, the idea of training with data) will be beneficial.

---

## Introduction to Learning-Based Control

**Why use learning?** For many robotic tasks, designing a controller by hand is extremely difficult. Imagine trying to write a classical controller to enable a humanoid robot to walk on uneven terrain. The dynamics are incredibly complex and the robot must constantly adapt to new situations.

**Learning-based control** offers a powerful alternative. Instead of telling the robot *how* to perform a task, we tell it *what* the goal is and let it figure out the "how" for itself.

-   **Benefits**:
    -   **Adaptability**: Learning-based controllers can adapt to changing environments and unforeseen situations.
    -   **Handling Complexity**: They can learn to control highly complex, non-linear systems where classical methods might fail.
-   **Challenges**:
    -   **Safety**: The learning process involves exploration, which can lead to the robot taking unsafe actions, especially in the physical world.
    -   **Sample Efficiency**: Machine learning often requires a huge amount of data. A robot may need to perform a task millions of times in simulation to learn it, which can be computationally expensive.

## Classical Control vs. Learning Control

**Classical Control** methods, like the well-known **PID (Proportional-Integral-Derivative)** controller, are workhorses in engineering. They use mathematical models of a system to create a reliable control law. They are predictable, stable, and well-understood. However, they require a reasonably accurate model of the system and can be brittle when faced with situations outside their design parameters.

**Learning-based control**, particularly **Reinforcement Learning (RL)**, doesn't necessarily require an explicit model of the system. It learns a control strategy (a policy) directly from interaction. This makes it more flexible but often less predictable, especially during the training process.

| Feature | Classical Control (e.g., PID) | Learning-Based Control (e.g., RL) |
| :--- | :--- | :--- |
| **Approach** | Model-based, analytical | Data-driven, trial-and-error |
| **Requires** | An accurate system model | A reward signal and interaction |
| **Strengths** | Stability, predictability, efficiency | Adaptability, handles complexity |
| **Weaknesses**| Can be brittle, requires good model | Sample inefficiency, safety concerns |

## Reinforcement Learning (RL) Basics

Reinforcement Learning is the primary framework for learning-based control. The setup consists of a few key components:

-   **Agent**: The learner and decision-maker (the robot's control software).
-   **Environment**: The world the agent interacts with (the physical world or a simulation).
-   **State (S)**: A snapshot of the environment at a particular moment.
-   **Action (A)**: A decision made by the agent, which changes the state.
-   **Reward (R)**: A feedback signal from the environment that tells the agent how well it is doing. The agent's goal is to maximize the cumulative reward over time.

This entire process is often formalized as a **Markov Decision Process (MDP)**. The core idea of an MDP is that the future is independent of the past, given the present state.

A central concept in RL is the **value function** or **Q-function** (as in **Q-learning**), which estimates the expected future reward from being in a certain state and taking a certain action. By learning this function, the agent can choose actions that lead to the highest expected reward.

## Policy Learning

A **policy (π)** is the agent's strategy or "brain." It is a function that maps a state to an action. In deep reinforcement learning, the policy is often represented by a neural network.

The goal of RL is to find the optimal policy that maximizes the cumulative reward. This is often done using **policy gradient** methods. These algorithms directly adjust the parameters of the policy network. They run the policy, observe the rewards, and then update the policy to make high-reward actions more likely in the future. **Proximal Policy Optimization (PPO)** and **Soft Actor-Critic (SAC)** are two popular and powerful policy gradient algorithms used in modern robotics.

## Exploration vs. Exploitation

A fundamental challenge in RL is the **exploration vs. exploitation** trade-off.
-   **Exploitation**: The agent should use what it has already learned to take actions that it knows will yield high rewards.
-   **Exploration**: The agent should also try new, random actions to discover potentially even better strategies that it hasn't seen before.

Balancing these two is critical for effective learning. Too much exploitation, and the agent gets stuck in a sub-optimal strategy. Too much exploration, and the agent never benefits from what it has learned.

---

## Tools Spotlight

-   **OpenAI Gym**: Now maintained as `Gymnasium`, this is a widely-used toolkit for developing and comparing reinforcement learning algorithms. It provides a standardized API for RL environments, including many classic control problems like "Cart-Pole," which we will use.

---

## Hands-On: Training a Simple RL Agent

*(Note: These examples are illustrative. See `reproducibility.md` for full setup instructions.)*

1.  **[PRAC-01] Setting up an RL Environment**:
    First, install `gymnasium` and set up the Cart-Pole environment. The goal in this environment is to balance a pole on top of a moving cart.
    ```python
    import gymnasium as gym
    env = gym.make("CartPole-v1", render_mode="human")
    observation, info = env.reset()
    ```

2.  **[PRAC-02 & 03] Implement and Train a Simple Agent**:
    Implementing a full RL agent from scratch is complex. For this hands-on, we'll use a library like `stable-baselines3` which contains pre-built implementations of algorithms like PPO.
    ```python
    from stable_baselines3 import PPO

    # SB3 uses a string to create the env internally
    model = PPO("MlpPolicy", "CartPole-v1", verbose=1)
    model.learn(total_timesteps=10000)
    ```
    This code initializes a PPO agent with a multi-layer perceptron policy and trains it on the CartPole environment for 10,000 steps.

3.  **[PRAC-04] Visualize Policy Performance**:
    After training, you can watch your agent perform the task.
    ```python
    vec_env = model.get_env()
    obs = vec_env.reset()
    for _ in range(1000):
        action, _states = model.predict(obs, deterministic=True)
        obs, reward, done, info = vec_env.step(action)
        vec_env.render("human")
        if done:
            obs = vec_env.reset()
    ```
    You should see the cart moving back and forth to keep the pole balanced for a significant amount of time.

---

## Connecting to the Physical World

-   **[PWC-01] Sample Inefficiency**: The 10,000 steps we used to train the Cart-Pole agent would take a significant amount of time on a real robot. For complex tasks, millions of steps are needed. This is a major reason why simulation is so critical for RL in robotics.
-   **[PWC-02] Safety Risks**: During training, our simple agent fell over many times. For a multi-million dollar humanoid robot, this is not acceptable. Researchers are actively developing "safe RL" algorithms that constrain the agent's exploration to prevent it from taking dangerous actions.
-   **[PWC-03] Sim-to-Real Transfer**: The policy we trained works perfectly in the `CartPole-v1` simulation. If we built a real cart-pole, would it work? Probably not perfectly. The real system would have friction and motor delays not present in the simple simulation. Overcoming this sim-to-real gap is one of the most significant challenges in learning-based robotics.

---

## Exercises

1.  **[EX-01] RL Terminology**:
    - For the Cart-Pole task, what is the **State**, what are the possible **Actions**, and what is the **Reward**?
    - *Assessment Criteria*: Your answer should correctly identify the components of the RL problem for the Cart-Pole environment.

2.  **[EX-02] Policy Design**:
    - You want to train a robot arm to learn to throw a ball into a basket. Propose a good reward function for this task. What would be a bad reward function, and why?
    - *Assessment Criteria*: Your proposed reward function should logically encourage the desired behavior. The analysis of a bad reward function should correctly identify potential failure modes (e.g., the agent finding a loophole).

3.  **[EX-03] Policy Training Analysis**:
    - When training an RL agent, you plot the reward per episode. The curve goes up steadily and then flattens out. What does this indicate about the agent's learning? What if the curve is highly erratic and not trending upwards?
    - *Assessment Criteria*: Correct interpretation of the training curves as signs of successful learning (convergence) and failure to learn, respectively.

---

## Conclusion

In this chapter, you've been introduced to the powerful concept of learning-based control. You've learned the fundamental principles of Reinforcement Learning—the language of agents, environments, states, actions, and rewards. You now understand the difference between classical and learning-based control and the critical trade-offs involved, especially regarding safety and sample efficiency. You've even seen how to train an agent to solve a classic control problem in a simulated environment.

In the next chapter, we will focus on a particularly challenging and exciting area of robotics: Humanoid Robots. We'll see how the concepts from all previous chapters come together in the quest to build robots in our own image.