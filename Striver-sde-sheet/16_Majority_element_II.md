# Majority Element II

## Problem statement

Given an integer array of size `n`, find all elements that appear more than `⌊ n/3 ⌋` times.

## Approach 1 (Brute force)

Time complexity : O(N^2)  
Space complexity : O(1)

```cpp
vector<int> majorityElement(vector<int>& nums) {
    int n = nums.size();
    vector<int> res;
    int czero=0;
    for(auto it:nums)
        if(it==0) czero++;
    if(czero > n/3)
        res.push_back(0);
    for(int i=0; i<n; i++) {
        if(nums[i] == 0) continue;
        int count = 0, temp=nums[i];
        for(int j=0; j<n; j++)
            if(nums[j] == temp)
                count++, nums[j]=0;
        if(count > n/3) res.push_back(temp);
    }
    return res;
}
```

## Approach 2 (Hash Map)

Time complexity : O(N*log(N))  
Space complexity : O(N)

```cpp
vector<int> majorityElement(vector<int>& nums) {
    vector<int> res;
    map<int, int> mp;
    for(auto it:nums)
        mp[it]++;
    for(auto it:mp)
        if(it.second > nums.size()/3)
            res.push_back(it.first);
    return res;
}
```

## Approach 3 (Sorting)

Time complexity : O(N*log(N))  
Space complexity : O(1) (Ignoring space taken by sorting algorithm, else O(N))

```cpp
vector<int> majorityElement(vector<int>& nums) {
    vector<int> res;
    sort(nums.begin(), nums.end());
    int c=1, n=nums.size();
    for(int i=1; i<n; i++) {
        if(nums[i] == nums[i-1])
            c++;
        else {
            if(c > n/3)
                res.push_back(nums[i-1]);
            c=1;
        } 
    }
    if(c > n/3)
        res.push_back(nums[n-1]);
    return res;
}
```

## Approach 4 (Moore's Voting Algorithm)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
vector<int> majorityElement(vector<int>& nums) {
    int c1=0, c2=0, el1=-1, el2=-1;
    for(auto it:nums) {
        if(it == el1) c1++;
        else if(it == el2) c2++;
        else if(c1 == 0) el1=it, c1=1;
        else if(c2 == 0) el2=it, c2=1;
        else c1--, c2--;
    }
    c1=0, c2=0;
    for(auto it:nums) {
        if(it == el1) c1++;
        else if(it == el2) c2++;
    }
    vector<int> res;
    if(c1 > nums.size()/3) res.push_back(el1);
    if(c2 > nums.size()/3) res.push_back(el2);
    return res;
}
```
