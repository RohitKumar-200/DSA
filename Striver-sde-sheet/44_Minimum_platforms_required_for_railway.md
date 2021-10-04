# Minimum no. of platforms required for a railway

## Problem statement

Given arrival and departure times of all trains that reach a railway station. Find the minimum number of platforms required for the railway station so that no train is kept waiting.
Consider that all the trains arrive on the same day and leave on the same day. Arrival and departure time can never be the same for a train but we can have arrival time of one train equal to departure time of the other. At any given instance of time, same platform can not be used for both departure of a train and arrival of another train. In such cases, we need different platforms.

## Approach 1

Time complexity : O(N\*log(N))  
Space complexity : O(N)

```cpp
static bool comp(pair<int, int> p1, pair<int, int> p2) {
    if(p1.first < p2.first)
        return true;
    else if(p1.first == p2.first)
        return p1.second > p2.second;
    return false;
}
int findPlatform(int arr[], int dep[], int n) {
    vector<pair<int, int>> vp;
    for(int i=0; i<n; i++) {
        vp.push_back({arr[i], 1});
        vp.push_back({dep[i], -1});
    }
    sort(vp.begin(), vp.end(), comp);
    int res = 1, curr=0;
    for(auto it:vp) {
        curr += it.second;
        res = max(res, curr);
    }
    return res;
}
```

## Approach 2

Time complexity : O(N\*log(N))  
Space complexity : O(1) (Ignoring space taken by merge sort)

```cpp
int findPlatform(int arr[], int dep[], int n) {
    sort(arr, arr+n);
    sort(dep, dep+n);
    int pNeeded = 1, res = 1;
    int i = 1, j = 0;
    while(i<n) {
        if(arr[i] <= dep[j]) {
            pNeeded++;
            i++;
        } else {
            pNeeded--;
            j++;
        }
        res = max(res, pNeeded);
    }
    return res;
}
```
