# Product of Array Except Self

## Problem

Given an array ```nums``` of n integers where n > 1,  return an array ```output``` such that ```output[i]``` is equal to the product of all the elements of ```nums``` except ```nums[i]```.

**Example:**

	Input:  [1,2,3,4]
	Output: [24,12,8,6]
**Note:** Please solve it **without division** and in O(n).

**Follow up:**
Could you solve it with constant space complexity? (The output array **does not** count as extra space for the purpose of space complexity analysis.)


## Solution

The goal is to multiply all elements of an array aside from the element at each index. The restriction is that we cannot use division and our algorithm has to be in linear time. 

The trivial solution is to iterate the array for each array element and multiply each element, which will calculate all products in O(n^2) time, but in constant space.

In order to fully explain the constant space complexity and linear time complexity solution, we can take 3 solutions:

1. Storing the products starting from the left and then the right in separate arrays. By allocating an array to keep track of products from the left to right direction, and then an additional array to keep track of products from the right to left direction, we can multiply the values at each index to achieve the product of input array except self. 

	![alt text](https://leetcode.com/problems/product-of-array-except-self/Figures/238/products.png "Sample Array Example")

	Since each array starts its products from 1, it will calculate everything before the current index of the array, so multiplying the left side product with its right side will result in the product of every element in the array except the current element.

	This leaves us with O(3n) = O(n) linear time solution as we have to iterate the array 2 times to compute the left and right product, and then a final time to calculate the final product array. This also uses O(3n) = O(n) space complexity since we are storing the left, right, and final product arrays.

2. The next solution involves calculating and altering the products as we go, without saving each element in the left or right array. This allows us to use constant space complexity, as we use the same logic as in solution 1, and multiply up to the current index starting from the left and then the right. This allows us to traverse the input array twice, and saving our products onto our final result array (instead of the left and right arrays). This solution allows us to achieve O(2n) = O(n) linear time, as well as O(1) constant space, since the output array is neglected in space complexity calculation. This can be considered the final solution.

3. The last solution is a variant of solution 2, as this once just condenses the 2 loops of solution 2 into a single loop, which may look like a singular loop O(n) solution, but it's actually doing the same number of operations as solution 2. This is an alternative solution which trades off readability for condensed code. Depending on the interviewer's preference, this may be the optimal solution. So in conclusion: for code readability choose solution 2, for condensed code choose solution 3, since both solutions are computationally-equivalent.

## Code

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        // left and right sub array multiplication method
        int n = nums.size();
        vector<int> left(n);
        vector<int> right(n);
        left[0] = 1;
        right[n-1] = 1;
        
        for (int i = 1; i < n; i++) {
            left[i] = left[i-1]*nums[i-1];
        }
        
        for (int i = n-2; i >= 0; i--) {
            right[i] = right[i+1]*nums[i+1];
        }
        
        for (int i = 0; i < n; i++) {
            nums[i] = left[i]*right[i];
        }
        
        return nums;
    }
};
```

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        // left and right integer multiplication (separate)
        int left = 1, right = 1, n = nums.size();
        vector<int> result(n,1);
        
        for (int i = 0; i < n; i++) {
            result[i] *= left;
            left *= nums[i];
        }
        
        for (int i = n-1; i >=0; i--) {
            result[i] *= right;
            right *= nums[i];
        }
        
        return result;
    }
};
```

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        // left and right integer multiplication (together)
        int left = 1, right = 1, n = nums.size();
        vector<int> result(n,1);
        
        for (int i = 0; i < n; i++) {
            result[i] *= left;
            left *= nums[i];
            result[n-1-i] *= right;
            right *= nums[n-1-i];
        }
        
        return result;
    }
};
```