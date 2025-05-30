---
layout: single
title: "Efficient ML Project Blog Post"
---

Project Title
=============
<span style="font-size:130%">Lidar image-guided trajectory generation model for automotives</span>

Authors
=======
Jiho Ryoo, Won Joon Choi

Introduction
============
Our project is to implement a trajectory generation neural network model on a Single Board Computer (SBC) equipped on an automotive.   
To realize this, our team focuses on building an efficient lidar image-guided generative model that is light enough to run on a low-performance computer.

Related Works
============
__1. Diffusion Models in Robotics__   
The remarkable success of generative models in language and vision domains has sparked growing interest in their application to robotics. With their strong expressive power, generative models can produce complex trajectories and simulate highly non-linear system dynamics. Among various robotic systems, robot manipulators have been most widely studied in this context. For example, [1] proposed a framework that learns smooth cost functions using diffusion models in SE(3) space, enabling joint optimization of 6-DoF grasp poses and motion trajectories.   
Similarly, there are some approaches to utilize generative models for automotives. For example, [3] introduced a conditional diffusion model to learn quadrotor dynamics, leading to improved robustness and reliability in model-based control. However, relatively less research has been conducted on efficiently applying generative models to automotives.

__2. Model Optimization__   
As neural networks often require intensive computations, designing an efficient model has become a crucial task, especially for deployment on resource-constrained devices. For instance, [4] implemented an efficient image classification model on microcontrollers using Neural Architecture Search (NAS). There are active works that made diffusion model more efficient, by applying quantization [4] and reducing the number of iteration steps [5,6].

Methods
=======
__1. Memory-efficient U-Net-based diffusion model__   
<p align="center">
  <img src="/assets/images/Efficient_ML_figure1.png">
</p>
<center>[U-Net model with skip connection compression]</center><br>
Our model should run on a single board computer on a vehicle, which has limited resources. In order to realize a diffusion model, which generates the future trajectory of the automotive, Our team developed a diffusion model which has a memory-efficient U-Net structure. By adopting the encoder-decoder based compressor network for the skip connection, the model can save memory while improving the quality at the same time.

__2. 2D-lidar image guidance__   
<p align="center">
  <img src="/assets/images/Efficient_ML_figure2.png">
</p>
<center>[An example 2D lidar image]</center><br>
In order to let the model to generate a trajectory of the vehicle, the model needs to obtain information of its surroundings. Therefore, our team suggests implementing a 2D lidar image as a guidance. 2D range images can be easily be obtained by attaching a lidar on the vehicle. It gives spatial structures of the surroundings which could be effective for generating a safe trajectory for automotives.

Experiments
===========
__1. Real-world trajectory dataset__
<p align="center">
  <img src="/assets/images/Efficient_ML_figure3.png">
</p>
In order to train a trajectory-generating diffusion model, we obtained real-world driving data using a RC car. The target task is to park in the designated position, which is surrounded with boxes. Total of 70 episodes of parking dataset is made. The dataset includes 1. LiDAR scan data, 2. velocity, 3. throttle and 4. steering command.

__2. Training__   
We trained the model with batch size 512, 100 epoch, learning rate 1e-5, skip connection compression ratio 50% for the first layer and 75% for the second layer.

Results
=======
__1. Memory saving__   
Using memory-efficient U-Net we proposed, we were able to not only save RAM usage, but also improve performance. This memory-efficient U-Net converged faster, where U-Net without this method often diverged. The figure below shows that proposed method suppresses the size of gradient, preventing gradient explosion.
<p align="center">
  <img src="/assets/images/Efficient_ML_figure4.png">
</p>

__2. Driving performance__  
The trained model is implemented on SBC (Jetson).

Discussions
===========
In this project, our team presents an efficient diffusion model which generates a trajectory of automotives, guided by a 2D lidar image. The proposed model is light enough to run on an SBC with limited computing resources.   
By implementing more various guidances including embedded RGB images, our model is expected to show more reliable trajectory generation performance.

References
==========
[1] Urain, Julen, et al. "Se (3)-diffusionfields: Learning smooth cost functions for joint grasp and motion optimization through diffusion." 2023 IEEE International Conference on Robotics and Automation (ICRA). IEEE, 2023.   
[2] Das, Avirup, et al. "Dronediffusion: Robust quadrotor dynamics learning with diffusion models." arXiv preprint arXiv:2409.11292 (2024).   
[4] Lin, Ji, et al. "Mcunet: Tiny deep learning on iot devices." Advances in neural information processing systems 33 (2020): 11711-11722.   
[4] So, Junhyuk, et al. "Temporal dynamic quantization for diffusion models." Advances in neural information processing systems 36 (2023): 48686-48698.   
[5] Song, Yang, et al. "Consistency models." (2023).   
[6] So, Junhyuk, Jungwon Lee, and Eunhyeok Park. "Frdiff: Feature reuse for universal training-free acceleration of diffusion models." European Conference on Computer Vision. Cham: Springer Nature Switzerland, 2024.   
