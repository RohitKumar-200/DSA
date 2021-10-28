# All permutations

## Problem statement

Given an array `nums` of distinct integers, return all the possible permutations. You can return the answer in **any order**.

## Solution (Recursion)

Time complexity : O(N! \* N)  
Space complexity : O(N! \* N) (O(1) if we ignore space by res)

```cpp
void findPermutations(int i, vector<int> &nums, vector<vector<int>> &res) {
    int n = nums.size();
    if(i == n) return res.push_back(nums);
    for(int j=i; j<n; j++) {
        swap(nums[i], nums[j]);
        findPermutations(i+1, nums, res);
        swap(nums[i], nums[j]);
    }
}
vector<vector<int>> permute(vector<int>& nums) {
    vector<vector<int>> res;
    findPermutations(0, nums, res);
    return res;
}
```

---

> Follow up

---

## To get all permutatins in ascending order

Time complexity : O(N! \* N)  
Space complexity : O(N! \* N)

```cpp
void findPermutations(int i, vector<int> &nums, vector<vector<int>> &res) {
    int n = nums.size();
    if(i == n) return res.push_back(nums);
    for(int j=i; j<n; j++) {
        swap(nums[i], nums[j]);
        findPermutations(i+1, nums, res);
    }
    int temp = nums[i];
    for(int j=i; j<n-1; j++) nums[j] = nums[j+1];
    nums[n-1] = temp;
}
vector<vector<int>> permute(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    vector<vector<int>> res;
    findPermutations(0, nums, res);
    return res;
}
```
