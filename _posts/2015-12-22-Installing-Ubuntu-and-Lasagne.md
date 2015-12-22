---
layout: post
title: Installing Ubuntu and Lasagne
---

Table of Contents:
- [SVM vs Softmax](#svmvssoftmax)

<a name='svmvssoftmax'></a>
## Installing Ubuntu and Lasagne
The purpose of this post is to provide a step-by-step instruction on (1) Dual-booting Ubunutu on a Windows machine,
(2) Installing dependencies needed to install Lasagne, (3) installing Lasagne, (4) optionally enable GPU processing
which is highly recommended, and (5) optionally install nvidia's library cuDNN to speed up convolutional neural networks. This post is supposed to serve as an intermediate step in order to allow readers to 
follow along in the post [The Power of Neural Networks and a Kickstart through Kaggle: An Introduction](), but
you are more than welcome to use any part of it.

Before starting the step-by-step instructions, I want to make sure you understand what is required for installation.
- Step 1 of this tutorial is meant for Windows machines (8/8.1/10) that will dual-boot ubuntu. Dual-booting ubuntu will require a portion of your memory (specifics in Step 1). If you are sshing into a computer running Linux or have a Mac, or have a computer running Linux / Mac system
then you can move to Step 2.
- Step 4 of these instructions highly recommends enabling GPU support for Lasagne. The reason why is that using the GPU causes a near 50 fold increase in speed. This is significant
especially when working with large neural networks and large datasets! If you are using your personal computer,
check to see if your computer has a GPU. My computer has a GEFORCE GTX 660M with 2GB and has a compute capability of
3.0. To check your compute capability, you can go to nvidia's website here. Compute capabilities are just relative, so
don't worry what they actually mean. Just because your computer does not have a GPU does not mean you can't use just,
your CPU (this is the default when you intall Lasagne without Step 4). 
Just note that running neural networks and obtaining results will take a bit longer!
- Step 5 is an additional speed up
when using convolutional neural networks. When I initially installed Lasagne I did not use this and the 50x speed up from Step 4 was great by itself!

Now let's start the setup!
# Step 1: Dual-boot Ubuntu
# Step 2: Installing dependencies needed to install Lasagne
# Step 3: Installing Lasagne
# Step 4: Optionally Enable GPU support (Highly Recommended!)
# Step 5: Optionally install Nvidia's library cuDNN to speed up Convolutional Neural Networks

## Start Following the First Post!
LINK TO FIRST POST Section
