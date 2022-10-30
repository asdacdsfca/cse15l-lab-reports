# Lab 03 Reasearching Commands
## Introduction
Welcome to week5! This week you are going to explore about command-line options! In this report, we are going to focus on the ```grep``` command!

## Part 1: ```-c``` option
In the first part we are going to examine the command-line option ```c``` for ```grep```!

Below we offer a general idea about how should we implement it in our example files and diretories from ```./technical ```.

***Example 1***
-
**Input**:
```
yingxizhao@asdfvbniop98 911report % ls |grep -c "world" chapter-12.txt
```
**Output**:
```
44
```
Note that in this example our working directory is ```911report```. The ```-c``` after grep indicates that this is a command line option to find all the number of lines (44) that mathces the given pattern (in this case "world") in the given file (in this case "chapter-12.txt"). 

***Example 2***
-
**Input**
```
yingxizhao@asdfvbniop98 biomed % ls |grep -c "is" 1468-6708-3-1.txt
```
**Output**:
```
82
```
Note that in this example is very similar to example 1 but here our working directory is ```biomed```. The ```-c``` after grep indicates that this is a command line option to find all the number of lines (82) that mathces the given pattern (in this case "is") in the given file (in this case "1468-6708-3-1.txt"). 

***Example 3***
-
**Input**
```
yingxizhao@asdfvbniop98 plos % ls |grep -c "developing" journal.pbio.0020001.txt
```
**Output**:
```
27
```
Note that in this example is very similar to example 1 and example 2 but here our working directory is ```plos```. The ```-c``` after grep indicates that this is a command line option to find all the number of lines (27) that mathces the given pattern (in this case "is") in the given file (in this case "journal.pbio.0020001.txt"). 

## Part 2: ```-n``` option
In the first part we are going to examine the command-line option ```n``` for ```grep```!

Below we offer a general idea about how should we implement it in our example files and diretories from ```./technical ```.

***Example 1***
-
**Input**:
```
yingxizhao@asdfvbniop98 911report % grep -n "cloudless" chapter-1.txt
```
**Output**:
```
6:    Tuesday, September 11, 2001, dawned temperate and nearly cloudless in the eastern United States. Millions of men and women readied themselves for work. Some made their way to the Twin Towers, the signature structures of the World Trade Center complex in New York City. Others went to Arlington, Virginia, to the Pentagon. Across the Potomac River, the United States Congress was back in session. At the other end of Pennsylvania Avenue, people began to line up for a White House tour. In Sarasota, Florida, President George W. Bush went for an early morning run.
```
Note that in this example our working directory is ```911report```. The ```-c``` after grep indicates that this is a command line option to find all the number of lines (44) that mathces the given pattern (in this case "world") in the given file (in this case "chapter-12.txt").  

***Example 2***
-
**Input**
```
yingxizhao@asdfvbniop98 biomed % grep -n "CHS" 1468-6708-3-1.txt
```
**Output**:
```
49:          The Cardiovascular Health Study (CHS) is a
366:          CHS participants were somewhat healthier than the
424:        CHS Cardiovascular Health Study
```
Note that in this example is very similar to example 1. Our working directory is ```biomed```. The ```-n``` after grep indicates that this is a command line option to find (in this case, "CHS") and display the line number (In this case, line 49, 366, 424) of file with the matched file and its content (the long tests after ":"). 

***Example 3***
-
**Input**
```
yingxizhao@asdfvbniop98 plos % grep -n "clear inequalities" journal.pbio.0020001.txt
```
**Output**:
```
7:        the clear inequalities in science between developing and developed countries and to the
```
Note that in this example is very similar to example 1 and example 2 but here our working directory is ```plos```. The ```-n``` after grep indicates that this is a command line option to find (in this case, "clear inequalities") and display the line number (In this case, line 7) of file with the matched file and its content (the long tests after ":").

## Part 3: ```-O``` option
In the first part we are going to examine the command-line option ```O``` for ```grep```!

Below we offer a general idea about how should we implement it in our example files and diretories from ```./technical ```.

***Example 1***
-
**Input**:
```
yingxizhao@asdfvbniop98 911report % grep -o "cloudless" chapter-1.txt
```
**Output**:
```
cloudless
```
Note that in this example has very similar input as example 1 part2 but very different output! Our working directory is ```911report```. The ```-o``` after grep indicates that this is a command line option to find and display only the matching string (In this case, "cloudless") in the file here. 

***Example 2***
-
**Input**
```
yingxizhao@asdfvbniop98 biomed %  grep -o "CHS" 1468-6708-3-1.txt
```
**Output**:
```
CHS
CHS
CHS
```
Note that in this example has very similar input as example 2 part2 but very different output! Our working directory is ```biomed```. The ```-o``` after grep indicates that this is a command line option to find and display only the matching string (In this case, "CHS") in the file here. 

***Example 3***
-
**Input**
```
yingxizhao@asdfvbniop98 plos % grep -o "clear inequalities" journal.pbio.0020001.txt
```
**Output**:
```
clear inequalities
```
Note that in this example has very similar input as example 3 part2 but very different output! Our working directory is ```plos```. The ```-o``` after grep indicates that this is a command line option to find and display only the matching string (In this case, "clear inequalities") in the file here.

## Conclusion
Congrats! You have completed the lab for this week! In this lab, you have learned and experienced some cool and useful command-line options! Now you can take this skill and explore the other ones! 