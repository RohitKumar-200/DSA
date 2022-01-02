# Largest rectangle in histogram

## Problem statement

Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return the area of the largest rectangle in the histogram.

## Approach 1

Time complexity : O(2N)  
Space complexity : O(N)

```cpp
int largestRectangleArea(vector<int>& heights) {
    int n = heights.size();
    vector<int> l(n);
    vector<int> r(n);
    stack<int> st;
    for(int i=0; i<n; i++) {
        while(!st.empty() && heights[st.top()] >= heights[i])
            st.pop();
        l[i] = st.empty() ? -1 : st.top();
        st.push(i);
    }
    while(!st.empty()) st.pop();
    for(int i=n-1; i>=0; i--) {
        while(!st.empty() && heights[st.top()] >= heights[i])
                st.pop();
        r[i] = st.empty() ? n : st.top();
        st.push(i);
    }
    int res = 0;
    for(int i=0; i<n; i++)
        res = max(res, heights[i] * (r[i]-l[i]-1));
    return res;
}
```

## Approach 2 (One pass)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
int largestRectangleArea(vector<int>& heights) {
    int n = heights.size(), res = 0;
    heights.push_back(0);
    stack<int> st;
    for(int i=0; i<=n; i++) {
        while(!st.empty() && heights[st.top()] > heights[i]) {
            int height = heights[st.top()];
            st.pop();
            int rightSmall = i;
            int leftSmall = st.empty() ? -1 : st.top();
            res = max(res, height * (rightSmall - leftSmall - 1));
        }
        st.push(i);
    }
    return res;
}
```
