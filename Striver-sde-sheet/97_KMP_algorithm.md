# Implement strStr()

## Problem statement

Implement `strStr()`.

Return the index of the first occurrence of needle in haystack, or `-1` if `needle` is not part of `haystack`.

**Note:**  
Return `0` when `needle` is an empty string. This is consistent to C's `strstr()` and Java's `indexOf()`.

## Solution (KMP Algorithm)

Time complexity : O(N)  
Space complexity : O(N+M)

```cpp
vector<int> getPiTable(string s) {
    int n = s.length();
    vector<int> piTable(n, 0);
    for(int i=1, len=0; i<n;) {
        if(s[i] == s[len]) {
            piTable[i] = len + 1;
            i++, len++;
        } else if(len > 0) {
            len = piTable[len-1];
        } else {
            i++;
        }
    }
    return piTable;
}
int strStr(string haystack, string needle) {
    int m = haystack.size(), n = needle.size();
    if(n == 0) return 0;
    vector<int> piTable = getPiTable(needle);
    int i = 0, j = 0;
    while(i < m) {
        if(j == n)
            return i - n;
        if(haystack[i] == needle[j])
            i++, j++;
        else if(j > 0)
            j = piTable[j-1];
        else
            i++;
    }
    return j==n ? i-n : -1;
}
```
