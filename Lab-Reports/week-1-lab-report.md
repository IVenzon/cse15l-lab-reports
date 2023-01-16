# CSE 15L Week 1 Lab Report: How to log in to ieng6

*Ian Venzon - Thursday 12:00 PM - B270*

## Step 1: How to install VScode:

The first step to installing VScode is to go to the [official VScode website](https://code.visualstudio.com/). Click on download and use the appropriate installer for your operating system. 

![Image](https://i.imgur.com/9zkNfu2.png)

Once VScode is installed on your system, run it, and if everything went smoothly, you should be greeted by a screen similar to the following.

![Image](https://i.imgur.com/CxOildq.png)

## Step 2: How to remotely connect:

Now that we have VScode installed, we can now remotely connect! This will be a very useful skill to know for future CSE courses as well as in the industry. However, before we begin, there are a few things you need to set up beforehand:

1. **Install git (for Windows):** You can download git for Windows [here](https://gitforwindows.org/). 
2. **Set up your course specific account:** Many CSE courses at UCSD have their own course specific account. You will first need to look up your account [here](https://sdacs.ucsd.edu/~icc/index.php). Follow the instructions carefully, and keep note of the username of your course account, as you will need to use it later.
3. **Open up terminal:** There are many ways to use terminal, but in this tutorial I will use VScode to open the terminal. To do this, press Shift + Ctrl + \` and it should open at the bottom of your VScode window.

If you followed those three steps correctly, you're now ready to remotely connect! This is the part where you'll need your course account name and password.

First, type out the following command in your terminal.

`$ ssh cs15lwi23___@ieng6.ucsd.edu`

Note that the $ is part of the terminal and you do not need to type it yourself. You will also need to replace ___ with the letters at the end of your course account name (there can be two or three letters).

![Image](https://i.imgur.com/9smKSyP.png)

**NOTE:** If you get the following message (or something similar to it), type 'yes' and then press enter.

`# On your client
⤇ ssh cs15lwi23___@ieng6.ucsd.edu
The authenticity of host 'ieng6-202.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])?`

Now enter the password you set earlier for your course account. Keep in mind that while you type your password you will not see any changes to the terminal window. Don't worry, this is the normal, intended behavior. Once you finish typing your password, just hit enter and you should see this message pop up.

![Image](https://i.imgur.com/NUhqwO7.png)

Congrats, you're now connected remotely to a computer in the CSE basement! Any commands that you enter and run from now on will be executed on that computer.


## Step 3: Trying out some commands:

Now that you're logged in remotely, you can start typing out some commands!

One useful command to keep yourself organized is `pwd`, which stands for *print working directory*. This command will display your current directory as an absolute path, starting from the root directory.

![Image](https://i.imgur.com/nLGlOVO.png)

As we can see, our directory starts in the root (/home) and ends at our account folder (which for me, is /cs15lwi23asn).

Another useful command is `ls`. This command will list all the files in the current directory. 

![Image](https://i.imgur.com/HLtXrGG.png)

In particular, the `ls -a` command will list all the files within the directory INCLUDING all hidden filetypes. In Linux, files which start with a '.' are considered hidden.

![Image](https://i.imgur.com/GSLVcVS.png)

Notice how many more files are listed compared to just using the normal `ls`.

As we can see from our `ls`, there is a text file *hello.txt* within our current directory. If you wanted to know the contents of a .txt file, one command you can use is the `cat` command. The `cat` command will first check if the file you have chosen is valid. If it is, then it will print the contents of the file to the terminal. If no such file is found, then it will return an error.

![Image](https://i.imgur.com/72Aej4E.png)

When you are done with your remote session, it is important to remember to log out. The `exit` command or simply inputing `Ctrl + D` will kill your session and log you out of ieng6.

![Image](https://i.imgur.com/Eb0MwcR.png)
