# Kth Largest Element in a Stream

## Problem statement

Design a class to find the `kth` largest element in a stream. Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

Implement `KthLargest` class:

- `KthLargest(int k, int[] nums)` Initializes the object with the integer `k` and the stream of integers `nums`.
- `int add(int val)` Appends the integer `val` to the stream and returns the element representing the `kth` largest element in the stream.

## Solution

Time complexity : O(N\*log(K))  
Space complexity : O(K)

```cpp
class KthLargest {
    priority_queue<int, vector<int>, greater<int>> pq;
    int K;
public:
    KthLargest(int k, vector<int>& nums) {
        for(auto it:nums) {
            pq.push(it);
            if(pq.size() > k)
                pq.pop();
        }
        K = k;
    }

    int add(int val) {
        pq.push(val);
        if(pq.size() > K)
            pq.pop();
        return pq.top();
    }
};
```
