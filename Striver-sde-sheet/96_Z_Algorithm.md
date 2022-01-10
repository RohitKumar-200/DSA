# Implement strStr()

## Problem statement

Implement `strStr()`.

Return the index of the first occurrence of needle in haystack, or `-1` if `needle` is not part of `haystack`.

**Note:**  
Return `0` when `needle` is an empty string. This is consistent to C's `strstr()` and Java's `indexOf()`.

## Approach 1 (Brute force)

Time complexity : O(N\*M)  
Space complexity : O(1)

```cpp
int strStr(string haystack, string needle) {
    int m = haystack.size(), n = needle.size();
    if(n == 0) return 0;
    for(int i=0; i<m; i++) {
        int j=0;
        for(; j<n; j++) {
            if(haystack[i+j] != needle[j])
                break;
        }
        if(j == n)
            return i;
    }
    return -1;
}
```

## Approach 2 (Z algorithm)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
vector<int> calculateZ(string s) {
    int n = s.size(), left = 0, right = 0;
    vector<int> z(n, 0);
    for(int k=1; k<n; k++) {
        if(k > right) {
            left = right = k;
            while(right < n && s[right-left] == s[right])
                right++;
            z[k] = right - left;
            right--;
        } else {
            int k1 = k - left;
            if(z[k1] <= right-k) {
                z[k] = z[k1];
            } else {
                left = k;
                while(right < n && s[right-left] == s[right])
                    right++;
                z[k] = right - left;
                right--;
            }
        }
    }
    return z;
}
int strStr(string haystack, string needle) {
    if(needle.size() == 0) return 0;
    int m = needle.size(), n = haystack.size(),res = 0;
    vector<int> z = calculateZ(needle + "$" + haystack);
    for(int i=m+1; i<m+n+1; i++)
        if(z[i] == m)
            return i-m-1;
    return -1;
}
```
