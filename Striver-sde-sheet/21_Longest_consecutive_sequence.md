# Longest Consecutive Sequence

## Problem statement

Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.

## Approach 1 (Brute force)

Time complexity : O(N\*log(N))  
Space complexity : O(N) (Due to merge sort)

```cpp
int longestConsecutive(vector<int>& nums) {
    if(nums.size()==0) return 0;
    sort(nums.begin(), nums.end());
    int res=0, c=1, n=nums.size();
    for(int i=1; i<n; i++) {
        if(nums[i] == nums[i-1]+1)
            c++;
        else {
            res = max(res, c);
            c=1;
        }
    }
    res = max(res, c);
    return res;
}
```

## Approach 2 (Hash)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
int longestConsecutive(vector<int>& nums) {
    int res=0;
    unordered_set<int> st;
    for(auto it:nums) st.insert(it);
    for(auto it:nums) {
        if(st.find(it-1) == st.end()) {
            int x=it+1;
            while(st.find(x) != st.end()) x++;
            res = max(res, x-it);
        }
    }
    return res;
}
```
