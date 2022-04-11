# Distinct Numbers in Window

## Problem statement

You are given an array of `N` integers, A1, A2 ,..., AN and an integer `B`. Return the of count of distinct numbers in all windows of size `B`.

Formally, return an array of size N-B+1 where i'th element in this array contains number of distinct elements in sequence Ai, Ai+1 ,..., Ai+B-1.

**NOTE:** if `B > N`, return an empty array.

## Solution

Time complexity : O(N\*log(B))  
Space complexity : O(B)

```cpp
dNums(vector<int> &A, int B) {
    map<int, int> mp;
    for(int i=0; i<B; i++) {
        mp[A[i]]++;
    }
    vector<int> res;
    res.push_back(mp.size());
    for(int i=B, n=A.size(); i<n; i++) {
        mp[A[i]]++;
        mp[A[i-B]]--;
        if(mp[A[i-B]] == 0) mp.erase(A[i-B]);
        res.push_back(mp.size());
    }
    return res;
}
```
