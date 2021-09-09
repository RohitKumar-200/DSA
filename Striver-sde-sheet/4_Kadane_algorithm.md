# Maximum subarray sum

## Problem statement

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

## Approach 1 [ O(N^3) ]

```cpp
int maxSubArray(vector<int>& nums) {
    int n = nums.size(), res=nums[0];
    for(int i=0; i<n; i++) {
        for(int j=i; j<n; j++) {
            int sum = 0;
            for(int k=i; k<=j; k++)
                sum+=nums[k];
            res = max(res, sum);
        }
    }
    return res;
}
```

## Approach 2 [ O(N^2) ]

```cpp
int maxSubArray(vector<int>& nums) {
    int n = nums.size(), res=nums[0];
    for(int i=0; i<n; i++) {
        int sum = 0;
        for(int j=i; j<n; j++) {
            sum += nums[j];
            res = max(res, sum);
        }
    }
    return res;
}
```

## Approach 3 [ O(N) ] -> Kadane's algorithm

```cpp
int maxSubArray(vector<int>& nums) {
    int n = nums.size(), maxi = nums[0], sum=nums[0];
    for(int i=1; i<n; i++) {
        if(sum<0) sum=0;
        sum += nums[i];
        maxi = max(maxi, sum);
    }
    return maxi;
}
```
