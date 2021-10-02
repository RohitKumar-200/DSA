# Remove duplicates from sorted array

## Problem statement

Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

## Approach 1 (Hash set)

Time complexity : O(N\*log(N))  
Space complexity : O(N)

```cpp
int removeDuplicates(vector<int>& nums) {
    set<int> st;
    for(auto it:nums) st.insert(it);
    int i=0;
    for(auto it:st) nums[i++] = it;
    return i;
}
```

## Approach 2 (Two pointer)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
int removeDuplicates(vector<int>& nums) {
    if(nums.size() == 0) return 0;
    int i=0;
    for(int j=0; j<nums.size(); j++) {
        if(nums[j] != nums[i])
            nums[++i] = nums[j];
    }
    return i+1;
}
```
