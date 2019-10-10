# Group Anagrams

## Problem

Given an array of strings, group anagrams together.

**Example:**

	Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
	Output:
	[
	  ["ate","eat","tea"],
	  ["nat","tan"],
	  ["bat"]
	]
Note:

* All inputs will be in lowercase.
* The order of your output does not matter.

## Solution

First solution could be to use a hash map, to use the sorted anagram string as the key and an array of such strings as the value. This way, we can iterate through the array of strings, sort each string by character, and use the sorted string as the key and then insert into the corresponding array. Notice we have to sort each string, and if the maximum string length is given as k, and that we have n strings in our input array, the overall run-time complexity would be O(nk\*logk).

Second solution would to build a dictionary of the word count of each string using an array, using each character of the string as the index. We can then convert this integer array to a string, and use that as the key to the hash map we build. Notice that we don't have to sort each string in the array anymore, thus our run-time complexity is reduced to O(nk).

## Code
```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> hash;
        for (string s : strs) {
            hash[calc_key(s)].push_back(s);
        }
        vector<vector<string>> anagrams;
        for (auto group : hash) {
            anagrams.push_back(group.second);
        }
        return anagrams;
    }
    
private:
    string calc_key(string s) {
        // build dictionary of word count
        int dict[26] = {0};
        for (char c : s) {
            dict[c-'a']++;
        }
        // return string representation of word count
        string res;
        for (int i = 0; i < 26; i++) {
            res += string(dict[i], i);
        }
        return res;
    }
};
```