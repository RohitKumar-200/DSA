# Median of two sorted arrays

## Problem statement

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return the **median** of the two sorted arrays.

## Approach 1

Time complexity : O(M+N)  
Space complexity : O(M+N)

```cpp
double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
    vector<int> v;
    int n1 = nums1.size(), n2 = nums2.size(), i = 0, j = 0;
    while(i<n1 && j<n2) {
        if(nums1[i] <= nums2[j]) v.push_back(nums1[i++]);
        else v.push_back(nums2[j++]);
    }
    while(i<n1) v.push_back(nums1[i++]);
    while(j<n2) v.push_back(nums2[j++]);
    int n = v.size();
    if(n & 1) return v[n/2];
    return (v[(n-1)/2] + v[n/2]) / 2.0;
}
```

## Approach 2

Time complexity : O(M+N)  
Space complexity : O(1)

```cpp
double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
    int n1 = nums1.size(), n2 = nums2.size(), n = n1+n2, i = 0, j = 0, x = 0, y = 0, ind = 0;
    while(i<n1 || j<n2) {
        int num1 = i<n1 ? nums1[i] : INT_MAX;
        int num2 = j<n2 ? nums2[j] : INT_MAX;
        if(ind == (n-1)/2) x = min(num1, num2);
        if(ind == n/2) y = min(num1, num2);
        if(num1 <= num2) i++;
        else j++;
        ind++;
    }
    if(n & 1) return y;
    return (x + y) / 2.0;
}
```

## Approach 3

Time complexity : O(log(min(M, N)))  
Space complexity : O(1)

```cpp
double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
    if(nums2.size() < nums1.size()) return findMedianSortedArrays(nums2, nums1);
    int n1 = nums1.size(), n2 = nums2.size();
    int l = 0, r = n1;
    while(l <= r) {
        int cut1 = (l + r) / 2;
        int cut2 = (n1 + n2 + 1)/2 - cut1;

        int left1 = cut1 == 0 ? INT_MIN : nums1[cut1-1];
        int left2 = cut2 == 0 ? INT_MIN : nums2[cut2-1];
        int right1 = cut1 == n1 ? INT_MAX : nums1[cut1];
        int right2 = cut2 == n2 ? INT_MAX : nums2[cut2];

        if(left1 <= right2 && left2 <= right1) {
            if((n1 + n2) % 2 == 0)
                return (max(left1, left2) + min(right1, right2)) / 2.0;
            else
                return max(left1, left2);
        } else if(left1 > right2) {
            r = cut1 - 1;
        } else {
            l = cut1 + 1;
        }
    }
    return 0.0;
}
```
