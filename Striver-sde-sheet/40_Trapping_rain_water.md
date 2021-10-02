# Trapping rain water

## Problem statement

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

## Approach 1 (Brute force)

Time complexity : O(N^2)  
Space complexity : O(1)

```cpp
int trap(vector<int>& height) {
    int n = height.size(), res=0;
    for(int i=1; i<n-1; i++) {
        int maxL = 0, maxR = 0;
        for(int j=i-1; j>=0; j--)
            maxL = max(maxL, height[j]);
        for(int j=i+1; j<n; j++)
            maxR = max(maxR, height[j]);
        int tappedWater = min(maxL, maxR) - height[i];
        if(tappedWater < 0) tappedWater = 0;
        res += tappedWater;
    }
    return res;
}
```

## Approach 2 (Precomputation)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
int trap(vector<int>& height) {
    int n = height.size(), res=0;
    int maxL = height[0], maxR = height[n-1];
    vector<int> l(n);
    vector<int> r(n);
    for(int i=1; i<n; i++) {
        l[i] = maxL;
        maxL = max(maxL, height[i]);
    }
    for(int i=n-2; i>=0; i--) {
        r[i] = maxR;
        maxR = max(maxR, height[i]);
    }
    for(int i=1; i<n-1; i++) {
        int tappedWater = min(l[i], r[i]) - height[i];
        res += tappedWater>0 ? tappedWater : 0;
    }
    return res;
}
```

## Approach 3 (Two pointer)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
int trap(vector<int>& height) {
    int l = 0, r = height.size()-1, maxL = 0, maxR = 0, res = 0;
    while(l <= r) {
        if(height[l] <= height[r]) {
            if(height[l] >= maxL)
                maxL = height[l];
            else
                res += maxL - height[l];
            l++;
        } else {
            if(height[r] >= maxR)
                maxR = height[r];
            else
                res += maxR - height[r];
            r--;
        }
    }
    return res;
}
```
