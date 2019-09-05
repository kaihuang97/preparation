# Contains Duplicate

## Problem

Given an array of integers, find if the array contains any duplicates.

Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

**Example 1:**

	Input: [1,2,3,1]
	Output: true
**Example 2:**

	Input: [1,2,3,4]
	Output: false
**Example 3:**

	Input: [1,1,1,3,3,4,3,2,4,2]
	Output: true


## Solution

The goal is to determine if an input array contains duplicate elements. 

This is a simple problem to showcase tradeoff between runtime and space complexity.

Sorting the input array would order the array in such a way that duplicates would be next to each other. 
Therefore, while scanning the array from left to right, if there exists two subsequent identical numbers, then there exists a duplicate.
This yields a runtime complexity of O(nlog(n)) due to sorting, and a space complexity of O(1) since we don't need to store numbers to compare.

A faster approach would be to store each number in the input array into a hash set (unordered_set in C++).
So scanning the array from left to right, we would insert each number into the set if it didn't already exist. 
If the number already exists, then there exists a duplicate.
This yields a runtime complexity of O(n) due to the creation of a hash set while only scanning the array once, and a space complexity of O(n) since we use a hash set to store seen numbers.

## Code

```cpp
class Solution {
public:
    // using hash set to store seen numbers
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> hash;
        for (int i = 0; i < (int) nums.size(); i++) {
            if (hash.find(nums[i]) != hash.end()) {
                return true;
            }
            hash.insert(nums[i]);            
        }
        return false;
    }
    
    // sorting, and then duplicates will be next to each other
    bool containsDuplicate(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        for (int i = 0; i < (int) nums.size()-1; i++) {
            if (nums[i] == nums[i+1]) return true;
        }
        return false;
    }
};
```