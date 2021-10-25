# Combination sum II

## Problem statement

Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the `candidate` numbers sum to `target`.

Each number in `candidates` may only be used **once** in the combination.

**Note:** The solution set must not contain duplicate combinations.

## Approach 1 (Recursion + Hashing)

Time complexity : O(2^N \* k \* log(N)) (k = time to put element in data structure)  
Space complexity : O(l \* x) (l = average length, x = no. of unique combinations)

```cpp
void solve(int i, vector<int> &v, int target, vector<int> &candidates, set<vector<int>> &st) {
    if(target == 0) { st.insert(v); return; }
    if(i == candidates.size()) return;
    solve(i+1, v, target, candidates, st);
    if(candidates[i] <= target) {
        v.push_back(candidates[i]);
        solve(i+1, v, target-candidates[i], candidates, st);
        v.pop_back();
    }
}
vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
    sort(candidates.begin(), candidates.end());
    set<vector<int>> st;
    vector<int> v;
    solve(0, v, target, candidates, st);
    vector<vector<int>> res;
    for(auto it:st)
        res.push_back(it);
    return res;
}
```

## Approach 2 (Recursion by skipping duplicates)

Time complexity : O(2^N \* k)  
Space complexity : O(l \* x)

```cpp
void solve(int i, vector<int> &v, vector<int> &candidates, int target, vector<vector<int>> &res) {
    if(target==0) return res.push_back(v);
    if(i==candidates.size()) return;
    for(int j=i; j<candidates.size();) {
        if(target-candidates[j] >= 0) {
            v.push_back(candidates[j]);
            solve(j+1, v, candidates, target-candidates[j], res);
            v.pop_back();
        }
        j++;
        while(j<candidates.size() && candidates[j] == candidates[j-1]) j++;
    }
}
vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
    sort(candidates.begin(), candidates.end());
    vector<vector<int>> res;
    vector<int> v;
    solve(0, v, candidates, target, res);
    return res;
}
```
