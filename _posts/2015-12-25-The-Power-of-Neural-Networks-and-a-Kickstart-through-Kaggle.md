---
layout: post
comments: true
title: The Power of Neural Networks and a Kickstart through Kaggle
excerpt: "Welcome to the first post in a series of blogs with a focus on making current research in deep learning and neural networks more tangeable!"
date: 2015-12-25 12:35:00
---

Table of Contents:

- [Introduction](#intro)
- [Setup Ubuntu and Lasagne](#setup)
- [Lasagne Examples](#examples)
- [Kaggle Competition](#kaggle)
  - [Load Dataset](#load-dataset)
  - [Get Predictions](#get-predictions)
  - [Save Predictions](#save-predictions)
  - [Save Neural Network](#save-nn)
  - [Load Neural Network](#load-nn)
  - [Run Your Neural Network](#run)

# Blah

Blah
====

<a name='intro'></a>
## The Power of Neural Networks and a Kickstart through Kaggle: An Introduction
Welcome to the first post in a series of blogs with a focus on making current research in deep learning and neural networks more tangeable! While this post will not go into details on what deep learning and neural networks are (this is saved for the next post), in this section, we are going to use the introduction machine learning problem on labeling pictures of numbers using the MNIST dataset to show the power of neural networks. We are then going to enter a competition and produce a submission with < 1% error! For those who are unaware, MNIST stands for Modified (or Mixed) National Institute of Standards and Technology and is a dataset of 70,000 black and white images (28 pixels by 28 pixels) of the numbers 0 through 9. A few examples of these images can be seen below. MNIST was created from two separate datasets whose purpose was to create a standard for how numbers were written. Half of the dataset is from American high school students' written digits and the other half is from American Census Bureau employees' written digits.

<div style="text-align:center;"><img src="/assets/The-Power-of-Neural-Networks-and-a-Kickstart-through-Kaggle/mnist_samples.png"></div>

We are going to use neural networks to classify these images by their respective numbers, and while this may seem easy to us, teaching a computer to do this can prove to be difficult. To do this, we only need to provide an image to the neural network as input, and the neural network will produce the number it represents as output. For now, it is unimportant for us to understand what is happening behind the scenes of a neural network; this will come in the following blog post. I just want you to see how powerful these can be before jumping into specifics. Thus, for now, you can just imagine the neural network as a function f that takes an image x and produces a number y. f(x) -> y.

In order to see how well we are doing, we will enter a Kaggle competition to compete for the best accuracy with our predicted classifications. Kaggle is a website that hosts competitions on predicitive analytics in order for researchers and people to produce the best predictive models, and I will teach you how to easily create a neural network that will earn you a top 50 finish! There will be some initial set up if you want to follow along, but if you don't you will be able to read the code and interact with the neural network right here on this blog!

<a name='setup'></a>
##Optionally Setup Lasagne
For this setup we are going to use the python neural network library Lasagne. There are several other neural network libraries out here such as TensorFlow (we will get to this one in the next blog post), Keras, Caffe, etc. A majority of computer scientists tend to use python when using neural networks (this will be clear in the next blog post LINK), so we will use Lasagne as a basis since it uses python. To setup Lasagne, click the link to the blog post below. When you complete the installation, you will be redirected back here. If you have any trouble installing or have advice to make it more clear, feel free to reach out!

[Setup Lasagne](http://pauljs.github.io/Dual-Booting-Ubuntu-and-Installing-Lasagne/)

<a name='examples'></a>
##Lasagne Examples
Now that you have successfully installed Lasagne, we are going to take a quick glimpse at the provided examples. To view the examples we need to download them by cloning the Lasagne github repository by using the command:

```
git clone https://github.com/Lasagne/Lasagne.git
```

  - This may require you to install git. Look [here](http://git-scm.com/documentation) if you don't know what git is and [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) if you need help installing. As long as git is installed, you don't need to know how to use git for this tutorial. Once you have git installed use the above command to get the Lasagne examples

Go ahead and move into the Lasagne folder by using:

```
cd Lasagne/examples
```

Here you will find will find an example python file named "mnist.py" which contains a few neural networks built to handle the MNIST images and to learn how to classify them by their respective numbers. We can actually just run the python file and see the working example go. Use the following command to start:

```
python mnist.py
```

- First, if you have GPU enabled, you should see a statement stating a gpu device is being used. If you don't, you will be using your CPU.
- Next the file will attempt to load the MNIST images into the program. If the images are not downloaded, then the program will go ahead and download them for you
- You will then see the program state it is "Building model and compiling functions...". What this is really doing is creating your neural network for you before it starts to learn how to classify the MNIST images.
- Next it will start training the neural network in order for it to learn how to classify the images. There will be some terminology such as "Epoch, training loss, validation loss, validation accuracy" that will be unfamiliar to you. This will be explained in the next blog post in full but a brief explanation for each is put below:

  - **Epoch**: This represents 1 run through of all images used for training the neural network. In the MNIST dataset, 50,000 images are used for training, so 1 epoch represents presenting each of these 50,000 images to the neural network to learn
  - **Loss**: This represents the error in our neural network's classification predictions.
    - **Training loss**: The error when using only the images used for training.
    - **Validation loss**: The error when providing the neural network with the 10,000 validation images. Validation images are separate from the training images because we want to get a glimpse of how well our neural network would do given new images.
  - **Validation accuracy**: This gives the percent the neural network predicts correctly out of the given 10,000 validation images.
- Once the 500 epochs are run through, you will see a final message stating the results with the test data. The test data contains 10,000 test images, similar to the validation data, but the neural network does not use the test data to learn from. You should get a final test result around 98% (I got 98.72%).

Now you may be thinking, "you said < 1%? I should be getting at least 99%!" To get < 1%, we are going to edit the example given to us slightly in order to not only give a better accuracy, but to also allow easy input from our Kaggle competition.

<a name='kaggle'></a>
##Kaggle Competition

Now is a great time to start the Kaggle competition. Go ahead and go to [Kaggle's website](https://www.kaggle.com/) and make an account. Once you have, make your way to the [Digit Recognizer competition](https://www.kaggle.com/c/digit-recognizer). From this page you can see the goal is to classify the MNIST dataset. Go to the next section [Get the Data](https://www.kaggle.com/c/digit-recognizer/data) in order to download the data. From the description we can grasp these key points:

- Images are 28 pixels by 28 pixels for a total of 784 pixels
- Each pixel value is integer ranging in value between 0 and 255 inclusive, indicating lightness and darkness of a pixel. 0 represents white and 255 is black
- We are given a train.csv file of 42,000 training images. There is a title row to tell what each column is, and each row represents a different image. Additionally the first column is the label column which represents what number the image represents.
- We are given a test.csv file that is the same as the train.csv file, but without the first column (without the label column), and only 28,000 test images.
- Images are layed out in the csv file in a row from pixel 0 to pixel 783. To put back into proper 28 x 28 form, we can just take batches of 28 pixels and stack them horizontally.

Lets go ahead and download the train.csv and test.csv files and move them to the same directory as the mnist.py. Additionally, lets make a copy of mnist.py and call it "kaggle-mnist.py" so we can preserve the original.

```
cp mnist.py kaggle-mnist.py
```

Looking at kaggle-mnist.py, we see we have several functions:

```python
# Loads the MNIST dataset and downloads it if not in the same directory
def load_dataset()
# The next three functions creates neural networks of varying types
def build_mlp()
def build_custom_mlp()
def build_cnn()
# Takes a random sample of the training images and returns them
def iterate_minibatches
# Starts the main program
def main
```

In order to make this file work with our Kaggle competition, we need to:

1. Create our own load\_kaggle_dataset function to load our train and test csv files
2. Create a get\_predictions function to see what our neural network predicted
3. Create a save\_predictions function to save our predicted labels in the required csv format
4. Create a save\_neural\_network function to optionally save our neural network at the end of training
5. Create a load\_neural\_network function to optionally load a previously saved neural network to perform testing on

<a name='load-dataset'></a>
### 1. Load Kaggle Dataset
Looking at our main function below we can see the first function is a call to load our dataset

```python
def main(model='mlp', num_epochs=500):
    # Load the dataset
    print("Loading data...")
    X_train, y_train, X_val, y_val, X_test, y_test = load_dataset()
```

We need to replace the X\_train, y\_train, and X\_test with our own personal function load\_kaggle\_dataset. To do this we will load the csv files using Numpy (referred to typically as "np" in python). [Numpy](http://www.numpy.org/) is one of the dependencies requried by Lasagne and is really just a package to do efficient operations on matrices. First let's define our function above the previous load\_dataset function.

```python
def load_kaggle_dataset():

```

Now lets load our training data through a numpy function [genfromtxt](http://docs.scipy.org/doc/numpy-1.10.0/reference/generated/numpy.genfromtxt.html) that loads data from text files.

```python
  # loads data into at Numpy array using a comma indicate a 
  # new element. dtype represents the type the data will be
  # loaded as. We choose float32 since the original dtype 
  # is float64, whose precision is unstable when placed on
  # the GPU
  training_data = np.genfromtxt('train.csv', delimiter=",", dtype="float32")
```

But remember that the function in the train.csv file is only used to tell us what each column is. We can actually remove this row using Numpy's [delete](http://docs.scipy.org/doc/numpy-1.10.1/reference/generated/numpy.delete.html) function

```python
  # axis=0 means we are deleting a row (axis=0 represents 
  # rows, axis=1 represents columns, etc.)
  # obj=0 means we are deleting the first slice in whatever
  # axis we are in. In this case, we delete the along the
  # rows (axis=0), and we delete the first slice along this
  # axis (obj=0). This means we delete the first row.
  training_data = np.delete(np.genfromtxt('train.csv', delimiter=",", dtype="float32"), obj=0, axis=0)
```

Next we need to separate the training data into images and their respective labels. The first column has the labels and the rest are the images. We also used numpy's [reshape](http://docs.scipy.org/doc/numpy-1.10.1/reference/generated/numpy.ndarray.reshape.html) method to reconstruct the images. (The -1 in the reshape method automatically applies the reshape to each of the training images).

```python
  # List of train images by deleting the 1st column of
  # labels and reshaping the 784 pixels into their 
  # original 28 x 28 image. Additionally, we divide 
  # all pixels by 256 in order to have the range of 
  # pixels between 0 and 1. This is done in order for 
  # neural networks to learn easier, keeping the range 
  # smaller but the proportions the same. (Actually the
  # range [0, 255/256], for compatibility to the version
  # provided at   
  # http://deeplearning.net/data/mnist/mnist.pkl.gz.)
  training_data_X = np.delete(training_data, obj=0, axis=1).reshape(-1, 1, 28, 28) / 256
  
  # List of corresponding labels for the training image.
  # This is just all items from the first column
  training_data_Y = training_data[:, 0]
```

Lastly, we need to load the data from test.csv, which should be exactly the same as loading in the training data but
without the label column

```python
  test_data = np.delete(np.genfromtxt('test.csv', delimiter=',', dtype="float32"), obj=0, axis=0).reshape(-1, 1, 28, 28) / 256

```

The full method is therefore:

```python
def load_kaggle_dataset():
    training_data = np.delete(np.genfromtxt('train.csv', delimiter=",", dtype="float32"), obj=0, axis=0)
    training_data_X = np.delete(training_data, obj=0, axis=1).reshape(-1, 1, 28, 28) / 256
    training_data_Y = training_data[:, 0]
    test_data = np.delete(np.genfromtxt('test.csv', delimiter=',', dtype="float32"), obj=0, axis=0).reshape(-1, 1, 28, 28) / 256
    # training_data_Y is cast to int32 since all labels are integer and for similar reasons as previous castings
    return training_data_X, np.int32(training_data_Y), test_data
```

Now that we create our new load method we need to insert it into our main method. Let's put it right below the previous load function in order to still use the validation data given to us by it, so we can see approximately how well our neural network is doing while it is training.

```python
def main(model='mlp', num_epochs=500):
    # Load the dataset
    print("Loading data...")
    X_train, y_train, X_val, y_val, X_test, y_test = load_dataset()
    # Newly inserted load_kaggle_dataset to repalce X_train, y_train, X_test
    X_train, y_train, X_test = load_kaggle_dataset()
```

Lastly, we need to comment out the code in the main method that would tell us our final test results since we don't know the corresponding labels to our new test data.

```python
# After training, we compute and print the test error:
# Comment all of the code below
'''
test_err = 0
test_acc = 0
test_batches = 0
for batch in iterate_minibatches(X_test, y_test, 500, shuffle=False):
    inputs, targets = batch
    err, acc = val_fn(inputs, targets)
    test_err += err
    test_acc += acc
    test_batches += 1

print("Final results:")
print("  test loss:\t\t\t{:.6f}".format(test_err / test_batches))
print("  test accuracy:\t\t{:.2f} %".format(
    test_acc / test_batches * 100))
'''
```

<a name='get-predictions'></a>
### 2. Get Predictions
Let's look at the current functions for evaluating predictions which can be found in the main function

```python
def main(...):
  ...
  # Create a loss expression for training, i.e., a scalar objective we want
  # to minimize (for our multi-class problem, it is the cross-entropy loss):
  prediction = lasagne.layers.get_output(network)
  loss = lasagne.objectives.categorical_crossentropy(prediction, target_var)
  loss = loss.mean()
  # We could add some weight decay as well here, see lasagne.regularization.

  # Create update expressions for training, i.e., how to modify the
  # parameters at each training step. Here, we'll use Stochastic Gradient
  # Descent (SGD) with Nesterov momentum, but Lasagne offers plenty more.
  params = lasagne.layers.get_all_params(network, trainable=True)
  updates = lasagne.updates.nesterov_momentum(
          loss, params, learning_rate=0.01, momentum=0.9)

  # Create a loss expression for validation/testing. The crucial difference
  # here is that we do a deterministic forward pass through the network,
  # disabling dropout layers.
  test_prediction = lasagne.layers.get_output(network, deterministic=True)
  test_loss = lasagne.objectives.categorical_crossentropy(test_prediction,
                                                          target_var)
  test_loss = test_loss.mean()
  # As a bonus, also create an expression for the classification accuracy:
  test_acc = T.mean(T.eq(T.argmax(test_prediction, axis=1), target_var),
                    dtype=theano.config.floatX)

  # Compile a function performing a training step on a mini-batch (by giving
  # the updates dictionary) and returning the corresponding training loss:
  train_fn = theano.function([input_var, target_var], loss, updates=updates)

  # Compile a second function computing the validation loss and accuracy:
  val_fn = theano.function([input_var, target_var], [test_loss, test_acc])
```

  - From the descriptions above, we can see that "test\_prediction" contains the predictions for the test images. However, we can't access these directly due to the nature of how Lasagne works. Lasagne uses Theano which ports directions on implementation to a more efficient language to do fast computations (see the following post for a more in depth description). You can think of "test\_prediction" as currently being in that other language, and we need to make a Theano function in order to obtain its values. This is why we have "train\_fn" and "val\_fn" which gives us access to values in the other language. Thus, we just need to create a function that returns the values of test\_prediction. We will place this below val\_fn.

```python
  # Get test predictions
  # test_prediction contains the probabilities of the image 
  # being each number for each image. In other words,
  # test_prediction contains arrays of length 10 where each
  # array contains 10 percentages representing the 
  # probability that an image is a particular number. For
  # example, [0.1, 0.2, 0.1, 0.05, 0.05, 0.025, 0.025, 0.15, 0.1, 0.1] 
  # represents the image having a 10% probability of being
  # a number 0, 20% probability of the image being a number
  # 1, etc. We want to take the number with the highest
  # probability which is why we use Theano's argmax function
  # to do so. Theano's argmax function gives us the index of
  # the probability (which in this case is also the number
  # with the highest probability). We take the max across a 
  # row (axis=1), which is for each array of length 10.
  # get_test_predictions = T.argmax(test_prediction, axis=1)
  # We create our function to obtain the values of the 
  # test_predictions. The theano function takes input_var 
  # which is the variable in the function representing our 
  # images input, and use the get_test_predictions 
  # directions we created to produce the values.
  test_predictions_fn = theano.function([input_var], get_test_predictions)
```

<a name='save-predictions'></a>
### 3. Save predictions
Now that we have a way to get our predictions we need to create a save predictions method to save our answers to a file. We can place this function save_predictions right before our main function. It is not obvious from [Kaggle's submission page](https://www.kaggle.com/c/digit-recognizer/submissions/attach) what format the csv file should be. The csv needs to columns, one titled "ImageId" and the next titled "Label". Image ids are from 1 to 28000 and the predicted labels are already in that order.

```python
# Take our new function test_predictions_fn as the first 
# argument and X_test as the second in order to obtain 
# the predicted labels from it. We will make the saved 
# file as "predicted_labels.csv"
def save_predictions(test_predictions_fn, X_test):
  filename = "predicted_labels.csv"
  # Call to our newly defined functions to get X_test's
  # predicted labels
  output = test_predictions_fn(X_test)
  # We open our file to write over any file already 
  # named the same ("w" stands for write)
  text_file = open(filename, "w")
  # Create the column titles
  text_file.write("ImageId,Label\n")
  # We close the file in order to append to it later
  text_file.close()
  # i represents the Image ids
  i = 1
  # We open our file where each write is now appended to 
  # the file ("a" stands for append)
  text_file = open(filename, "a")
  for label in output:
      text_file.write("%d," % i)
      i += 1
      text_file.write("%d\n" % label)
  text_file.close()
```

We are going to hold off on inserting this function into our main method for now. The reason why will be explained below.

<a name='save-nn'></a>
### 4. Save the neural network
Luckily at the bottom of the kaggle-mnist.py file, we have a suggested method to save the neural network. 

```python
# Optionally, you could now dump the network weights to a file like this:
# np.savez('model.npz', lasagne.layers.get_all_param_values(network))
```

We will use this in a defined function save_nn which you can place after the main method.

```python
def save_nn(network, filename):
  # Gets all of the parameters of the neural network
  all_params = lasagne.layers.get_all_params(network)
  # Saves the parameters to a filename(in this case it will be 
  # model.npz) with the array title 'network'
  np.savez(filename, network=lasagne.layers.get_all_param_values(network))
```

Now place the newly defined method in your main method

```python
# Optionally, you could now dump the network weights to a file like this:
# np.savez('model.npz', lasagne.layers.get_all_param_values(network))
# .npz is a file format for saving numpy arrays
filename = "model.npz"
save_nn(network, filename)
```

<a name='load-nn'></a>
### 5. Load a saved neural network
We will now create a function load\_nn and place right after the save\_nn function

```python
def load_nn(network, filename):
  # Load the file using numpy
  all_param_values = np.load(filename)
  # Set all the parameter value to our saved neural network.
  # This is just doing the opposite of our save_nn function
  lasagne.layers.set_all_param_values(network, all_param_values['network']) 
```

To make sure this works you can place this right after the save\_nn function call in your main method

```python
# Optionally, you could now dump the network weights to a file like this:
# np.savez('model.npz', lasagne.layers.get_all_param_values(network))
filename = "model.npz"
save_nn(network, filename)
load_nn(network, filename)
```

Lastly, we are now going to insert our save\_predictions function after our load\_nn function. The key really is to save the function after our save_nn function. The reason why is because there are sometimes memory issues with retrieving all of our test image predictions at once; we might not have enough memory to pull all 28,000 image predictions at once from Theano. We will fix this if you have this problem when running the program below.

<a name='run'></a>
### Run your neural network!
We are ready to run the neural network! However, before we run the program I want you to note some approximate benchmarks for how long the program will take to, depending on the type of neural network and whether you use a GPU.

<table class="border-table">
  <tr>
    <th></th>
    <th>CPU Time Per Epoch (sec)</th>
    <th>GPU Time Per Epoch (sec)</th>		
  </tr>
  <tr>
    <td>mlp</td>
    <td>18</td>
    <td>1</td>
  </tr>
  <tr>
    <td>cnn</td>
    <td>240</td>	
    <td>6</td>	
  </tr>
</table>

The CPU times can vary depending on your machine, but the point is that if we run the default of 500 epochs, CPU times can take hours to even days to complete depending on the size of dataset and neural network! This is why a GPU is highly recommended for creating neural networks.

Now let's go ahead and run a test of our program! On the terminal run this command to start:

```
# We pass the argument 'cnn' in order to run a particular type of 
# neural network which will provide better accuracy for
# this problem. We give another argument 1 to run only 1 epoch
python kaggle-mnist.py 'cnn' 1
```

After the 1 epoch is run, see if you get this message:

```
Error allocating 2064384000 bytes of device memory (out of memory). Driver report 1774694400 bytes free and 2146762752 bytes total
...
```

If you do then you ran out of memory when attempting to get our test prediction values from Theano. I wanted you to see this error in case it happens in the future. To fix this follow the next section. If you didn't get this error, great! But you should still follow the next section because this error will probably happen to you if you move on to more complex neural networks.

#### Memory issues
If you look closely at your error you will see that it occurs in our save\_predictions method. Specifically, it occurs at our call to the theano function test\_predictions\_fn. The X\_test we pass to this theano function is requesting too large of a numpy array to return; it is able to calculate the answers but can't bring it back from the theano function. To fix this all we need to do is split our X\_train into several parts and make a several calls to our theano function test\_predictions\_fn to get answers in smaller chunks.

```python
def save_predictions(test_predictions_fn, X_test):
  filename = "predicted_labels.csv"
  text_file = open(filename, "w")
  text_file.write("ImageId,Label\n")
  text_file.close()
  # We split our test images into 5 sets
  splits = np.split(X_test, 5)
  i = 1
  # For each split we get their predicted labels and append them 
  # to our save file
  for split in splits:
      output = test_predictions_fn(split)
      for label in output:
          text_file = open(filename, "a")
          text_file.write("%d," % i)
          i += 1
          text_file.write("%d\n" % label)
          text_file.close()
```

#### Submitting to Kaggle
Now that we fixed the memory issue we can finally get our predictions! Go ahead and run the following command:

```python
python kagggle-mnist.py 'cnn'
```

When it is complete you will find the predicted_labels.csv file in your directory. Then, head on over to the [Kaggle submission page](https://www.kaggle.com/c/digit-recognizer/submissions/attach) and submit the file. When Kaggle completes the upload you should have an accuracy around 99%! (I got 99.414%).

As stated a few times in this tutorial, more specifics on how libraries like Lasagne and Theano work will be mentioned in the next blog post, but this time using Google's TensorFlow. After that we will start diving into research papers on deep learning and neural networks to understand how neural networks work and what researchers are looking into in order to improve deep learning. See you in the next post!
