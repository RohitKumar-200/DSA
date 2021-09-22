# Next Permutation

## Problem statement

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such an arrangement is not possible, it must rearrange it as the lowest possible order (i.e., sorted in ascending order).

## Approach 1 (Brute force)

Time complexity : O(N! \* N)  
Space complexity : O(N! \* N)

```cpp
void getPermutations(int i, vector<int> nums, vector<vector<int>>& p) {
    if(i==nums.size())
        p.push_back(nums);
    for(int j=i; j<nums.size(); j++) {
        swap(nums[i], nums[j]);
        getPermutations(i+1, nums, p);
    }
}
void nextPermutation(vector<int>& nums) {
    vector<int> v(nums.begin(), nums.end());
    sort(v.begin(), v.end());
    vector<vector<int>> p;
    getPermutations(0, v, p);
    for(int i=0; i<p.size(); i++) {
        if(p[i]==nums) {
            int ind = (i+1)%p.size();
            nums = p[ind];
            break;
        }
    }
}
```

## Approach 2 (Optimal)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
void nextPermutation(vector<int>& nums) {
    int x=-1, y=-1, n=nums.size(), i;
    for(i=n-2; i>=0; i--) {
        if(nums[i]<nums[i+1]) {
            x=i;
            break;
        }
    }
    if(x==-1) {
        reverse(nums.begin(), nums.end());
        return;
    }
    for(i=n-1; i>=0; i--) {
        if(nums[i]>nums[x]) {
            y=i;
            break;
        }
    }
    swap(nums[x], nums[y]);
    reverse(nums.begin()+x+1, nums.end());
}
```

## Approach 3 (Using STL with above approach)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
void nextPermutation(vector<int>& nums) {
    auto i = is_sorted_until(nums.rbegin(), nums.rend());
    if (i != nums.rend())
        swap(*i, *upper_bound(nums.rbegin(), i, *i));
    reverse(nums.rbegin(), i);
}
```

## Approach 4 (Using STL, not for Interviews)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
void nextPermutation(vector<int>& nums) {
    next_permutation(nums.begin(), nums.end());
}
```
