# Best Time to Buy and Sell Stock

## Problem

Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

**Example 1:**

	Input: [7,1,5,3,6,4]
	Output: 5
	Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
	             Not 7-1 = 6, as selling price needs to be larger than buying price.
**Example 2:**

	Input: [7,6,4,3,1]
	Output: 0
	Explanation: In this case, no transaction is done, i.e. max profit = 0.



## Solution

This is a classic example of a greedy algorithm, as we are looking for the local optimal choice, so when we have scanned through the entire array, we find the global optimal choice by comparisons between many local choices.

Our goal is to find the maximum profit, by buying at the locally cheapest and selling at the most locally expensive, linearly through time.
Our restriction is that we can only buy first and sell second to induce the maximum profit.

Scanning the array from left to right, we first find the cheapest stock so far, by keeping track of the minimum of the array. 
We also calculate the current profit (current price - minimum price so far), and compare it against our past profit to maximize our overall profit.


Runtime complexity is linear O(n) since we only look through the array once.

Space complexity is constant O(1) since we use constant number of variables for comparison.


## Code

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int min_price = INT_MAX;
        int cur_profit = 0;
        for (int i = 0; i < (int) prices.size(); i++) {
            min_price = min(min_price, prices[i]); // finding cheapest stock so far
            cur_profit = max(cur_profit, prices[i] - min_price); // keeping track of maximum selling profit so far
        }
        return cur_profit;
    }
};
```