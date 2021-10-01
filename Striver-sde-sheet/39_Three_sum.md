# Three sum

## Problem statement

Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

## Approach 1 (Brute force)

Time complexity : O(N^3 \* log(M))  
Space complexity : O(M) (M = no. of triplets in final answer)

```cpp
vector<vector<int>> threeSum(vector<int>& nums) {
    int n = nums.size();
    set<vector<int>> st;
    for(int i=0; i<n; i++) {
        for(int j=i+1; j<n; j++) {
            for(int k=j+1; k<n; k++) {
                if(nums[i] + nums[j] + nums[k] == 0) {
                    vector<int> v = {nums[i], nums[j], nums[k]};
                    sort(v.begin(), v.end());
                    st.insert(v);
                }
            }
        }
    }
    vector<vector<int>> res;
    for(auto it:st) res.push_back(it);
    return res;
}
```

## Approach 2 (Hash)

Time complexity : O(N^2 \* log(N) \* log(M))  
Space complexity : O(N + M)

```cpp
vector<vector<int>> threeSum(vector<int>& nums) {
    int n = nums.size();
    set<vector<int>> st;
    map<int, int> count;
    for(auto it:nums) count[it]++;
    for(int i=0; i<n; i++) {
        count[nums[i]]--;
        for(int j=i+1; j<n; j++) {
            count[nums[j]]--;
            int target = 0 - nums[i] - nums[j];
            auto it = count.find(target);
            if(it != count.end() && it->second > 0) {
                vector<int> v = {nums[i], nums[j], it->first};
                sort(v.begin(), v.end());
                st.insert(v);
            }
            count[nums[j]]++;
        }
        count[nums[i]]++;
    }
    vector<vector<int>> res;
    for(auto it:st) res.push_back(it);
    return res;
}
```

## Approach 3 (Two pointers)

Time complexity : O(N^2)  
Space complexity : O(M)

```cpp
vector<vector<int>> threeSum(vector<int>& nums) {
    int n = nums.size();
    sort(nums.begin(), nums.end());
    vector<vector<int>> res;
    for(int i=0; i<n;) {
        int target = -1*nums[i];
        for(int l=i+1, r=n-1; l<r;) {
            if(nums[l] + nums[r] < target) {
                l++;
                while(l<r && nums[l] == nums[l-1]) l++;
            } else if(nums[l] + nums[r] > target) {
                r--;
                while(r>l && nums[r] == nums[r+1]) r--;
            } else {
                res.push_back({nums[i], nums[l], nums[r]});
                l++, r--;
                while(l<r && nums[l] == nums[l-1]) l++;
                while(r>l && nums[r] == nums[r+1]) r--;
            }
        }
        i++;
        while(i<n && nums[i] == nums[i-1]) i++;
    }
    return res;
}
```
