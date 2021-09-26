# Largest subarray with 0 sum

## Problem statement

Given an array having both positive and negative integers. The task is to compute the length of the largest subarray with sum 0.

## Approach 1 (Brute force, generating all subarrays)

Time complexity : O(N^3)  
Space complexity : O(1)

```cpp
int maxLen(vector<int>&A, int n) {
    int res=0;
    for(int i=0; i<n; i++) {
        for(int j=i+1; j<n; j++) {
            int sum=0;
            for(int k=i; k<=j; k++)
                sum+=A[k];
            if(sum==0)
                res = max(res, j-i+1);
        }
    }
    return res;
}
```

## Approach 2 (Brute optimal)

Time complexity : O(N^2)  
Space complexity : O(1)

```cpp
int maxLen(vector<int>&A, int n) {
    int res=0;
    for(int i=0; i<n; i++) {
        int sum=A[i];
        for(int j=i+1; j<n; j++) {
            sum+=A[j];
            if(sum==0)
                res = max(res, j-i+1);
        }
    }
    return res;
}
```

## Approach 3 (Hash map)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
int maxLen(vector<int>&A, int n) {
    int res=0, sum=0;
    unordered_map<int, int> mp;
    for(int i=0; i<n; i++) {
        sum+=A[i];
        if(A[i]==0 && res==0) res=1;
        if(sum==0) res=i+1;
        if(mp.find(sum) != mp.end())
            res = max(res, i-mp[sum]);
        else
            mp[sum] = i;
    }
    return res;
}
```
