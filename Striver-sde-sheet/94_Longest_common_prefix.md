# Longest common prefix

## Problem statement

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

## solution

Time complexity : O(N\*M)  
Space complexity : O(1)

```cpp
string longestCommonPrefix(vector<string>& strs) {
    if(strs.size() == 0) return "";
    int len = strs[0].size();
    for(int i=1; i<strs.size(); i++) {
        for(int j=0; j<len; j++) {
            if(strs[i][j] != strs[i-1][j]) {
                len = j;
                break;
            }
        }
    }
    return strs[0].substr(0, len);
}
```
