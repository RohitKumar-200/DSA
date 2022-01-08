# Longest palindromic substring

## Problem statement

Given a string `s`, return the **longest palindromic substring** in `s`.

## Approach 1 (Brute force)

Time complexity : O(N^3)  
Space complexity : O(1)

```cpp
bool isPalindrome(int i, int j, string& s) {
    while(i < j)
        if(s[i++] != s[j--])
            return false;
    return true;
}
string longestPalindrome(string s) {
    int n = s.size(), start=0, end=0;
    for(int i=0; i<n; i++) {
        for(int j=i+1; j<n; j++)
            if(isPalindrome(i, j, s) && j-i+1 > end-start+1)
                start=i, end=j;
    }
    return s.substr(start, end-start+1);
}
```

## Approach 2

Time complexity : O(N^2)  
Space complexity : O(1)

```cpp
string longestPalindrome(string s) {
    int n = s.size(), start = 0, end = 0;
    for(int i=0; i<n; i++) {
        int l = i-1, r = i+1;
        while(l>=0 && r<n && s[l]==s[r]) l--, r++;
        if(end-start+1 < r-l-1) start=l+1, end=r-1;
    }
    for(int i=0; i<n-1; i++) {
        if(s[i] != s[i+1]) continue;
        int l = i-1, r = i+2;
        while(l>=0 && r<n && s[l]==s[r]) l--, r++;
        if(end-start+1 < r-l-1) start=l+1, end=r-1;
    }
    return s.substr(start, end-start+1);
}
```
