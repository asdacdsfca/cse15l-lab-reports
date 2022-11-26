# Lab 05 Grading Script
## Introduction
Welcome to week9! This week you are going to explore about grading script! Have you ever had a CS class that uses autograder to give feed back about your submission (programming assgiment) and wondering how does it work? In this report, we are going to focus on leanring about some basic idea about it and get some hands on pratice!

## Part 1: Constructing Your Grading Script
In this part we are going to build our grading script that can give some helpful feedback about students' submissions and give it a grade based on the number of tests passed.

Here is an example (Notice that I made many comments in the code block about the reasoning behind this script. Please Check them out!):
```
#Some of the Idea is Referenced from https://github.com/vnikonov63/list-examples-grader/blob/main/grade.sh

# Create your grading script here
 
# set -e

#Git clone the student submission
DirNAME="./student-submission/" 
rm -rf student-submission
git clone $1 student-submission

cd student-submission

#Setting up the initial values
echo -e "\n"
Score=0 #Current Score
MaxScore=100 #Max score can get
EachSucess=10 #Number of points per question
#Give every file we are going to use a refernce
InputFile="ListExamples.java"
TestFile="TestListExamples.java"
file="ListExamples"
#We use .. to go back to the lib folder since we were in student-submission
CPATH=".:../lib/hamcrest-core-1.3.jar:../lib/junit-4.13.2.jar"
total=1

# Check if the file exists
if [[ -e $InputFile ]]
then
    #if exists then add 10 points and report the status
   echo -e [Found] $InputFile [+10 points]
   Score=$(($Score+$EachSucess))
else
    #if not exist then print the current score, report the status and exit
   echo -e "File Does not Exist." [Exception]
   echo "Total points: [$Score]"
   exit
fi
cp ../TestListExamples.java ./
javac -cp $CPATH *.java 2> Compile-err.txt >stdOutput.txt 2>stdError.txt

#Check if ListExamples.java compilies
javac ListExamples.java
if [[ $? == 0 ]]
then
    #if it compilies then add 10 points, report the status and run JUnit test
   echo [Compile Success] $InputFile [+10 points]
   Score=$(($Score+$EachSucess))
   javac -cp .:../lib/hamcrest-core-1.3.jar:../lib/junit-4.13.2.jar *.java
   java -cp .:../lib/hamcrest-core-1.3.jar:../lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples > error.txt
else
    #if it doesn't compile then report the status, print the current score and exit 
   echo [Fail to Compile] $InputFile [Exception]
   echo "Total Points: [$Score]"
   exit
fi

#Save the last line of JUnit to a txt file
grep -A100000  Failures: error.txt > calculation.txt
#Remove the unnessary part so we can calculate our score in later steps
sed -e 's/^.*, //' calculation.txt > calculation2.txt
#Remove the unnessary part so we can calculate our score in later steps
sed -e 's/^.*: //' calculation2.txt > calculation3.txt

#Print out the results and information about how we grade it
echo -e "\nResults:\n[+10 points for every correct test]"
#Print out the error message to help students make revisions
grep -A100000 Failures: error.txt

#Calculate the final Score 
echo -e "Total Points:"
awk '{sum= sum+$1} END { print 100-sum*10}' calculation3.txt
```
## Part 2: Running Grading Script Using Server
In this part we are going to explore how to run our grading script on students' submissions and do it using server.

