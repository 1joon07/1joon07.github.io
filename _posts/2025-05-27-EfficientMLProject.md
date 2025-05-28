---
layout: single
title: "Efficient ML Project Blog Post"
---

Project Title
=============

Introduction
============
Our project is to implement a trajectory generation neural network model on a microcontroller unit (MCU) equipped on an Unmanned Aerial Vehicle (UAV).   
To realize this, our team focuses on building an efficient image-guided flow-based model that is light enough to run on a low-performance Single Board Computer (SBC).

Related Works
============
1. Diffusion/Flow-based Models in Robotics
------------------------------------------
The remarkable success of generative models in language and vision domains has sparked growing interest in their application to robotics. With their strong expressive power, generative models can
produce complex trajectories and simulate highly non-linear system dynamics. Among various robotic systems, robot manipulators have been the most widely studied in this context. For example, [1] proposed a framework that learns smooth cost functions using diffusion models in SE(3) space, enabling joint optimization of 6-DoF grasp poses and motion trajectories.   
Similarly, there are some approaches to utilize generative models for UAVs. For example, [3] introduced a conditional diffusion model to learn quadrotor dynamics, leading to improved robustness and reliability in model-based control. However, relatively less research has been conducted on efficiently applying generative models to UAVs.

2. Model Optimization
---------------------
As neural networks often require intensive computation, designing an efficient model has become a crucial task, especially for deployment on resource-constrained devices. For instance, [4] imple-mented an efficient image classification model on microcontrollers using neural architecture search (NAS). There are active works that made diffusion model more efficient, by applying quantization [4] and reducing the number of iteration steps [5,6].

Methods
=======

Results
=======

Discussions
===========

References
==========
[1] Urain, Julen, et al. "Se (3)-diffusionfields: Learning smooth cost functions for joint grasp and motion optimization through diffusion." 2023 IEEE International Conference on Robotics and Automation (ICRA). IEEE, 2023.   
[2] Das, Avirup, et al. "Dronediffusion: Robust quadrotor dynamics learning with diffusion models." arXiv preprint arXiv:2409.11292 (2024).   
[4] Lin, Ji, et al. "Mcunet: Tiny deep learning on iot devices." Advances in neural information processing systems 33 (2020): 11711-11722.   
[4] So, Junhyuk, et al. "Temporal dynamic quantization for diffusion models." Advances in neural information processing systems 36 (2023): 48686-48698.   
[5] Song, Yang, et al. "Consistency models." (2023).   
[6] So, Junhyuk, Jungwon Lee, and Eunhyeok Park. "Frdiff: Feature reuse for universal training-free acceleration of diffusion models." European Conference on Computer Vision. Cham: Springer Nature Switzerland, 2024.   
