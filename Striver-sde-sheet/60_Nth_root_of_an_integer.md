# Find Nth root of M

## Problem statement

You are given `2` numbers `(n , m)`; the task is to find **<sup>n</sup>√m** (nth root of m).

## Solution

Time complexity : O(log(n)\*log(m))  
Space complexity : O(1)

```cpp
int NthRoot(int n, int m) {
    int lo = 1, hi = m, mid;
    while(lo < hi) {
        mid = lo + (hi-lo)/2;
        if(pow(mid, n) < m) lo = mid + 1;
        else hi = mid;
    }
    return pow(lo, n) == m ? lo : -1;
}
```
