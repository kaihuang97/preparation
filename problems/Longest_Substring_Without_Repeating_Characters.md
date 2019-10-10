# Longest Substring Without Repeating Characters

## Problem

Given a string, find the length of the **longest substring** without repeating characters.

**Example 1:**

	Input: "abcabcbb"
	Output: 3 
	Explanation: The answer is "abc", with the length of 3. 
	Example 2:

	Input: "bbbbb"
	Output: 1
	Explanation: The answer is "b", with the length of 1.
	Example 3:

	Input: "pwwkew"
	Output: 3
	Explanation: The answer is "wke", with the length of 3. 
	             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.


## Solution

Brute-force solution is to check every single substring created from given string, which will start at a window length of 1 and grow the window length until reaching the length of the string, and then move over the window after reaching the end of the string, and starting over from window length 1. To check if a character is a duplicate or not, we can insert into hashset and attempt to find each letter in the set to verify its uniqueness.

Semi-optimized will attempt the same solution as brute-force, except it will now stop growing the window length when reaching a duplicate character. This is done using a two-pointer approach, growing the right pointer as long as there are no duplicates, and if there is then we take out the letter in the set at the left pointer if the next letter is a duplicate. This allows us to alter and slide our window, and once our right pointer reaches the end, then our algorithm terminates. In the worst-case, this algorithm checks each string index twice, making the run-time complexity = O(2n). 

Best optimized algorithm is a strange one. You have to use a dictionary ASCII bank to keep track of past indices of seen characters. When you see a character for the first time, you log its index. If you see that character again, you check if the past index of that character is greater than the overall start index (left pointer), then you skip to that index in order to find the immediate next valid substring with unique characters. This will truely be single pass since every iteration we increment the right pointer by 1, meaning O(n). 

## Code
```cpp
class Solution {
public:
    // dictionary vector O(n)
    int lengthOfLongestSubstring(string s) {
        vector<int> dict(256, -1);
        int maxLen = 0, start = -1;
        for (int i = 0; i != s.length(); i++) {
            if (dict[s[i]] > start)
                start = dict[s[i]];
            dict[s[i]] = i;
            maxLen = max(maxLen, i - start);
        }
        return maxLen;
    }
    
    // hashset O(2n)
    int lengthOfLongestSubstring(string s) {
        int left = 0;
        int right = 0;
        int res = 0;
        unordered_set<char> set;
        
        while (right < s.size()) {
            if (set.find(s[right]) == set.end()) {
                // new unique letter, expanding the window
                set.insert(s[right]);
                right++;
                res = max(res, right-left); // right - left = current length of window
            } else {
                // found duplicate, shifting the window
                set.erase(s[left]);
                left++;
            }
        }
        return res;
    }
};
```