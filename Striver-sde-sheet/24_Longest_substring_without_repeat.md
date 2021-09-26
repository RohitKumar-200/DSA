# Longest Substring Without Repeating Characters

## Problem statement

Given a string `s`, find the length of the **longest substring** without repeating characters.

## Approach 1 (Brute force)

Time complexity : O(N^2)  
Space compelxity : O(1) (Max of 256 char space is required, does not depend on N)

```cpp
int lengthOfLongestSubstring(string s) {
    int res = 0, n=s.size();
    for(int i=0; i<n; i++) {
        unordered_set<int> st;
        for(int j=i; j<n; j++) {
            if(st.find(s[j]) == st.end()) {
                res = max(res, j-i+1);
                st.insert(s[j]);
            }
            else break;
        }
    }
    return res;
}
```

## Approach 2 (Hash map & Two pointer)

Time complexity : O(2N)  
Space complexity : O(1)

```cpp
int lengthOfLongestSubstring(string s) {
    unordered_set<int> st;
    int res = 0, l=0, n=s.size();
    for(int r=0; r<n; r++) {
        if(st.find(s[r]) != st.end()) {
            do {
                st.erase(s[l]);
            } while(s[l++] != s[r]);
        }
        st.insert(s[r]);
        res = max(res, r-l+1);
    }
    return res;
}
```

## Approach 3 (One iteration & hash map)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
int lengthOfLongestSubstring(string s) {
    vector<int> index(256, -1);
    int res = 0, start=-1, n=s.size();
    for(int i=0; i<n; i++) {
        if(index[s[i]] > start)
            start = index[s[i]];
        index[s[i]] = i;
        res = max(res, i-start);
    }
    return res;
}
```
