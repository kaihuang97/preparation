# Missing Number in Sorted Array

## Problem

Given an array of consecutive positive integers, find the one that is missing from the array.

**Example 1:**

	Input: [1,2,3,4,6,7]
	Output: 5
**Example 2:**

	Input: [10,12,13,14,15]
	Output: 11

## Solution

The goal is to find the missing number within a list of consecutive positive integers. In other words, every integer in the array will be consecutive except for a "hole" in which the missing number will take up.

The trivial solution is to search through the entire array, keeping a counter for the predicted next number (incrementing our counter once every interation), which will take linear time complexity. However since our input array is sorted, we can utilize a divide-and-conquer approach using binary search, will will take out time complexity to logarithmic = O(log(n)).

To do this, we can utilize binary search to look for the "hole" in the array. If one half of the array contains the hole, we can drop the next half. We can then repeat this rule until we find our hole = missing number, which defines our logarithmic time compexity. In order to find our hole, we can begin by looking at the difference between the first and midpoint indices of the array and its values. In the case that the difference between indices and the difference between values are equal, we know there isn't a hole in the first half of the array and we can eliminate it for the next iteration. We are left with two final cases to end our algorithm: (start, mid) or (mid, end). To return the missing number, we increment or decrement one for the value at mid depending on left or right half, i.e. (start, mid) returns mid - 1, and (mid, end) returns mid + 1.

Therefore, the overall time complexity is O(log(n)) utilizing binary search, and the space compexity is constant O(1) since the variables we use to keep track of start, end, and mid indices is constant and not dependant on the input array.

## Code

```cpp
class Solution {
public:
	int find_missing (vector<int>& nums){
		int start = 0;
		int end = nums.size() - 1;
		int mid = (start + end)/2;

		while (start < end) {
			// difference between indexes vs. difference between values
			if ((nums[mid] - nums[start]) != (mid - start)) {
			    // there is a hole in the start half
			    if ((mid - start) == 1 && (nums[mid] - nums[start] > 1)) {
			    	// location of mid is after start, so take mid - 1
			        return (nums[mid] - 1);
			    }

			    end = mid;
			} else if ((nums[end] - nums[mid]) != (end - mid)) {
				// there is a hole in the second half
				if ((end - mid) == 1 && (nums[end] - nums[mid] > 1)) {
					// location of mid is before end, so take mid + 1
				    return (nums[mid] + 1);
				}

				start = mid;
			} else {
				// there is no hole
				return 0;
			}

			mid = (start + end)/2;
		}

		// there is no hole
		return 0;
	}
}
```