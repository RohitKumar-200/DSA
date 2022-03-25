# Valid Anagram

## Problem statement

Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## Solution

Time complexity : O(N)  
Space complexity : O(26)

```cpp
bool isAnagram(string s, string t) {
    vector<int> freq(26, 0);
    for(char &ch:s) freq[ch-'a']++;
    for(char &ch:t) freq[ch-'a']--;
    for(int it:freq) {
        if(it != 0)
            return false;
    }
    return true;
}
```
