# Valid Parentheses

## Problem

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

* Open brackets must be closed by the same type of brackets.
* Open brackets must be closed in the correct order.
Note that an empty string is also considered valid.

**Example 1:**

	Input: "()"
	Output: true
**Example 2:**

	Input: "()[]{}"
	Output: true
**Example 3:**

	Input: "(]"
	Output: false
**Example 4:**

	Input: "([)]"
	Output: false
**Example 5:**

	Input: "{[]}"
	Output: true

## Solution

Use a stack in order to keep track of the last inserted item. If met with a closing brace of any kind, check if the last inserted item was an opening brace of the same kind, and if it isn't then invalid, and if the entire stack is traversed succesfully then the string contains valid parentheses.

## Code
```cpp
class Solution {
public:
    bool isValid(string s) {
        if (s.size() == 0) return true;
        
        stack<char> stack;
        
        int i = 0;
        while (i < (int) s.size()) {
            if (s[i] == '(' || s[i] == '{' || s[i] == '[') {
                stack.push(s[i]);
            } else if (s[i] == ')' && !stack.empty() && stack.top() == '(') {
                stack.pop();
            } else if (s[i] == '}' && !stack.empty() && stack.top() == '{') {
                stack.pop();
            } else if (s[i] == ']' && !stack.empty() && stack.top() == '[') {
                stack.pop();
            } else {
                return false;
            }
            
            i++;
        }
        return stack.empty() ? true : false;
    }
};
```