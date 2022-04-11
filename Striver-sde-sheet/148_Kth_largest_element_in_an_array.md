# Kth Largest Element in an Array

## Problem statement

Given an integer array `nums` and an integer `k`, return the **kth largest element** in the array.

**Note:** that it is the kth largest element in the sorted order, not the kth distinct element.

## Solution

Time complexity : O(N\*log(K))  
Space complexity : O(K)

```cpp
int findKthLargest(vector<int>& nums, int k) {
    priority_queue<int, vector<int>, greater<int>> pq;
    for(int &num:nums) {
        pq.push(num);
        if(pq.size()>k) pq.pop();
    }
    return pq.top();
}
```
