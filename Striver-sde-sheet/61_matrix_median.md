# Matrix median

## Problem statement

Given a matrix of integers `A` of size `N x M` in which each row is **sorted**.

Find an return the overall **median** of the matrix `A`.

**Note:** Rows are numbered from top to bottom and columns are numbered from left to right.

## Constraint

- 1 <= N, M <= 10^5
- 1 <= N\*M <= 10^6
- 1 <= A[i] <= 10^9
- N\*M is odd

## Approach 1 (Binary search + Extra space)

Time comoplexity : O(n\*m\*log(n\*m))  
Space complexity : O(n\*m)

```cpp
findMedian(vector<vector<int> > &A) {
    int n = A.size(), m = A[0].size();
    vector<int> v;
    for(auto it1:A) {
        for(auto it2:it1)
            v.push_back(it2);
    }
    sort(v.begin(), v.end());
    return v[(n*m)/2];
}
```

## Approach 2 (Binary search)

Time complexity : O(n\*log(m) \* log(INT_MAX))  
Space complexity : O(1)

```cpp
int countSmaller(int x, vector<int> &v) {
    int l = 0, h = v.size()-1;
    while(l <= h) {
        int mid = l + (h-l)/2;
        if(v[mid] <= x) l = mid+1;
        else h = mid-1;
    }
    return l;
}
int Solution::findMedian(vector<vector<int> > &A) {
    int low = 1, high = 1e9, n = A.size(), m = A[0].size();
    while(low <= high) {
        int mid = low + (high-low)/2, cnt = 0;
        for(auto &it:A)
            cnt += countSmaller(mid, it);
        if(cnt <= (n*m)/2) low = mid + 1;
        else high = mid - 1;
    }
    return low;
}
```
