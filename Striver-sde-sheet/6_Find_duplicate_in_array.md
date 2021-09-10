# Find the duplicate number

## Problem statement

Given an array of integers nums containing n + 1 integers where each integer is in the range [1, n] inclusive.

There is only one repeated number in nums, return this repeated number.

# Approach 1 (Sorting)

Time complexity : O(N\*log(N))  
Space complexity : O(1) (Ignoring space taken by sorting algo)

```cpp
int findDuplicate(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    for(int i=1; i<nums.size(); i++) {
        if(nums[i]==nums[i-1]) return nums[i];
    }
    return -1;
}
```

## Approach 2 (Calculate frequency)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
int findDuplicate(vector<int>& nums) {
    int n = nums.size();
    vector<int> freq(n+1, 0);
    for(int &i:nums) freq[i]++;
    for(int i=0; i<n+1; i++)
        if(freq[i]>1) return i;
    return -1;
}
```

## Approach 3 (Floyd's Tortoise and Hare)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
int findDuplicate(vector<int>& nums) {
    int tortoise = nums[0];
    int hare = nums[0];
    do {
        tortoise = nums[tortoise];
        hare = nums[nums[hare]];
    } while(tortoise != hare);
    tortoise = nums[0];
    while(tortoise != hare) {
        tortoise = nums[tortoise];
        hare = nums[hare];
    }
    return tortoise;
}
```
