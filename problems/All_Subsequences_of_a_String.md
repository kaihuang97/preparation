# All Subsequences of a String

## Problem

Given a string *str*, the task is to print all the sub-sequences of *str*.
A subsequence is a sequence that can be derived from another sequence by deleting some or no elements without changing the order of the remaining elements.

## Solution

![alt text](./images/Subsequences_Tree.png "Recursive Tree")

## Code

```java
public class Solution { 
  
    public static void printSubSeq(String sub, String ans) {
        if (sub.length() == 0) { 
            System.out.print("" + ans + " "); 
            return; 
        } 
  		// grab first character
        char ch = sub.charAt(0); 
  
        // create substring from remaining characters
        String ros = sub.substring(1); 
  		
  		// pass substring - character
        printSubSeq(ros, ans); 
  	
  		// pass substring + character
        printSubSeq(ros, ans + ch); 
    } 
  
    public static void main(String[] args) 
    { 
        String str = "abc"; 
        printSubSeq(str, ""); 
    } 
} 
```