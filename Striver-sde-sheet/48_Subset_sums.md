# Subset Sums

## Problem statement

Given a list arr of `N` integers, print sums of all subsets in it.

## Approach 1 (Power set)

Time complexity : O(N\*2^N)  
Space complexity : O(2^N)

```cpp
vector<vector<int>> getPowerSet(vector<int> &arr) {
    int n = arr.size(), pow_set_size = 1<<n;
    vector<vector<int>> res;
    for(int counter = 0; counter < pow_set_size; counter++) {
        vector<int> v;
        for(int j = 0; j < n; j++)
            if(counter & (1<<j))
                v.push_back(arr[j]);
        res.push_back(v);
    }
    return res;
}
vector<int> subsetSums(vector<int> arr, int N) {
    vector<vector<int>> powSet = getPowerSet(arr);
    vector<int> res;
    for(auto it:powSet) {
        int sum = 0;
        for(auto it2:it)
            sum+=it2;
        res.push_back(sum);
    }
    return res;
}
```

## Approach 2 (Recursion)

Time complexity : O(2^N)  
Space complexity : O(N)

```cpp
void findSubsetSums(int sum, int n, vector<int> &arr, vector<int> &res) {
    if(n==0) return res.push_back(sum);
    findSubsetSums(sum+arr[n-1], n-1, arr, res);
    findSubsetSums(sum, n-1, arr, res);
}
vector<int> subsetSums(vector<int> arr, int N) {
    vector<int> res;
    findSubsetSums(0, N, arr, res);
    return res;
}
```
