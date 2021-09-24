# Two sum

## Problem statement

Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

You may assume that each input would have **exactly one solution**, and you may not use the same element twice.

You can return the answer in any order.

## Approach 1 (Brute force)

Time complexity : O(N^2)  
Space complexity : O(1)

```cpp
vector<int> twoSum(vector<int>& nums, int target) {
    int n = nums.size();
    for(int i=0; i<n; i++)
        for(int j=i+1; j<n; j++)
            if(nums[i]+nums[j] == target)
                return {i, j};
    return {-1,-1};
}
```

## Approach 2 (Hash map)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> mp;
    for(int i=0; i<nums.size(); i++) {
        if(mp.find(target-nums[i]) != mp.end())
            return {mp[target-nums[i]], i};
        else
            mp[nums[i]] = i;
    }
    return {-1,-1};
}
```
