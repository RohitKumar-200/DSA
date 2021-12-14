# Search in rotated sorted array

## Problem statement

There is an integer array nums sorted in ascending order (with distinct values).

Prior to being passed to your function, nums is **possibly rotated** at an unknown pivot index `k (1 <= k < nums.length)` such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (0-indexed). For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index `3` and become `[4,5,6,7,0,1,2]`.

Given the array `nums` **after** the possible rotation and an integer `target`, return the _index_ of `target` if it is in `nums`, or `-1` if it is not in `nums`.

## Approach 1 (Two binary search)

Time complexity : O(log(N))  
Space complexity : O(1)

```cpp
int search(vector<int>& nums, int target) {
    int n = nums.size(), l = 0, r = n-1, mid;
    while(l < r) {
        mid = l + (r-l)/2;
        if(nums[mid] > nums[r]) l = mid+1;
        else r = mid;
    }
    int rot = l, realMid;
    l = 0, r = n-1;
    while(l <= r) {
        mid = l + (r-l)/2;
        realMid = (mid+rot)%n;
        if(nums[realMid] == target) return realMid;
        else if(nums[realMid] < target) l = mid+1;
        else r = mid-1;
    }
    return -1;
}
```

## Approach 2

Time complexity : O(log(N))  
Space complexity : O(1)

```cpp
int search(vector<int>& nums, int target) {
    int l = 0, r = nums.size()-1;
    while(l <= r) {
        int mid = l + (r-l)/2;
        if(nums[mid] == target) return mid;
        if(nums[l] <= nums[mid]) {
            if(nums[l] <= target && target <= nums[mid])
                r = mid-1;
            else
                l = mid+1;
        } else {
            if(nums[mid] <= target && target <= nums[r])
                l = mid+1;
            else
                r = mid-1;
        }
    }
    return -1;
}
```

## Approach 3

Time complexity : O(log(N))  
Space complexity : O(1)

```cpp
int search(vector<int>& nums, int target) {
    int n = nums.size(), l = 0, r = n-1, mid;
    while(l < r) {
        mid = (l + r)/2;
        if((nums[n-1]-nums[mid])*(nums[n-1]-target) > 0) {
            if(nums[mid] < target) l = mid+1;
            else r = mid;
        } else if(target > nums[n-1]) {
            r = mid;
        } else {
            l = mid+1;
        }
    }
    return (nums[l] == target) ? l : -1;
}
```
