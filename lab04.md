# Lab 04 Vim
## Introduction
Welcome to week7! This week you are going to explore about vim! A way to access and make changes on files that are not available locally! In this report, we are going to focus on the leanring about some basic idea about it!

## Part 1: Make Changes Using Vim
In the first part we are going to explore how to use ```vim``` to make some changes on our files! We will be making changes on ```DocSearchServer.java``` from ```week6-skill-demo1```, specifically, we will change the main method so rather than hardcoding the search on the ```./technical``` directory, it uses the second command-line argument for the path to search. 

Set Up: Start ```DocSearchServer.java``` using vim.
![Image](lab4(1).png)
if you have entered vim mode successfully then you should see something similar to this:
![Image](lab4(2).png)

Here is a summarized version of the keys that I pressed:
```/mai<Enter>/ca<Enter>/)<Enter>i<Enter>+args[1] <Enter><ESC>:wq```

The followings are a break down of all the steps!: 

1. ```/mai<Enter>```
![Image](lab4(3).png)
we use this command to find the place that contains ```mai``` these three characters which the only place that has it in our file is the ```main``` method. 

You should see something like this if you have done it correctly:
![Image](lab4(4).png)

2. ```/ca<Enter>```

Similar to step 1, we use this command to find the place that contains ```cal``` these three characters which would locate ```./technical``` for us.
![Image](lab4(5).png)

If you have done it correctly then you should see something like this:
![Image](lab4(6).png)

3. ```/)<Enter>```

Similar to the previous two teps, we use this command to find the place that contains ```)``` these three characters which would locate ```)``` for us. Since we were at ```./technical``` this would locate us at the first closing bracket!
![Image](lab4(7).png)

If you have done it correctly then you should see something like this:
![Image](lab4(8).png)

4. ```i<Enter>```

Press i to enter insert mode so you can start editing the code!
![Image](lab4(9).png)

If you have done it correctly then you should see something like this:
![Image](lab4(10).png)

5. ```+args[1] <Enter>```

Last step takes us to insert mode so now we type our changes ```args[1]``` so main takes a command line argument. 
![Image](lab4(11).png)

6. ```<ESC>```

We use ```ESC``, the escape key to exit insert mode.


7. ```:wq```

We use ```:wq``` to save the changes we made on our file!
![Image](lab4(12).png)

If you have done it correctly then you should see something like this:
![Image](lab4(13).png)

And now we have done our changes! We have sucessfully changed the ```main``` method in ```DocSearchServer.java``` to take a command-line argument!

## Part 2: Chaing Files on Remote Machines Using Scp and Vim
In this second part, we are going to test the difference (mainly on time) between using vim and scp for making changes on files that are on remote machines.

Here are some screen shots of how to do it via scp:

1. Making changes locally
![Image](lab4(14).png)

2. Scp the file to remote machine
![Image](lab4(15).png)

3. Logging to our remote machine
![Image](lab4(16).png)

4. Run the test bash script
![Image](lab4(17).png)


The Vim method is easier:

Since we assume that we are already in our remote machine, all we have to do is ![Image](lab4(18).png) and then start making changes that we mentioed in part1!


## Report:
It took me around 3 and half minutes using SCP. The only difficulty I encoutered was that I forgot how to do SCP.

Regard to VIM method, it took me around 2 and half minutes. I did not encounter any difficulties. 



```Which of these two styles would you prefer using if you had to work on a program that you were running remotely, and why?```

I would definately prefer using vim. It requires less work and it is faster! Consider that the scp requires you to make changes locally first (which means you have to pull it) and then upload the edited version, it wastes a lot of time in this download/upload process. AND consider the case when the file is huge you probably don't want to download it to your computer (cause the space issue and of course, the time issue). 


```What about the project or task might factor into your decision one way or another?```

I would say most of the time I'd prefer using vim because the time and space issue I mentioned in the previous question. However, if I want to save a copy of the file or the changes locally then I might prefer SCP over VIM. Because in this case it would actually be more convinent (since we have to download the file from remote machine in either way and the SCP method makes it easier if you want to keep and original version and a changed version locally). 

## Conclusion
Congrats! You have completed the lab for this week! In this lab, you have learned and experienced vim and you have also made a comparison between SCP and VIM for making changes on remote machines! I hope you find these skills useful and I encourage you to explore more about them!