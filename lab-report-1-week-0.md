# Lab 01 Remote Access and the FileSystem

## Introduction
Welcome to CSE 15L! In this lab you are going to explore the remote machines and getting a basic understanding about how to use them! 
## 1. Installing VS Code

If you haven't download visual Studio Code, download it [here](https://code.visualstudio.com/)!

![Image](Lab01(1).png)

## 2. Remotely Connecting

If you are on windows: install a program called OpenSSH, which is a program that can connect your computer to other computers that have this kind of account. Download it [here](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse?tabs=gui)

a. For the first step, open a terminal in VSCode (Ctrl or Command + `). Type (ssh cs15lfa22xx@ieng6.ucsd.edu) *note replace xx with your unique two letters

b. If this is your first time logging in, then you would probably see a message asking for permission, in this case say yes. 

c. When you are logged in you should see something like this:
```
# On your client
⤇ ssh cs15lfa22zz@ieng6.ucsd.edu
The authenticity of host 'ieng6-202.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])? 
Password: 
```
![Image](Lab01(2).png)

If you see this then you are connected to a computer in the CSE basement!


## 3. Run Some Commands

a. Try to run some commands
```
cd ~
cd
ls -lat
ls -a
ls <directory> where <directory> is /home/linux/ieng6/cs15lfa22/cs15lfa22abc, where the abc is one of the other group members’ username
cp /home/linux/ieng6/cs15lfa22/public/hello.txt ~/
cat /home/linux/ieng6/cs15lfa22/public/hello.txt
```

This is an example! 
![Image](Lab01(3).png)


## 4. Moving Files over SSH with scp

a.  Now we are introduing you how to copy files from your local computer to remote machine! Just like storing/uploading files to cloud drive!

b. This process is called scp. Create a file on your computer called ```WhereAmI.java``` and put the following contents into it:
```
class WhereAmI {
  public static void main(String[] args) {
    System.out.println(System.getProperty("os.name"));
    System.out.println(System.getProperty("user.name"));
    System.out.println(System.getProperty("user.home"));
    System.out.println(System.getProperty("user.dir"));
  }
}
```
Compile and run the WhereAmI program using the commands below.
```
javac WhereAmI.java
java WhereAmI
```

c. In your terminal run this command:
```
scp WhereAmI.java cs15lfa22zz@ieng6.ucsd.edu:~/
```

d. Then, log into ieng6 with ssh again, and use ls. You should see the file there in your home directory! And run the following commands:
```
javac WhereAmI.java
java WhereAmI
```

Here are some screenshots which you would see the same thing if you did correctly!
![Image](Lab01(4).png)

![Image](Lab01(5).png)

## 5. SSH Keys

a. Typing your password in everytime could be annoying, now we are going to creat ssh keys to create less repetitive work. 

![Image](Lab01(6).png)

b. Then do the following steps:
```
# on client
$ ssh cs15lfa22zz@ieng6.ucsd.edu
<Enter Password>
```
![Image](Lab01(7).png)

then: 
![Image](Lab01(8).png)

And finally you would see this if you did correctly:
![Image](Lab01(9).png)

c. If you have done this then you don't have to enter your password everytime when doing ssh or scp. 

## 6. Making Remote Running Even More Plesant

a. Now based on what you have leanred through this lab, try to make a local edit to ```WhereAmI.java``` then copying it to the remote server and running it. 

b. Here is an example:

![Image](Lab01(10).png)

## Conclusion

Now you have learned how to use remote machine and have some knowledge about the applications of local and remote file transferring. You are now ready to explore more about those fields!

