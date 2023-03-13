# CSE 15L Week 9 Lab Report: Simple Grading Script using Bash

*Ian Venzon - Thursday 12:00 PM - B270*

## Gradescope at Home

For this lab report, we will be covering `grade.sh`, a simple bash script that takes in a student submission for `ListExamples.java`, runs some tests to check for possible compile/runtime/output errors, then gives an appropriate grade based on the observed behavior.

Here is the entirety of `grade.sh`. At the moment it is configured for a Windows machine, but it can be converted for Mac/Linux very easily.

```
# CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar' # uncomment this line and comment the line below if on Mac
CPATH=".;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar"

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

cp ListExamples.java ..
cd ..


rm -rf testing-folder
mkdir testing-folder

cp TestListExamples.java testing-folder
cp ListExamples.java testing-folder
cp -r lib testing-folder

echo 'Files ready for testing'

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


cd testing-folder

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
