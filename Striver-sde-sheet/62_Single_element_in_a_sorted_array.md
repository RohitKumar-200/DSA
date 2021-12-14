# Single element in a sorted array

## Problem statement

You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once.

Return the single element that appears only once.

## Approach 1 (Brute force)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
int singleNonDuplicate(vector<int>& nums) {
    int n = nums.size();
    for(int i=0; i<n; i+=2) {
        if(i == n-1 || nums[i] != nums[i+1])
            return nums[i];
    }
    return -1;
}
```

## Approach 2 (XOR)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
int singleNonDuplicate(vector<int>& nums) {
    int res = 0;
    for(auto it:nums)
        res = res ^ it;
    return res;
}
```

## Approach 3 (Binary search)

Time complexity : O(log(N))  
Space complexity : O(1)

```cpp
int singleNonDuplicate(vector<int>& nums) {
    int l = 0, r = nums.size()-1;
    while(l < r) {
        int mid = l + (r-l)/2;
        if(mid & 1) {
            if(nums[mid] == nums[mid-1]) l = mid+1;
            else r = mid;
        } else {
            if(nums[mid] == nums[mid+1]) l = mid+1;
            else r = mid;
        }
    }
    return nums[l];
}
```

## Approach 4 (Short code of above approach)

Time complexity : O(log(N))  
Space complexity : O(1)

```cpp
int singleNonDuplicate(vector<int>& nums) {
    int l = 0, r = nums.size()-1;
    while(l < r) {
        int mid = l + (r-l)/2;
        if(nums[mid] == nums[mid^1]) l = mid+1;
        else r = mid;
    }
    return nums[l];
}
```
