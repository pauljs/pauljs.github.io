---
layout: post
title: The Power of Neural Networks and A Kickstart through Kaggle
---

Table of Contents:
- [Introduction](#intro)
- [Setup Ubuntu and Lasagne](#setup)
- [Lasagne Examples](#examples)
- [Kaggle Competition](#kaggle)

<a name='intro'></a>
## The Power of Neural Networks and A Kickstart through Kaggle: An Introduction
Welcome to the first post in a series of blogs with a focus on making current research in deep learning more tangeable! In this section, we are going to use the classic machine learning introduction classification problem MNIST to show the power of neural networks. We are then going to enter a competition and produce a submission with < 1% error! For those who are unaware, MNIST stands for Mixed National Institute of Standards and Technology and is a dataset of 70,000 black and white images (28 pixels by 28 pixels) of the numbers 0 through 9. A few examples of these images can be seen below. MNIST was created from two separate datasets whose purpose was to create a standard for how numbers were written. Half of the dataset is from American high school students' written digits and the other half is from American Census Bureau employees' written digits.

INSERT IMAGES

We are going to use neural networks to classify these images by their respective numbers, and while this may seem easy to umans, teaching a computer to do this can prove to be difficult. To do this, we only need to provide an image to the neural network as input, and the neural network will produce the number it represents as output. For now, it is unimportant for us to understand what is happening behind the scenes of a neural network; this will come in the following blog post. I just want you to see how powerful these can be before jumping into specifics. Thus, for now, you can just imagine the neural network as a function f that takes an image x and produces a number y. f(x) -> y.

In order to see how well we are doing, we will enter a Kaggle competition to compete for the best accuracy with our predicted classifications. Kaggle is a website that hosts competitions on predicitive analytics in order for researchers and people to produce the best predictive models, and I will teach you how to easily create a neural network that will earn you a top 50 finish! There will be some initial set up if you want to follow along, but if you don't you will be able to read the code and interact with the neural network right here on this blog!

<a name='setup'></a>
##Optionally Setup Lasagne
For this setup we are going to use the python neural network library Lasagne. There are several other neural network libraries out here such as TensorFlow (we will get to this one in the next blog post), Keras, Caffe, etc. A majority of computer scientists tend to use python when using neural networks (this will be clear in the next blog post LINK), so we will use Lasagne as a basis since it uses python. To setup Lasagne, click the link to the blog post below. When you complete the installation, you will be redirected back here. If you have any trouble installing or have advice to make it more clear, feel free to reach out!

[Setup Lasagne](http://pauljs.github.io/Installing-Ubuntu-and-Lasagne/)

<a name='examples'></a>
##Lasagne Examples
Now that you have successfully installed Lasagne, we are going to take a quick glimpse at the provided examples. To view the examples we need to download them by cloning the Lasagne github repository by using the command:
```
git clone https://github.com/Lasagne/Lasagne.git
```
  - This may require you to install git. Look [here](http://git-scm.com/documentation) if you don't know what git is and [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) if you need help installing. As long as git is installed you don't need to know how to use git for this tutorial. Once you have git installed use the above command to get the Lasagne examples

Go ahead and move into the Lasagne folder by using:
```
cd Lasagne/examples
```
Here you will find will find an example python file named "mnist.py" which contains a few neural networks built to handle the MNIST images and to learn how to classify them by their respective numbers. We can actually just run the python file and see the working example go. Use the following command to start:
```python
python mnist.py
```
- First, if you have GPU enabled, you should see a statement stating a gpu device is being used. If you don't *****
- Next the file will attempt to load the MNIST images into the program. If the images are not downloaded, then the program will go ahead and download them for you
- You will then see the program state it is "Building model and compiling functions...". What this is really doing is creating your neural network for you before it starts to learn how to classify the MNIST images.
- Next it will start training the neural network in order for it to learn how to classify the images. There will be some terminology such as "Epoch, training loss, validation loss, validation accuracy" that will be unfamiliar to you. This will be explained in the next blog post in full but a brief explanation for each is put below:
  - Epoch: This represents 1 run through of all images used for training the neural network. In the MNIST dataset, 50,000 images are used for training, so 1 epoch represents presenting each of these 50,000 images to the neural network to learn
  - Loss: This represents the error in our neural network's classification predictions.
    - Training loss: The error when using only the images used for training.
    - Validation loss: The error when providing the neural network with the 10,000 validation images. Validation images are separate from the training images because we want to get a glimpse of how well our neural network would do given new images.
  - Validation accuracy: This gives the percent the neural network predicts correctly out of the given 10,000 validation images.
- Once the 500 epochs are run through, you will see a final message stating the results with the test data. The test data contains 10,000 test images, similar to the validation data, but the neural network does not use the test data to learn from. You should get a final test result around 98% (I got 98.72%).

Now you may be thinking, "you said < 1%? I should be getting at least 99%". To get < 1%, we are going to edit the example given to us slightly in order to not only give a better accuracy, but to also allow easy input from our Kaggle competition.

<a name='kaggle'></a>
##Kaggle Competition

