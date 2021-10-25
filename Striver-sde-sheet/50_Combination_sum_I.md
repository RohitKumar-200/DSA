# Combination Sum I

## Problem statement

Given an array of **distinct** integers `candidates` and a target integer `target`, return a list of all **unique combinations** of `candidates` where the chosen numbers sum to target. You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

It is **guaranteed** that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

## Solution (Recursion)

Time complexity : O(2^t \* k) (t = target, k = time to put element in data structure)  
Space complexity : O(l \* x) (l = average length, x = no. of combinations)

```cpp
void findCombinationSum(int i, vector<int> v, vector<int> &candidates, int target, vector<vector<int>> &res) {
    if(target == 0) return res.push_back(v);
    if(i<0) return;
    findCombinationSum(i-1, v, candidates, target, res);
    if(candidates[i] <= target) {
        v.push_back(candidates[i]);
        findCombinationSum(i, v, candidates, target-candidates[i], res);
        v.pop_back();
    }
}
vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
    vector<vector<int>> res;
    findCombinationSum(candidates.size()-1, vector<int>(), candidates, target, res);
    return res;
}
```
