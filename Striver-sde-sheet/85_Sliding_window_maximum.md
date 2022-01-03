# Sliding window maximum

## Problem statement

You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return _the max sliding window_.

## Approach 1 (Brute force)

Time complexity : O(N\*K)  
Space complexity : O(1)

```cpp
int findMax(vector<int>& nums, int i, int j) {
    int mx = INT_MIN;
    while(i <= j)
        mx = max(mx, nums[i++]);
    return mx;
}
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    vector<int> res;
    for(int i=k-1; i<nums.size(); i++)
        res.push_back(findMax(nums, i-k+1, i));
    return res;
}
```

## Approach 2 (Multiset)

Time complexity : O(N\*log(K))  
Space complexity : O(K)

```cpp
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    multiset<int> st;
    for(int i=0; i<k; i++)
        st.insert(nums[i]);
    vector<int> res;
    res.push_back(*st.rbegin());
    for(int i=k; i<nums.size(); i++) {
        st.erase(st.find(nums[i-k]));
        st.insert(nums[i]);
        res.push_back(*st.rbegin());
    }
    return res;
}
```

## Approach 3 (Deque)

Time complexity : O(N)  
Space complexity : O(K)

```cpp
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    deque<int> dq;
    vector<int> res;
    for(int i=0; i<nums.size(); i++) {
        if(!dq.empty() && dq.front() == i-k) dq.pop_front();
        while(!dq.empty() && nums[dq.back()] <= nums[i])
            dq.pop_back();
        dq.push_back(i);
        if(i >= k-1) res.push_back(nums[dq.front()]);
    }
    return res;
}
```
