---
layout: post
title: Neural Networks
date: 2023-12-09 21:30:00-0400
description: A short explanation of neural networks 
tag: ML/NLP
category: 
giscus_comments: false
related_posts: false
---
Neural networks are a widely used algorithm in supervised learning, which involves labeled data. These networks take in inputs and produce a corresponding label.

As the name suggests, a neural network consists of multiple neurons. Each neuron performs two tasks:

1. It computes the linear combination of inputs from the previous layer using weights.
2. It transforms this linear combination using an activation function.

Training a neural network involves two steps: forward propagation and backward propagation. Here’s a simplified explanation of both procedures and how they contribute to training a neural network:

1. Initialize Weights and Biases: The weights and biases of the neural network are initially set to random values.

2. Forward Propagation: The input data is passed through the network, resulting in an initial prediction.

3. Calculate Loss: The difference between the network’s prediction and the actual output is calculated. This difference is often referred to as the loss or error. The goal is to minimize this error so that our prediction closely matches the expected label. To achieve this, we adjust the learnable parameters (weights and biases) in the next step: backward propagation. After each adjustment, our predicted label should get closer to the expected label. Remember, we are dealing with labeled data in supervised learning!

4. Backward Propagation (Backpropagation): The error is then propagated back through the network. This involves calculating the gradient of the error with respect to the weights and biases. The gradient points in the direction of the steepest increase in the error.

5. Update Weights and Biases: The weights and biases are then updated in the opposite direction of the gradient. This is achieved by subtracting the gradient of the weights and biases (multiplied by a learning rate) from the current weights and biases. This process is known as gradient descent.

6. Iterate: Steps 2-5 are repeated for a number of iterations or until the network’s predictions are satisfactory.

The learning rate is a hyperparameter that determines the extent of adjustment to the weights and biases with each update. A smaller learning rate might slow down the learning process but increase its precision, while a larger learning rate might speed it up but decrease its accuracy.

This process allows the neural network to learn from its mistakes, much like how humans learn from their experiences. Over time, this iterative process of forward propagation, loss calculation, backpropagation, and weight and bias updates enables the neural network to minimize the error of its predictions.

For more information, you can refer to this blog article: [A Data Scientist’s Guide to Gradient Descent and Backpropagation Algorithms.](https://developer.nvidia.com/blog/a-data-scientists-guide-to-gradient-descent-and-backpropagation-algorithms/). Also, please make sure to check out these two discussion notes: [Neural Networks](https://umich-my.sharepoint.com/:b:/g/personal/bowenyi_umich_edu/EdvDNzOy65lDgObkMYGg7hgBImzrTPGlaSV0mzeAiwq7Pg?e=pvAq8O) and [Convolutional Neural Networks](https://umich-my.sharepoint.com/:b:/g/personal/bowenyi_umich_edu/EcwmM3MDDyxGi_YGvqRhiMEBUJwkoG4QTbfMB-Uyu2KjPw?e=TjUBEd) of EECS 445 at UMich for more details!  