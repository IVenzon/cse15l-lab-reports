# CSE 15L Week 7 Lab Report: CLDQ – CSE Labs “Done Quick”

*Ian Venzon - Thursday 12:00 PM - B270*

## The Tasks:

In this lab report, we will be trying to complete a list of 9 tasks as quickly as possible by any means necessary. Our job is to complete the following:

1) **Setup pt. 1:** Delete any existing forks of the repo on your github account and on your ieng6 account.
2) **Setup pt. 2:** Fork the following [repository](https://github.com/ucsd-cse15l-w23/lab7).
3) Start the timer!
4) Log into your ieng6 account.
5) Clone the fork you made of the [repository](https://github.com/ucsd-cse15l-w23/lab7).
6) Run the tests (They should fail here!).
7) Edit the code to fix whatever is causing the failures.
8) Run the tests again (They should all pass here!)
9) Commit and push the changes you made to your GitHub account.

While these tasks are fairly straightforward, there are lots of ways to optimize your execution of them to lessen the amount of time needed or the amount of keystrokes used (hopefully both!).

## My (admittedly slow) approach:

The first three steps are the same for every person, so I won't really go in depth here. For step 1, if you can't find where to delete your fork of the repository, first go to your fork of the repo and click the "Settings" tab. Scroll all the way to the bottom of the page, and then click the "Delete this repository" button.

![Image](https://i.imgur.com/8QUaftB.png)

### Step 4: Log into ieng6

![Image](https://i.imgur.com/mSLyiPN.png)

For this step, I typed out `ssh cs15lwi23asn@ieng6.ucsd.edu` and then hit `<enter>`. Not much more to this step.

### Step 5: Clone the fork of the repository

![Image](https://i.imgur.com/9h4AxG7.png)

For this step, I typed out `git clone `, pressed `ctrl + V` to copy the link to my forked repo, then finally hit `<enter>`.

### Step 6: Run the tests for the first time (failure expected)

![Image](https://i.imgur.com/bF05mlc.png)

This step is a little more involved, so I will break it down line by line.

The first thing I typed was `cd la`, then I pressed `<tab>` to autocomplete and then pressed `<enter>`.

Next, I entered `ctrl + R` and typed `javac` until it found `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java` from my history, then I pressed `<enter>`.

Lastly, I entered `ctrl + R` once again and typed `j`. This time it immediately found `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests` and I hit `<enter>` to run the tests.

### Step 7: Edit the code to fix the problem

![Image](https://i.imgur.com/XJ5Wnt1.png)

![Image](https://i.imgur.com/MKDmfwn.png)

#### Before:
![Image](https://i.imgur.com/beRCaxB.png)

#### After:
![Image](https://i.imgur.com/6gFgWgW.png)

This is the most complex step of the entire process, so once again I will break it down line by line.

First, I typed `nano L` then hit `<tab>` to autocomplete and hit `<enter>`.

Next, I entered `ctrl + O` then hit `<enter>`.

Then, I pressed the `<down>` arrow until it was on the line I wanted, then I pressed the `<right>` arrow until it was at the position seen in the third image.

After this, I pressed `<backspace>` and then `2` to implement the fix. After this I entered `ctrl + X` and then `Y` to save my changes, then hit `<enter>` a final time to save my changes.

### Step 8: Run the tests for the second time (should now all pass)

![Image](https://i.imgur.com/6ze55KL.png)

For this step, I only pressed the arrow keys in the following way:

For the first line, the `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java` command was 2 up in the history, so I entered `<up> <up>` and then `<enter>`.

For the second line, the `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests` command was 3 up in the history, so I entered `<up> <up> <up> <up>` followed by `<enter>` to run the tests once again.

### Step 9: Commit and push the changes made to GitHub

![Image](https://i.imgur.com/BK3mtBb.png)

For this last step, I did the following:

First, I typed `git add L` then hit `<tab>` to autocomplete, then typed `.java` and hit `<enter>`.

Then, I typed `git commit -m "Fixed the bug"`.

Lastly, I typed `git push` to push my changes to my forked repository. Now if I look at my fork, the changes I made through the terminal show up!

#### Here is my commit message:
![Image](https://i.imgur.com/X9KOSnX.png)

#### And here is the code after I pushed the fixes:
![Image](https://i.imgur.com/B8Ex26R.png)

Obviously, there are much, much faster ways to execute these nine tasks. However, when I tried pushing for a faster time I kept on making errors that ended up costing me time instead. The steps that I have laid out in this lab report gave me the best balance between speed and accuracy out of all of my attempts.
