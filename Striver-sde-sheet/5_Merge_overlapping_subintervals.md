# Merge overlapping subintervals

## Problem statement

Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

## Approach 1 [ O(N^2) ]

```cpp
vector<vector<int>> merge(vector<vector<int>>& intervals) {
    vector<vector<int>> res;
    int n = intervals.size();
    vector<bool> vis(n, 0);
    for(int i=0; i<n; i++) {
        if(vis[i]) continue;
        int x = intervals[i][0], y = intervals[i][1];
        for(int k=0; k<2; k++) // to run next loop twice, to include all possible pairs
        for(int j=i+1; j<n; j++) {
            if(!vis[j] && ((intervals[j][0]>=x && intervals[j][0]<=y) || (intervals[j][1]>=x && intervals[j][1]<=y))) {
                vis[j] = true;
                x = min(x, intervals[j][0]);
                y = max(y, intervals[j][1]);
            }
        }
        res.push_back({x, y});
    }
    return res;
}
```

## Approach 2 [ O(N\*log(N)) ]

```cpp
vector<vector<int>> merge(vector<vector<int>>& intervals) {
    vector<vector<int>> res;
    sort(intervals.begin(), intervals.end());
    int x = intervals[0][0], y = intervals[0][1];
    for(auto it:intervals) {
        if(it[0] <= y)
            y = max(y, it[1]);
        else {
            res.push_back({x, y});
            x = it[0];
            y = it[1];
        }
    }
    res.push_back({x, y});
    return res;
}
```
