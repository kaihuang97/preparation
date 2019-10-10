# Valid Anagram

## Problem

Given two strings s and t , write a function to determine if t is an anagram of s.

**Example 1:**

	Input: s = "anagram", t = "nagaram"
	Output: true
**Example 2:**

	Input: s = "rat", t = "car"
	Output: false
**Note:**
You may assume the string contains only lowercase alphabets.

**Follow up:**
What if the inputs contain unicode characters? How would you adapt your solution to such case?

## Solution

Using a hash map allows us to store character frequencies. Various solutions are possible:
* We can populate a hash map for one string, and then decrement the values of that map to the characters of the second string. If the empty is empty after traversing the second string, then they are valid anagrams, else not.
* We can store both strings in seperate maps, and then compare the two maps. If the two maps are identical, then they are anagrams, else not. 
* We can use an ASCII array to store each character (using character as integer index value), and checking for an array of all zeroes would yield anagram, else not.


## Code
```java
// Deletion of key when found, empty map signifies anagram
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;
        
        Map<Character, Integer> dict = new HashMap<>(); 
        for (int i = 0; i < s.length(); i++) {
            if (dict.containsKey(s.charAt(i))) {
                dict.put(s.charAt(i), dict.get(s.charAt(i))+1);
            } else {
                dict.put(s.charAt(i), 1);
            }
        }
        
        for (int i = 0; i < t.length(); i++) {
            if (dict.containsKey(t.charAt(i))) {
                dict.put(t.charAt(i), dict.get(t.charAt(i))-1);
                if (dict.get(t.charAt(i)) == 0) {
                    dict.remove(t.charAt(i));
                }
            } else {
                return false;
            }
        }
        
        return dict.isEmpty();
    }
}

// Using Map comparison
class Solution {
    public boolean isAnagram(String s, String t) {
        Map<Character,Integer> sChars = new HashMap<>();
        Map<Character,Integer> tChars = new HashMap<>();
        if (s.length() != t.length()) return false;
        for (int i = 0; i<s.length(); i++) {
            addToMap(sChars, s.charAt(i));
            addToMap(tChars, t.charAt(i));
        }
        return sChars.equals(tChars);
    }
    private void addToMap(Map<Character,Integer> map, char c) {
        if (map.keySet().contains(c)) {
            map.put(c,map.get(c)+1);
        } else {
            map.put(c,1);
        }
    }
}


// dictionary alphabet array
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;
        
        int[] dict = new int[26];
        
        for (int i = 0; i < s.length(); i++) {
            dict[s.charAt(i)-'a']++;
        }
        
        for (int i = 0; i < t.length(); i++) {
            if (dict[t.charAt(i)-'a'] > 0) dict[t.charAt(i)-'a']--;
            else return false;
        }
        
        for (int i = 0; i < dict.length; i++) {
            if (dict[i] != 0) return false;
        }
        
        return true;
    }
}
```