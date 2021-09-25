# Four sum problem

## Problem statement

Given an array `nums` of `n` integers, return an array of all the unique quadruplets `[nums[a], nums[b], nums[c], nums[d]]` such that:

- 0 <= a, b, c, d < n
- a, b, c, and d are distinct.
- nums[a] + nums[b] + nums[c] + nums[d] == target

You may return the answer in any order.

## Approach 1 (Brute force)

Time complexity : O(N^4 \* log(N))  
Space complexity : O(N)

```cpp
vector<vector<int>> fourSum(vector<int>& nums, int target) {
    int n = nums.size();
    vector<vector<int>> res;
    set<vector<int>> st;
    for(int i=0; i<n; i++)
        for(int j=i+1; j<n; j++)
            for(int k=j+1; k<n; k++)
                for(int l=k+1; l<n; l++)
                    if(nums[i]+nums[j]+nums[k]+nums[l] == target) {
                        vector<int> v = {nums[i], nums[j], nums[k], nums[l]};
                        sort(v.begin(), v.end());
                        st.insert(v);
                    }
    for(auto it:st) res.push_back(it);
    return res;
}
```

## Approach 2 (3 loop + binary search)

Time complexity : O(N^3 \* log(N) \* log(N))  
Space complexity : O(N)

```cpp
 vector<vector<int>> fourSum(vector<int>& nums, int target) {
    int n = nums.size();
    sort(nums.begin(), nums.end());
    vector<vector<int>> res;
    set<vector<int>> st;
    for(int i=0; i<n; i++)
        for(int j=i+1; j<n; j++)
            for(int k=j+1; k<n; k++) {
                long long x = (long long)target - nums[i] - nums[j] - nums[k];
                if(binary_search(nums.begin()+k+1, nums.end(), x))
                    st.insert({nums[i], nums[j], nums[k], (int)x});
            }
    for(auto it:st)
        res.push_back(it);
    return res;
}
```

## Approach 3 (2 loop + 1 iteration)

Time complexity : O(N^3)  
Space complexity : O(1) (Ignoring sorting and res space)

```cpp
vector<vector<int>> fourSum(vector<int>& nums, int target) {
    int n = nums.size();
    sort(nums.begin(), nums.end());
    vector<vector<int>> res;
    for(int i=0; i<n;) {
        for(int j=i+1; j<n;) {
            for(int l=j+1, r=n-1; l<r;) {
                long long x = (long long)target - nums[i] - nums[j];
                long long left = nums[l], right = nums[r];
                if(left + right < x) {
                    l++;
                    while(l<r && nums[l]==nums[l-1]) l++;
                } else if (left + right > x) {
                    r--;
                    while(r>l && nums[r]==nums[r+1]) r--;
                } else {
                    res.push_back({nums[i], nums[j], nums[l], nums[r]});
                    l++, r--;
                    while(l<r && nums[l]==nums[l-1]) l++;
                    while(r>l && nums[r]==nums[r+1]) r--;
                }
            }
            j++;
            while(j<n && nums[j]==nums[j-1]) j++;
        }
        i++;
        while(i<n && nums[i]==nums[i-1]) i++;
    }
    return res;
}
```
