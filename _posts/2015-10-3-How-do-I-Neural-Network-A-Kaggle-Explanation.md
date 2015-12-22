---
layout: post
title: The Power of Neural Networks and A Kickstart through Kaggle
---

Table of Contents:
- [SVM vs Softmax](#svmvssoftmax)

<a name='svmvssoftmax'></a>
## The Power of Neural Networks and A Kickstart through Kaggle: An Introduction
Welcome to the first post in a series of blogs with a focus on making current research in deep learning more tangeable! In this section, we are going to use the classic machine learning introduction classification problem MNIST to show the power of neural networks. We are then going to enter a competition and produce a submission with < 1% error! For those who are unaware, MNIST stands for Mixed National Institute of Standards and Technology and is a dataset of 70,000 black and white images (28 pixels by 28 pixels) of the numbers 0 through 9. A few examples of these images can be seen below. MNIST was created from two separate datasets whose purpose was to create a standard for how numbers were written. Half of the dataset is from American high school students' written digits and the other half is from American Census Bureau employees' written digits.

INSERT IMAGES

We are going to use neural networks to classify these images by their respective numbers, and while this may seem easy to umans, teaching a computer to do this can prove to be difficult. To do this, we only need to provide an image to the neural network as input, and the neural network will produce the number it represents as output. For now, it is unimportant for us to understand what is happening behind the scenes of a neural network; this will come in the following blog post. I just want you to see how powerful these can be before jumping into specifics. Thus, for now, you can just imagine the neural network as a function f that takes an image x and produces a number y. f(x) -> y.

In order to see how well we are doing, we will enter a Kaggle competition to compete for the best accuracy with our predicted classifications. Kaggle is a website that hosts competitions on predicitive analytics in order for researchers and people to produce the best predictive models, and I will teach you how to easily create a neural network that will earn you a top 50 finish! There will be some initial set up if you want to follow along, but if you don't you will be able to read the code and interact with the neural network right here on this blog!

SETUP SECTION: IF YOU DON'T WANT TO FOLLOW ALONG CLICK HERE TO SKIP
For this setup we are going to use the python neural network library Lasagne. There are several other neural network libraries out here such as TensorFlow (we will get to this one in the next blog post), Keras, Caffe, etc. A majority of computer scientists tend to use python when using neural networks (this will be clear in the next blog post LINK), so we will use Lasagne as a basis since it uses python. To setup lasagne, click the link to the blog post below. When you complete the installation, you will be redirected back here. If you have any trouble installing or have advice to make it more clear, feel free to reach out!
Link to blogpost on setup

LASAGNE SHORT TESTS
Now that you have successfully installed Lasagne, we are going to take a quick glimpse at the provided examples.

ENTER KAGGLE