### A. a submission with some errors:
![Image](lab05(1).png)
Explanation: the result shows that the file is found, it sucessful compiled and after running 8 tests it passed 4 of them so the final grade would then be 10*4(# of sucessful tests) + 20(points for compile and file existence).

### B. a submission with no errors:
![Image](lab05(2).png)
Explanation: the result shows that the file is found, it sucessful compiled and after running 8 tests it passed all of them so the final grade would then be 10*8(# of sucessful tests) + 20(points for compile and file existence).

### C. a submission with compile errors:
![Image](lab05(3).png)
Explanation: the result shows that the file is found, but it fail to compile so the final grade would then be 10*0(# of sucessful tests) + 10(points for file existence).

## Trace:
we are going to trace example C, the one with compile errors.
```
#Git clone the student submission
DirNAME="./student-submission/" 
rm -rf student-submission
git clone $1 student-submission

cd student-submission

#Setting up the initial values
echo -e "\n"
Score=0 #Current Score
MaxScore=100 #Max score can get
EachSucess=10 #Number of points per question
#Give every file we are going to use a refernce
InputFile="ListExamples.java"
TestFile="TestListExamples.java"
file="ListExamples"
#We use .. to go back to the lib folder since we were in student-submission
CPATH=".:../lib/hamcrest-core-1.3.jar:../lib/junit-4.13.2.jar"
total=1
```
For this part of the code, the standard output and and standard error would both be empty since its just about some initialization(see comments for details). Since these lines don't have any errors when running, the return code would just be 0.

```
# Check if the file exists
if [[ -e $InputFile ]]
then
    #if exists then add 10 points and report the status
   echo -e [Found] $InputFile [+10 points]
   Score=$(($Score+$EachSucess))
else
    #if not exist then print the current score, report the status and exit
   echo -e "File Does not Exist." [Exception]
   echo "Total points: [$Score]"
   exit
fi
cp ../TestListExamples.java ./
javac -cp $CPATH *.java 2> Compile-err.txt >stdOutput.txt 2>stdError.txt
```
For this part of the code, since the file is found, so the if statement would be true and echo the status (see comments for details). Thus, the else part wouldn't run (as well as the lines that only run when else is true). The standard output of the echo command would be "[Found] ListExamples.java" and "[+10 points]". The standard error would be empty. The return code would be 0 since these lines ran without any errors.

```
#Check if ListExamples.java compilies
javac ListExamples.java
if [[ $? == 0 ]]
then
    #if it complies then add 10 points, report the status and run JUnit test
   echo [Compile Success] $InputFile [+10 points]
   Score=$(($Score+$EachSucess))
   javac -cp .:../lib/hamcrest-core-1.3.jar:../lib/junit-4.13.2.jar *.java
   java -cp .:../lib/hamcrest-core-1.3.jar:../lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples > error.txt
else
    #if it doesn't compile then report the status, print the current score and exit 
   echo [Fail to Compile] $InputFile [Exception]
   echo "Total Points: [$Score]"
   exit
fi
```
For this part of the code, the student submission fail to compile, so the ```if``` condition wouldn't run(as well as the lines that only run when its true), instead, the ```else``` condition would trigger and echo the status(see in-line comments for details) and then exit the grading script. The standard output of the echo command would be "[Fail to Compile] ListExamples.java [Exception]" and "Total Points: [10]". The standard error would be something like this:
```
ListExamples.java:15: error: ';' expected
        result.add(0, s)
                    ^
1 error
```
The return code would be non-zero since there were errors when running.

```
#Save the last line of JUnit to a txt file
grep -A100000  Failures: error.txt > calculation.txt
#Remove the unnessary part so we can calculate our score in later steps
sed -e 's/^.*, //' calculation.txt > calculation2.txt
#Remove the unnessary part so we can calculate our score in later steps
sed -e 's/^.*: //' calculation2.txt > calculation3.txt

#Print out the results and information about how we grade it
echo -e "\nResults:\n[+10 points for every correct test]"
#Print out the error message to help students make revisions
grep -A100000 Failures: error.txt

#Calculate the final Score 
echo -e "Total Points:"
awk '{sum= sum+$1} END { print 100-sum*10}' calculation3.txt
```
This part of the code wouldn't run, because I designed my grading script to terminate when there's compiling erros.

## Conclusion
Congrats! You have completed the lab for this week! In this lab, you have learned and experienced creating grading script using bash! I hope you find these skills useful and I encourage you to explore more about them!

