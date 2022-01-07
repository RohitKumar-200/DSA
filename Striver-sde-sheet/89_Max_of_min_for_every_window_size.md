# Maximum of minimum for every window size

## Problem statement

Given an integer array. The task is to find the maximum of the minimum of every window size in the array.

**Note:** Window size varies from 1 to the size of the Array.

## Solution (Stack)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
vector <int> maxOfMin(int arr[], int n) {
    stack<int> st;
    vector<int> ans(n, 0), l(n, -1), r(n, n);
    for(int i=0; i<n; i++) {
        while(!st.empty() && arr[st.top()] > arr[i]) {
            r[st.top()] = i;
            st.pop();
        }
        if(!st.empty()) l[i] = st.top();
        st.push(i);
    }
    for(int i=0; i<n; i++) {
        int windowSize = r[i]-l[i]-1;
        ans[windowSize-1] = max(ans[windowSize-1], arr[i]);
    };
    for(int i=n-2; i>=0; i--)
        ans[i] = max(ans[i], ans[i+1]);
    return ans;
}
```
