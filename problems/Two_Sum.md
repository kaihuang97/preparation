# Two Sum

## Problem

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

**Example:**

	Given nums = [2, 7, 11, 15], target = 9,

	Because nums[0] + nums[1] = 2 + 7 = 9,
	return [0, 1].

## Solution

The goal is to return the indices of 2 numbers from an input array such that they add up to a certain target sum.
The restriction is that the same element can't be used twice and that each input has only 1 exact solution.

Build hash map of (number, index).
For each number, if its result of (target - current number) is found in the hash map, then return hashed index of (target - current number) and the current number's index. 
If the result is not found in the hash map, then add the current number and its index as a pair. 

Runtime complexity will be O(n) to build hash map and iterating input vector.

Space complexity will be O(n) since hash map will never exceed input vector length.


## Code

```cpp
class Solution {
public:
    std::vector<int> twoSum(std::vector<int>& nums, int target) {
    	// <number, index>
        std::unordered_map<int, int> hash;
        for (int i = 0; i < nums.size(); i++) {
        	// find (target - nums[i]) in hash map
            if (hash.find(target - nums[i]) != hash.end()) {
                return {hash[target - nums[i]], i};
            }
            hash[nums[i]] = i;
        }
        return {};
    }
};
```