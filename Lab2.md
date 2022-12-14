# Lab 02 Debugging and URL
## Introduction
Welcome to week3! This week you are going to explore about debugging methods and some common used knowledge about url's and servers.
## Part 1: Search Engines
In this first part you are going to create a simple search engine by implementing a web server that tracks a list of strings. You will be implementing a path for adding a new string to the list, a path for querying the list of strings and returning a list of all strings that have a given substring. 

```
import java.io.IOException;
import java.net.URI;
import java.util.*;

class Search implements URLHandler {
    ArrayList<String> result = new ArrayList<>();

    public String handleRequest(URI url){
        if (url.getPath().equals("/")) {
            return result.toString();
        } else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    result.add(parameters[1]);
                    return result.toString();
                }
            }
            else if (url.getPath().contains("/search")) {
                ArrayList<String> output = new ArrayList<>();
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    for (String i: result) {
                        if (i.toUpperCase().contains(parameters[1].toUpperCase())) {
                            output.add(i);
                        }
                    }
                    return output.toString();
                }
            }
            return "404 NOT Found!";
        }
    }
}
class SearchEngine {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Search());
    }
}
```
Above is an example of how to implement the method. 

After this, you will need to use:
```
javac Server.java SearchEngine.java 
java NumberServer 4000
```
to start your server!

The following are some screen shots of using the search engine method:
![Image](lab2(4).png)
```
In this screenshot we can exmaine that our path is "/add" so the if statement under the first else statement is going to run. Then the next line will split the query by "=" and check if it contains "s" which is true in this case. Thus our result array list will take the element next right after "=" and store it as a string.
```
![Image](lab2(5).png)
```
In this screenshot we can exmaine that our path
is "/add" so the if statement under the first else statement is going to run. Then the next line will split the query by "=" and check if it contains "s" which is true in this case. Thus our result array list the element right after "=" into the list which in this case is the "pineapple". 
```
![Image](lab2(3).png)
```
In this screenshot we can exmaine that our path
is "/search" so the else if statement under the first else statement is going to run. Then the next line will split the query by "=" and check if it contains "s" which is true in this case. Then it checks our reuslt array list which already has "apple" and "pineapple" in it. Then it runs into a for loop checking if the elements in result array list contain app which is all true in this case and thus it just return an array list of "apple" and "pineapple"
```

Here are some general guidance ideas:

a. You may want to first create an empty array list to store the information that you want.

b. Then in the method body you want to first check if the path equals "/" and in such case you want to return your array since there's no additional commands. 

c. Else you want to then print out the path and then check if the command is "add" in the path and if so, you want to get its query and check what is the first element after "=". If it is a character s, then you want to add the next element in the query into your storage list and return the information in the storage list as a string.

d. Else if, if the path tells us that the command is "search", then you want to create a new array list and then split the query by "=" and get its first element. If the first element is a letter s then for each strings in the storage list you are going to check if it contains the second element in the query and if it does, then you add it to your new array list. After the loop, you are going to return the information in the array list as a string.

e. In all other cases, you may want to print out "404 Not Found" to warn the users. 




## Part 2 Debugging
Debugging is an important process of writing the codes. In the second part of the lab, you are going to practice your debugging skills! 

There are many different files but in this tutorial I am only going to demonstrate clearing 2 bugs, one from ```ArrayExamples``` and one from  ```LinkedListExample```.

We are going to first examine ```ArrayExamples.java```; Method ```reversed``` clearly has a problem. Here is an exmaple:

**Failure inducing input**:
![Image](lab2(6).png)

**Symptom:**
![Image](lab2(7).png)
```
Note that the output right here tells us that we have ran 4 tests and one of them failed! We can also see that the output is telling us what is causing the error so we can fix them accordingly! 
```
**Original Code**
```
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
```
Issue: It changes the element to be the one in its reversed index, however, it doesn't change the element in its reversed index to the element we are changing. 

**The Bug (Fixed Code):**
```
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < (arr.length/2); i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i -1] = temp;
    }
  }
```

**Reasoning:**
It changes the element to be the one in its reversed index, however, it doesn't change the element in its reversed index to the element we are changing. Thus we need to let the for loop only go through half of the length of the array(so it doesn't reverse and then reverse) so every time we can create a temp element storing the element we want to reverse and then change that element and put the temp element into the index where the changes happened


The second one which we are going to examine would be the ```LinkedListExample.java```; The method ```append``` is clearly wrong. 

**Failure inducing input**:
![Image](lab2(9).png)

**Symptom:**
![Image](lab2(8).png)
```
Note that the output right here tells us that we have ran 1 tests and one of them failed! We can also see that the output is telling us what is causing the error so we can fix them accordingly! 
```
**Original Code**
```
    public void append(int value) {
        if(this.root == null) {
            this.root = new Node(value, null);
            return;
        }
        // If it's just one element, add if after that one
        Node n = this.root;
        if(n.next == null) {
            n.next = new Node(value, null);
            return;
        }
        // Otherwise, loop until the end and add at the end with a null
        while(n.next != null) {
            n = n.next;
            n.next = new Node(value, null);
        }
    }
```
Issue: The while loop used to have 
```
n.next = new Node(value, null);
```
inside the loop. This would cause the loop to run into an infinite loop since there would be an infinite number of nulls so n.next will never be null thus the loop will never stop becaue the condition won't met. This causes the heap to crash. 

**The Bug (Fixed Code):**
```
    /**
     * Adds the value to the _end_ of the list
     * @param value
     */
    public void append(int value) {
        if(this.root == null) {
            this.root = new Node(value, null);
            return;
        }
        // If it's just one element, add if after that one
        Node n = this.root;
        if(n.next == null) {
            n.next = new Node(value, null);
            return;
        }
        // Otherwise, loop until the end and add at the end with a null
        while(n.next != null) {
            n = n.next;
        }
        n.next = new Node(value, null);
    }
```
**Reasoning:**
The while loop used to have 
```
n.next = new Node(value, null);
```
inside the loop. This would cause the loop to run into an infinite loop since there would be an infinite number of nulls so n.next will never be null thus the loop will never stop becaue the condition won't met. This causes the heap to crash. So to fix it, we have to move  
```
n.next = new Node(value, null);
```
this line out of the while loop so it would actually stop when there's out of elements in the linked list and then we can do the assigning. 


## Conclusion
Congrats! You have completed the lab for this week! For this lab, you learned the how to start a server and how to create basic search functions to it. You can use what you have learned to explore about search methods. You also went through the process of debugging this week. I wish that you now have a basic understanding on how/what to debug your or other's code. This is an very important skill for programming, so keep building on!