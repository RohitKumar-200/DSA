# Subsets II

## Problem statement

Given an integer array `nums` that may contain duplicates, return all possible subsets (the power set).

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

## Approach 1

Time complexity : O((2^N)\*N\*log(N))  
Space complexity : O(2^N)

```cpp
vector<vector<int>> subsetsWithDup(vector<int>& nums) {
    set<vector<int>> st;
    int n = nums.size(), pow_set_size = (1<<n);
    for(int count=0; count<pow_set_size; count++) {
        vector<int> v;
        for(int j=0; j<n; j++)
            if(count & (1<<j))
                v.push_back(nums[j]);
        sort(v.begin(), v.end());
        st.insert(v);
    }
    vector<vector<int>> res;
    for(auto it:st)
        res.push_back(it);
    return res;
}
```

## Approach 2

Time complexity : O(N\*2^N)  
Space complexity : O(K\*2^N) (K = Average subset size)  
Auxiliary space : O(N)

```cpp
void findUniqueSubs(int i, vector<int> &nums, vector<int> v, vector<vector<int>> &res) {
    res.push_back(v);
    for(int j=i; j<nums.size();) {
        v.push_back(nums[j++]);
        findUniqueSubs(j, nums, v, res);
        v.pop_back();
        while(j<nums.size() && nums[j] == nums[j-1]) j++;
    }
}
vector<vector<int>> subsetsWithDup(vector<int>& nums) {
    vector<int> v;
    vector<vector<int>> res;
    sort(nums.begin(), nums.end());
    findUniqueSubs(0, nums, v, res);
    return res;
}
```
