# Next greater element

## Problem statement

Given an array `arr[]` of size `N` having distinct elements, the task is to find the next greater element for each element of the array in order of their appearance in the array.

Next greater element of an element in the array is the nearest element on the right which is greater than the current element.

If there does not exist next greater of current element, then next greater element for current element is `-1`.  
For example, next greater of the last element is always `-1`.

## Solution

Time complexity : O(N)  
Space complexity : O(N)

```cpp
vector<long long> nextLargerElement(vector<long long> arr, int n){
    vector<long long> res(n);
    stack<long long> st;
    for(int i=n-1; i>=0; i--) {
        while(!st.empty() && st.top() <= arr[i])
            st.pop();
        res[i] = st.empty() ? -1 : st.top();
        st.push(arr[i]);
    }
    return res;
}
```
