# Reverse pairs

## Problem statement

Given an integer array `nums`, return the number of reverse pairs in the array.

A reverse pair is a pair `(i, j)` where `0 <= i < j < nums.length` and `nums[i] > 2 * nums[j]`.

## Approach 1 (Brute force)

Time complexity : O(N^2)  
Space complexity : O(1)

```cpp
int reversePairs(vector<int>& nums) {
    int n = nums.size(), res=0;
    for(int i=0; i<n; i++) {
        for(int j=i+1; j<n; j++)
            if(nums[i] > 2*nums[j])
                res++;
    }
    return res;
}
```

## Approach 2 (Merge sort)

Time complexity : O(N\*log(N))  
Space complexity : O(N)

```cpp
int mergeCount(int l, int r, vector<int>& nums, vector<int>& temp) {
    if(l==r) return 0;
    int mid = l + (r-l)/2, i, j, k;
    int res = mergeCount(l, mid, nums, temp) + mergeCount(mid+1, r, nums, temp);
    for(i=l, j=mid+1; i<=mid; i++) {
        while(j<=r && nums[i] > 2*(long)nums[j]) j++;
        res += j-mid-1;
    }
    for(i=l, j=mid+1, k=0; i<=mid && j<=r; k++) {
        if(nums[i] <= nums[j])
            temp[k] = nums[i++];
        else
            temp[k] = nums[j++];
    }
    while(i<=mid) temp[k++] = nums[i++];
    while(j<=r) temp[k++] = nums[j++];
    k=0;
    for(i=l; i<=r; i++) nums[i] = temp[k++];
    return res;
}
int reversePairs(vector<int>& nums) {
    vector<int> temp(nums.size());
    return mergeCount(0, nums.size()-1, nums, temp);
}
```
