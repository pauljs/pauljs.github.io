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
The purpose of this post is to provide a step-by-step instruction on:
1. Dual-booting Ubunutu on a Windows machine  
2. Installing dependencies needed to install Lasagne
3. Installing Lasagne
4. Optionally enable GPU processing which is highly recommended
5. Optionally install NVIDIA's library cuDNN to speed up convolutional neural networks.

This post is supposed to serve as an intermediate step in order to allow readers to follow along in the post [The Power of The Power of Neural Networks and A Kickstart through Kaggle](http://pauljs.github.io/How-do-I-Neural-Network-A-Kaggle-Explanation/), but you are more than welcome to use any part of it.

Before starting the step-by-step instructions, I want to make sure you understand what is required for installation.  
- Step 1 of this tutorial is meant for Windows machines (8/8.1/10) that will dual-boot ubuntu. Dual-booting ubuntu will require a portion of your memory (specifics in Step 1). If you are sshing into a computer running Linux, or have a computer running Linux / Mac system then you can move to Step 2.
- Step 4 of these instructions highly recommends enabling GPU support for Lasagne. The reason why is that using the GPU causes a near 50 fold increase in speed. This is significant especially when working with large neural networks and large datasets! If you are using your personal computer, check to see if your computer has a GPU. My computer has a GEFORCE GTX 660M with 2GB and has a compute capability of 3.0. To check your compute capability, you can go to NVIDIA's website here. Compute capabilities are just relative, so don't worry what they actually mean. Just because your computer does not have a GPU does not mean you can't use just, your CPU (this is the default when you intall Lasagne without Step 4). Just note that running neural networks and ob
- taining results will take a bit longer!
- Step 5 is an additional speed up when using convolutional neural networks. When I initially installed Lasagne I did not use this and the 50x speed up from Step 4 was great by itself! This step requires that you have a GPU with compute capability of at least 3.0.

Now let's start the setup!
### Step 1: Dual-boot Ubuntu
Requirements: Windows 8/8.1/10 and at least 2 GB USB Flash Drive (the USB will have to be reformatted to contain the Ubuntu download so if you have anything important on your USB be sure to copy it somewhere safe for it will be removed when installing Ubuntu on it)

For dual-booting Ubuntu, I followed [this Youtube video](https://www.youtube.com/watch?v=hOz66FC0pWU) though the video skips out on some steps with Windows BIOS and accessing both Ubuntu and Windows at the end. I also provided step-by-step instructions from the video below.  
**1.** First you will ned to turn off fast boot for Windows. To do this, search for "control panel" by pressing the windows key and typing "control panel." Click the option for control panel. (I used this [link](http://www.eightforums.com/tutorials/6320-fast-startup-turn-off-windows-8-a.html) as a guide).  
**2.** In the control panel, click "System and Security" and then click "Power Options."  
**3.** In the Power Options menu, click "Choose what the power buttons do"  
**4.** Under "Shutdown settings", uncheck "Turn on fast startup (recommended)." You can close the PC Settings menu now.  
**5.** We will need to mark down how much RAM you have. To do this, open a File Explorer and right click on "This PC" or "Computer" and click "Properties." You will see under System, "Installed memory (RAM): " and the amount of RAM you have. Write this down for it will be needed later.
**6.** Now, you will need to partition part of your hard drive that will contain Ubuntu. This is really just taking extra memory you have left and ysing it for your new operating system. Search your computer by pressing the windows key and search for "Disk Management." On Windows 8/8.1 you will click on "" and Windows 10 you will click on "Create and format hard disk partitions."  
**7.** We will now shrink some of the space you have for Windows in order to provide space for Ubuntu. Right click on the partition marked (C:) (or the partition with the largest space) and click shrink.  
**8.** In the "Enter the amount of space to shrink in MB: " space, enter your amount. This amount depends how much you will be working in Ubuntu. If you are going to be working in Ubuntu full time or a lot, the video suggests 80 to 100 GB (8192 MB or 102400 MB). If you are not going to be working in Ubuntu full time, the video suggests 30 GB - 50 GB (30750 MB or 51250 MB). I used around 100 GB, and my computer has around 450 GB of storage. (Keep in my in a later step, it will require a final 2 GB - 4GB more of your storage for a different part).  
**9.** After you enter the amount press shrink. You should now have an "Unallocated" amount in the bottom right portion of the Disk Management screen.  
**10.** Now we will download Ubuntu Desktop to prepare for installation. Go to Ubuntu's website's [downloads for desktop](http://www.ubuntu.com/download/desktop) and choose which version of Ubuntu you want. At the time of this tutorial, 14.04 LTS has the most stability and the Youtube video uses this as well. After choosing your version, click Download.  
**11.** In addition to Ubuntu, we need to download the Universal USB in order to install Ubuntu through a USB. Go to its [website](http://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3/) and click the "Download UUI" button.  
**12.** Once it has downloaded, double click the Universal USB executable and agree to the terms.  
**13.** On the "Setup your Selection Page," select Ubuntu in the dropdown for Step 1's Linux Distribution.  
**14.** Browse to find the Ubuntu iso you downloaded and select it for Step 2.  
**15.** Connect your USB to your computer and select your USB in Step 3. Do not remove the USB until told to do so!  
**16.** Click Create and then click yes to accept what will be done to the USB (any files will be deleted on the USB!), and it will start installing Ubuntu onto your USB.  
**17.** When the installation is finished, we will need to enter Windows BIOS (a program that helps start your computer) in order to boot from the USB drive to allow us to install Ubuntu from the USB. To enter BIOS, you need to restart your computer and when restarting press and hold the F2 key for a majority of laptops. (For some laptops you may need to press the F12 key and hold instead). Keep in mind that you should have this tutorial open on a different device in order to see next steps.  
**18.** Now that you are in BIOS, move over to the Boot menu by pressing the right key twice. Under "Boot Option Priorities" you should see a few Boot Options including your USB Flash Drive. If it is not in Boot Option #1, we will need to switch it to that position. To do so, press the down key until you are highlighting the "Boot Option #1" row, and press the enter key. Move down until you highlight your USB and then press the enter key. Your USB should now be selected for Boot Option #1. If you need to exit a Boot Option menu press the escape key.  
**19.** With your USB as the Boot Option #1, move to the Save & Exit menu by pressing the right key twice.  
**20.** Press enter on the "Save Changes and Exit" and press enter on the highlighted yes to exit the BIOS.  
**21.** Upon restart you'll be show the Welcome screen for Ubuntu Installation. Select your language (typically English) and click "Install Ubuntu."  
**22.** On the "Preparing to install Ubuntu" screen, optionally select the check marks for "Download updates while installing" and "Install this third-party software" though it is recommended by the video. I did select both of these. Click continue when you are done.  
**23.** On the "Installation type" screen, select the "Something else" option. People have had issues with selecting the "Install Ubuntu alongside Windows 8" option where the option does not work for everyone, so we will do it manually to ensure success. Once you select the "Something else" option, click continue.  
**24.** On this new screen you will see your different disks of memory similar to the screen earlier when you shrunk your memory to make room for Ubuntu. This step is for making a swap area. If your computer has a solid state drive (SSD) then you do NOT need a swap area, otherwise it will eat into the life of your SSD. If your computer has a hard drive then you do need a swap area. A swap area is extra space to allowing for memory optimization, freeing memory, and hibernation in Ubuntu. For more information on swap, see [Ubuntu's FAQs on swap](https://help.ubuntu.com/community/SwapFaq). If you need the swap area (I did), select the "free space" row and click the "+" button. On the "Create partition" screen, in the size field, enter the size you want for your partition. In Ubuntu's FAQs for swap, it suggests using a minimum size equal to how much RAM you have "if you use hibernation." If you do not use hibernation, you need a minimum of round(sqrt(RAM)) and a maximum of twice the amount of RAM. For example, since I have 8 GB of RAM, and I do not use hibernation, I needed a minimum size of 3 GB for my swap (I ended up using 4 GB or 4096 MB). Calculate what you need using the amount of RAM you marked down and enter the size amount in MB in the size box. Then select "swap area" in the drop down for "Use as". Click ok when done.  
**25.** Click the "free space" row to highlight it if it isn't already highlighted and click the "+" button. Make sure "Ext4 journaling file system" is selected in the "Use as" dropdown (it should already be preselected). Under the drop down for "Mount point", select the option "/" which means root. Then select ok.  
**26.** Lastly for this screen, you want to look at the row that contains your "Windows (loader)" (under the System column). It should look something like "/dev/sda1" under the "Device" column (though "sda" may be swapped with sdb or sdc, etc. and the number may be different but most likely 1). Note what the three letters (sda, sdb, or sdc, etc.). These three letters represent your hard drive that contains the Windows loader, and you want to put the Ubuntu loader in the same location. The three letters with a number appended is a certain partition on the hard drive. With the "free space" row selected, under the "Device for boot loader installation:" dropdown you want to make sure the hard drive matching the three letters (without the appended number) you noted is selected. For example, my Windows 8 (loader) has a Device "/dev/sda1". This means in the dropdown for "Device for boot loader installations:" I selected "/dev/sda" since the "/dev/sda" matches that from my Windows 8 (loader). Once this is selected, there should now automatically be a check mark in the row for "free space" under the column "Format?". Make sure all of this is done correctly otherwise it will not work.  
**27.** Click Install Now  
**28.** Type the location of where you are or a major city that is in your time zone in order for your clock to be set correctly. Click continue.  
**29.** Next, select your Keyboard layout. (I selected "English (US)") and then click continue.  
**30.** Type your name and the "Your computer's name" box should be auto-filled. Feel free to change your computer's name if you'd like by just stuck with the default. Then type in your username, your password, and confirm your password. Then click continue.  
**31.** You will then be asked to restart your computer. Before you restart you need to remove your USB Flash Drive now! If you don't then you will then boot from your USB and will start you back at the Welcome screen for installing Ubuntu (it shouldn't delete your newly installed Ubuntu; you will just have to restart again and remove the USB). Go ahead and restart your computer. Upon restart you will see a screen titled "GNU GRUB" where GRUB stands for GRand Unified Bootloader. This bootloader is synonymous to the BIOS we visited for Windows, but just think of it as Ubuntu's version. You will want to press enter on the highlighted Ubuntu. You may wonder why there is no option to select your "Windows (loader)" in order to start Windows. The reason why is because we need to let GRUB know that it is available (this is NOT mentioned in the Youtube link!). Press enter on Ubuntu if you have not done so and we will do this now to complete the installation!  
**32.** Log into your account and open up a terminal (CTRL + ALT + T). Type "sudo update-grub" then press enter. You may have to enter your password when prompted. This will let GRUB recognize your Windows (loader). Now when you restart your computer you will have the option to select Windows (loader). You can move down to this and press enter to start Windows, or press enter on Ubuntu to start Ubuntu. Also keep in mind GNU GRUB has a timer. If you move or select anything in the time limit it will just default to the first option. Congratulations on dual-booting Ubuntu!  
### Step 2: Installing Lasagne Depedencies
### Step 3: Installing Lasagne
### Step 4: Optionally Enable GPU support (Highly Recommended!)
### Step 5: Optionally Install NVIDIA's library cuDNN to speed up Convolutional Neural Networks

## Start Following the First Post!
LINK TO FIRST POST Section
