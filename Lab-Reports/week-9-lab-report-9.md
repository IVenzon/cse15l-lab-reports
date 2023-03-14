# CSE 15L Week 9 Lab Report: Simple Grading Script using Bash

*Ian Venzon - Thursday 12:00 PM - B270*

## Gradescope at Home

For this lab report, we will be covering `grade.sh`, a simple bash script that takes in a student submission for `ListExamples.java`, runs some tests to check for possible compile/runtime/output errors, then gives an appropriate grade based on the observed behavior.

Here is the entirety of `grade.sh`. At the moment it is configured for a Windows machine, but it can be converted for Mac/Linux very easily.

```
# CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar' # uncomment this line and comment the line below if on Mac
CPATH=".;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar"

#--------------------------------------------------
# PART 1: CLONING AND CHECKING FOR CORRECT FILES
#--------------------------------------------------

rm -rf student-submission
git clone $1 student-submission
echo 'Finished cloning'

cd student-submission

if [[ -f ListExamples.java ]]
then
    echo 'Correct file found'
else
    echo 'Need ListExamples.java'
    exit
fi

#--------------------------------------------------
# PART 2: SETTING UP FILES FOR TESTING
#--------------------------------------------------

cp ListExamples.java ..
cd ..


rm -rf testing-folder
mkdir testing-folder

cp TestListExamples.java testing-folder
cp ListExamples.java testing-folder
cp -r lib testing-folder

echo 'Files ready for testing'

#--------------------------------------------------
# PART 3: COMPILING STUDENT SUBMISSION
#--------------------------------------------------

rm -rf compile-result.txt

javac -cp $CPATH ./testing-folder/*.java 2> compile-result.txt

X=$?

if [[ $X -eq 0 ]]
then
    echo 'Compiled successfully'
else
    echo 'Errors were found while compiling'
    echo 'Error code is: ' $X
    exit
fi

#--------------------------------------------------
# PART 4: RUNNING STUDENT SUBMISSION
#--------------------------------------------------

cd testing-folder

rm -rf compile-result.txt

# java -cp $CPATH org.junit.runner.JUnitCore ./testing-folder/TestListExamples > run-result.txt
java -cp ".;lib/junit-4.13.2.jar;lib/hamcrest-core-1.3.jar" org.junit.runner.JUnitCore TestListExamples > run-result.txt

cp run-result.txt ..

cd ..

X=$?

if [[ $X -eq 0 ]]
then
    echo 'Ran successfully'
else
    echo 'Errors were found while running'
    echo 'Error code is: ' $X
    exit
fi

#--------------------------------------------------
# PART 5: GRADING STUDENT SUBMISSION
#--------------------------------------------------

rm -rf failures.txt 

grep -c -i "FAILURES" run-result.txt > failures.txt


FAILS=`grep -c -i "FAILURES" run-result.txt`

echo "-----"

if [[ $FAILS -eq 0 ]]
then
    echo "You passed!"
else
    echo "We found an error, so you fail!"
fi
```

Now, we will go more in depth on each section of the grading script, starting with part 1.


## Part 1: Cloning and Checking for Correct Files

```
# CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar' # uncomment this line and comment the line below if on Mac
CPATH=".;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar"

#--------------------------------------------------
# PART 1: CLONING AND CHECKING FOR CORRECT FILES
#--------------------------------------------------

rm -rf student-submission
git clone $1 student-submission
echo 'Finished cloning'

cd student-submission

if [[ -f ListExamples.java ]]
then
    echo 'Correct file found'
else
    echo 'Need ListExamples.java'
    exit
fi
```
This part of the script is fairly simple. When running `grade.sh`, the student's github repository is passed in through the command line and is stored in `$1`. The script first clones this repo into a directory called `student-submission` and `cd`'s into it. It then checks to see if the correct file, in this case `ListExamples.java` is within `student-submission`. If `ListExamples.java` is not found, the program exits. If it is found, we move on to part 2.

## Part 2: Setting up Files for Testing

