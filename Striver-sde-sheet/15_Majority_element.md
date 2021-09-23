# Majority element

## Problem statement

Given an array `nums` of size `n`, return the majority element.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

## Approach 1 (Brute force)

Time complexity : O(N^2)  
Space complexity : O(1)

```cpp
int majorityElement(vector<int>& nums) {
    int n = nums.size();
    for(int i=0; i<n; i++) {
        int count = 0;
        for(int j=0; j<n; j++)
            if(nums[j] == nums[i])
                count++;
        if(count > n/2) return nums[i];
    }
    return 0;
}
```

## Approach 2 (Hash Map)

Time complexity : O(N*log(N))  
Space complexity : O(N)

```cpp
int majorityElement(vector<int>& nums) {
    int n = nums.size();
    map<int, int> mp;
    for(auto it:nums) {
        mp[it]++;
        if(mp[it] > n/2)
            return it;
    }
    return 0;
}
```

## Approach 3 (Sorting)

Time complexity : O(N*log(N))  
Space complexity : O(1) (Ignoring space taken by sorting algorithm, else O(N))

```cpp
int majorityElement(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    int c=1, n=nums.size();
    for(int i=1; i<n; i++) {
        if(nums[i] == nums[i-1])
            c++;
        else {
            if(c > n/2)
                return nums[i-1];
            c=1;
        } 
    }
    return nums[n-1];
}
```

## Approach 4 (Moore's Voting Algorithm)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
int majorityElement(vector<int>& nums) {
    int count=0, el=nums[0], n=nums.size();
    for(int i=0; i<n; i++) {
        if(count == 0)
            el = nums[i];
        if(el == nums[i])
            count++;
        else
            count--;
    }
    return el;
}
```
