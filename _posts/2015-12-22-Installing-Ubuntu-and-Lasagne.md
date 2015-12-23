---
layout: post
title: Installing Ubuntu and Lasagne
---

Table of Contents:
- [Intro to Installing Ubuntu and Lasagne](#intro)
- [Dual-boot Ubuntu](#dual-boot-ubuntu)
- [Installing Lasagne Depedencies](#dependencies)
- [Installing Lasagne](#lasagne)
- [Enable GPU Support](#gpu)
- [Install NVIDIA's cuDNN](#cuDNN)

<a name='intro'></a>
## Installing Ubuntu and Lasagne
The purpose of this post is to provide a step-by-step instruction on (1) Dual-booting Ubunutu on a Windows machine,
(2) Installing dependencies needed to install Lasagne, (3) installing Lasagne, (4) optionally enable GPU processing
which is highly recommended, and (5) optionally install nvidia's library cuDNN to speed up convolutional neural networks. This post is supposed to serve as an intermediate step in order to allow readers to follow along in the post [The Power of Neural Networks and a Kickstart through Kaggle: An Introduction](), but you are more than welcome to use any part of it.

Before starting the step-by-step instructions, I want to make sure you understand what is required for installation.
- Step 1 of this tutorial is meant for Windows machines (8/8.1/10) that will dual-boot ubuntu. Dual-booting ubuntu will require a portion of your memory (specifics in Step 1). If you are sshing into a computer running Linux, or have a computer running Linux / Mac system then you can move to Step 2.
- Step 4 of these instructions highly recommends enabling GPU support for Lasagne. The reason why is that using the GPU causes a near 50 fold increase in speed. This is significant especially when working with large neural networks and large datasets! If you are using your personal computer, check to see if your computer has a GPU. My computer has a GEFORCE GTX 660M with 2GB and has a compute capability of 3.0. To check your compute capability, you can go to nvidia's website here. Compute capabilities are just relative, so don't worry what they actually mean. Just because your computer does not have a GPU does not mean you can't use just, your CPU (this is the default when you intall Lasagne without Step 4). Just note that running neural networks and ob
- taining results will take a bit longer!
- Step 5 is an additional speed up when using convolutional neural networks. When I initially installed Lasagne I did not use this and the 50x speed up from Step 4 was great by itself! This step requires that you have a GPU with compute capability of at least 3.0.

Now let's start the setup!
### Step 1: Dual-boot Ubuntu
Requirements: Windows 8/8.1/10 and at least 2 GB USB Flash Drive (the USB will have to be reformatted to contain the Ubuntu download so if you have anything important on your USB be sure to copy it somewhere safe for it will be removed when installing Ubuntu on it)

For dual-booting Ubuntu, I followed [this Youtube video](https://www.youtube.com/watch?v=hOz66FC0pWU). I also provided step-by-step instructions from the video below.  
1. First you will ned to turn off fast boot for Windows. To do this, search for "control panel" by pressing the windows key and typing "control panel." Click the option for control panel. (I used this [link](http://www.eightforums.com/tutorials/6320-fast-startup-turn-off-windows-8-a.html) as a guide).  
2. In the control panel, click "System and Security" and then click "Power Options."  
3. In the Power Options menu, click "Choose what the power buttons do"  
4. Under "Shutdown settings", uncheck "Turn on fast startup (recommended)."  
5. Now, you will need to partition part of your hard drive that will contain Ubuntu. This is really just taking extra memory you have left and ysing it for your new operating system. Search your computer by pressing the windows key and search for "Disk Management." On Windows 8/8.1 you will click on "" and Windows 10 you will click on "Create and format hard disk partitions."  
6. We will now shrink some of the space you have for Windows in order to provide space for Ubuntu. Right click on the (C:) drive and click shrink.  
7. In the "Enter the amount of space to shrink in MB: " space, enter your amount. This amount depends how much you will be working in Ubuntu. If you are going to be working in Ubuntu full time or a lot, the video suggests 80 to 100 GB (8192 MB or 102400 MB). If you are not going to be working in Ubuntu full time, the video suggests 30 GB - 50 GB (30750 MB or 51250 MB). I used around 100 GB, and my computer has around 450 GB of storage. (Keep in my in a later step, it will require a final 2 GB - 4GB more of your storage for a different part).  
8. After you enter the amount press shrink. You should now have an "Unallocated" amount in the bottom right portion of the Disk Management screen.  
9. Now we will download Ubuntu Desktop to prepare for installation. Go to Ubuntu's website's [downloads for desktop](http://www.ubuntu.com/download/desktop) and choose which version of Ubuntu you want. At the time of this tutorial, 14.04 LTS has the most stability and the Youtube video uses this as well. After choosing your version, click Download.  
10. In addition to Ubuntu, we need to download the Universal USB in order to install Ubuntu through a USB. Go to its [website](http://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3/) and click the "Download UUI" button.  
11. Once it has downloaded, double click the Universal USB executable and agree to the terms.  
12. On the "Setup your Selection Page," select Ubuntu in the dropdown for Step 1's Linux Distribution.  
13. Browse to find the Ubuntu iso you downloaded and select it for Step 2.  
14. Connect your USB to your computer and select your USB in Step 3. Do not remove the USB until told to do so!  
15. Click Create and then click yes to accept what will be done to the USB (any files will be deleted on the USB!), and it will start installing Ubuntu onto your USB.  
16. When the installation is finished, we will need to enter Windows BIOS (a program that helps start your computer) in order to boot from the USB drive to allow us to install Ubuntu from the USB. To enter BIOS, you need to restart your computer and when restarting press and hold the F2 key for a majority of laptops. (For some laptops you may need to press the F12 key and hold instead). Keep in mind that you should have this tutorial open on a different device in order to see next steps.  
17. Now that you are in BIOS, move over to the Boot menu by pressing the right key twice. Under "Boot Option Priorities" you should see a few Boot Options including your USB Flash Drive. If it is not in Boot Option #1, we will need to switch it to that position. To do so, press the down key until you are highlighting the "Boot Option #1" row, and press the enter key. Move down until you highlight your USB and then press the enter key. Your USB should now be selected for Boot Option #1. If you need to exit a Boot Option menu press the escape key.  
18. With your USB as the Boot Option #1, move to the Save & Exit menu by pressing the right key twice.  
19. Press enter on the "Save Changes and Exit" and press enter on the highlighted yes to exit the BIOS.  
20. 
### Step 2: Installing Lasagne Depedencies
### Step 3: Installing Lasagne
### Step 4: Optionally Enable GPU support (Highly Recommended!)
### Step 5: Optionally Install NVIDIA's library cuDNN to speed up Convolutional Neural Networks

## Start Following the First Post!
LINK TO FIRST POST Section
