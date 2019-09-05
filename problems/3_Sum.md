# 3 Sum

## Problem

Given an array *nums* of n integers, are there elements a, b, c in *nums* such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

**Note:**

The solution set must not contain duplicate triplets.

**Example:**

	Given array nums = [-1, 0, 1, 2, -1, -4],

	A solution set is:
	[
	  [-1, 0, 1],
	  [-1, -1, 2]
	]

## Solution

Our goal is to find 3 elements (a, b, c) which will sum to 0. The restriction is that our 3 elements have to be unique and non-repeating.

Sorting the input array will allow us to easily deal with negative and repeating numbers. 
Iterating through the input array, we check if the first number is positive, if it is then a 0 sum can't be acheived since the array is sorted.
In the same manner, we can also look for repeating numbers by looking at the previous index value, since the array is sorted.

We then attempt a 2 pointer sweep of the array, only looking at numbers to the right of our current number. 
We have two pointers, one located at the current index + 1, and another one at the end of the array.
If we find a match for valid triplet, we push it into our result vector, then we check for duplicate values near the two pointers, then increasing the left pointer and decreasing the right pointer, but also changing the pointers if none are found to move onto next possibilities.
In the case that our current summation of our select 3 numbers is greater than 0, we overshot so we decrement right pointer to decrease the summation value. In the case that our summation is less than 0, then we undershot so we increment the left pointer.

Runtime complexity is O(nlog(n)) for sorting with MergeSort, but our two-pointer approach is done for each number in the input array, so O(n\*n). Since n\*n > nlog(n), overall = O(n^2).

Space complexity is O(1) since we're allocating a constant amount of variables for use finding triplets and doing in-place comparisons. 

## Code

**C++:**
```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> result;
        if (nums.size() <= 2) return result;
        sort(nums.begin(), nums.end());

        for (int i = 0; i < nums.size() - 2; i++) {
            int a = nums[i];

            // first num can't be positive in sorted array
            // impossible to have subsequent numbers sum to 0
            if (a > 0) break;

            // repeating number
            if (i > 0 && a == nums[i - 1]) continue;

            // 2 pointer sweep of array
            int j = i+1;
            int k = nums.size()-1;
            while (j < k) {
                int b = nums[j];
                int c = nums[k];
                int value = a + b + c;

                if (value == 0) {
                    result.push_back(vector<int>({a, b, c}));
                    while (j < k && b == nums[j+1]) j++;	// skip same result
                    while (j < k && c == nums[k-1]) k--;	// skip same result
                    // still need to move pointers if no duplicates
                    j++;
                    k--;
                } else if (value > 0) {
                    k--; // overshot, decrement right pointer to decrease val b/c sorted array
                } else { 
                    j++; // undershot, increment left pointer to increase val b/c sorted array
                }
            }
        }
        return result;
    }
};
```

**Java:**
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new LinkedList<>();
        Arrays.sort(nums);
        
        for (int i = 0; i < nums.length-2; i++) {
            int a = nums[i];
            
            // first num can't be positive in sorted array
            // impossible to have subsequent numbers sum to 0
            if (a > 0) break;
            
            // repeating number
            if (i > 0 && a == nums[i-1]) continue;
            
            // 2 pointer sweep of array
            int j = i+1;
            int k = nums.length-1;
            while (j < k) {
                int b = nums[j];
                int c = nums[k];
                int val = a + b + c;
                
                if (val == 0) {
                    result.add(Arrays.asList(a, b, c));
                    while (j < k && b == nums[j+1]) j++;  // skip same result
                    while (j < k && c == nums[k-1]) k--;  // skip same result
                    // still need to move pointers if no duplicates
                    j++;
                    k--;
                } else if (val > 0) {
                    k--; // overshot, decrement right pointer to decrease val b/c sorted array
                } else {
                    j++; // undershot, increment left pointer to increase val b/c sorted array
                }
            }
        }
        return result;
    }
}
```