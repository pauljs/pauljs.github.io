---
layout: post
title: The Power of Neural Networks and A Kickstart through Kaggle
---

Table of Contents:
- [SVM vs Softmax](#svmvssoftmax)

<a name='svmvssoftmax'></a>
## The Power of Neural Networks and A Kickstart through Kaggle: An Introduction
Welcome to the first post in a series of blogs with a focus on making current research in deep learning more tangeable! In this section, we are going to use the classic machine learning introduction classification problem MNIST to show the power of neural networks. We are then going to enter a competition and produce a submission with < 1% error! For those who are unaware, MNIST stands for Mixed National Institute of Standards and Technology and is a dataset of 70,000 black and white images (28 pixels by 28 pixels) of the numbers 0 through 9. A few examples of these images can be seen below.

INSERT IMAGES

We are going to use neural networks to classify these images by their respective numbers. To do this, we only need to provide an image to the neural network as input, and the neural network will produce the number it represents as output. Now it is unimportant for now what is happening behind the scenes of a neural network; this will come in the following blog post. Currently we just want to see what neural networks can do, so for now you can just imagine the neural network as a function f that takes an image x and produces a number y. f(x) -> y.
