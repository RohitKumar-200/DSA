# Find median from data stream

## Problem statement

Implement the MedianFinder class:

- `MedianFinder()` initializes the `MedianFinder` object.
- `void addNum(int num)` adds the integer `num` from the data stream to the data structure.
- `double findMedian()` returns the median of all elements so far. Answers within 10<sup>-5</sup> of the actual answer will be accepted.

## Solution

Time complexity : O(log(N)) for addNum, O(1) for findMedian  
Space complexity : O(N)

```cpp
class MedianFinder {
    priority_queue<int> large;
    priority_queue<int, vector<int>, greater<int>> small;
public:
    void addNum(int num) {
        small.push(num);
        large.push(small.top());
        small.pop();
        if(small.size() < large.size()) {
            small.push(large.top());
            large.pop();
        }
    }

    double findMedian() {
        if(small.size() > large.size())
            return small.top();
        return (small.top() + large.top()) / 2.0;
    }
};
```