```
#--------------------------------------------------
# PART 2: SETTING UP FILES FOR TESTING
#--------------------------------------------------

cp ListExamples.java ..
cd ..


rm -rf testing-folder
mkdir testing-folder

cp TestListExamples.java testing-folder
cp ListExamples.java testing-folder
cp -r lib testing-folder

echo 'Files ready for testing'
```
All we are doing in this part of the script is copying/moving around files for organizational purposes. First, we copy `ListExamples.java` into the parent directory, then `cd` into the parent directory. Then, we create the directory `testing-folder` to store all the files we need to compile/run the program. We then copy `TestListExamples.java`, `ListExamples.java`, and the `/lib` directory into `testing-folder`. These are all the files we need in order to compile the program and run the JUnit tests in parts 3 and 4 respectively.

## Part 3: Compiling Student Submission

```
#--------------------------------------------------
# PART 3: COMPILING STUDENT SUBMISSION
#--------------------------------------------------

rm -rf compile-result.txt

javac -cp $CPATH ./testing-folder/*.java 2> compile-result.txt

X=$?

if [[ $X -eq 0 ]]
then
    echo 'Compiled successfully'
else
    echo 'Errors were found while compiling'
    echo 'Error code is: ' $X
    exit
fi
```

This part of the script is where we compile the student's submission. First, we redirect the output of running `javac` into `compile-result.txt`. We then store the exit status of running `javac` into a variable `X`. `X` is used within our if/else statement to check whether or not we were able to compile the student submission successfully. If `X` holds any value other than 0, we know something went wrong while compiling, so we tell the user that there was a problem and exit the script. If everything compiled successfully, we move on to part 4.


## Part 4: Running Student Submission

```
#--------------------------------------------------
# PART 4: RUNNING STUDENT SUBMISSION
#--------------------------------------------------

cd testing-folder

rm -rf compile-result.txt

# java -cp $CPATH org.junit.runner.JUnitCore ./testing-folder/TestListExamples > run-result.txt
java -cp ".;lib/junit-4.13.2.jar;lib/hamcrest-core-1.3.jar" org.junit.runner.JUnitCore TestListExamples > run-result.txt

cp run-result.txt ..

cd ..

X=$?

if [[ $X -eq 0 ]]
then
    echo 'Ran successfully'
else
    echo 'Errors were found while running'
    echo 'Error code is: ' $X
    exit
fi
```

Now that everything is compiled, we can move on to the next part of the script, which is running the code/JUnit tests. We first `cd` into `testing-folder`, as it contains all the files we need. We then redirect the output of running `java` into `run-result.txt` and copy `run-result.txt` into the parent directory. Just like in part 3, we also store the exit code of `java` into `X`. Much like earlier, if `X` contains a value other than 0, we know that an error was found while running the code, so we tell the user and exit. If the program was able to run successfully, we move on to part 5.

## Part 5: Grading Student Submission

```
#--------------------------------------------------
# PART 5: GRADING STUDENT SUBMISSION
#--------------------------------------------------

rm -rf failures.txt 

grep -c -i "FAILURES" run-result.txt > failures.txt


FAILS=`grep -c -i "FAILURES" run-result.txt`

echo "-----"

if [[ $FAILS -eq 0 ]]
then
    echo "You passed!"
else
    echo "We found an error, so you fail!"
fi
```

Now, in the final part of the script, we assign the student's submission a grade based on the results of the JUnit tests. We first use `grep` in combination with the `-i` and `-c` options to find any and all instances of the word "FAILURES" within `run-result.txt` and store it in a variable called `FAILS`. `FAILS` will contain the number of times the word "Failures" appears in `run-result.txt` regardless of capitalization. Our grader is pretty brutal (but not by design!), and uses a pass/fail system. If any error is found, it is an automatic fail. If the program runs correctly, the student passes.

Obviously, there is a lot of room for improvement within this part of the grading script. One idea we had was to use `grep` to try and isolate the following lines from `run-result.txt`. 

[!Image](https://i.imgur.com/6aOv0Jz.png)

We know that these lines only show up if one or more JUnit tests fails, so our idea was to somehow store the number of failures and the number of tests into two separate variables. We could then give a percentage grade with the following calculation:

**( Total # of Tests - # of Failed Tests) / ( Total # of Tests)

This would definitely be a more fair grading scheme than our current pass/fail system, and would actually make it so implementing more tests within `TestListExamples.java` would be beneficial to the student instead of detrimental. Unfortunately, we were not able to come up with a working solution in time, but after looking into this on my own time it looks like command such as `awk` or `sed` could be used to achieve this goal.
