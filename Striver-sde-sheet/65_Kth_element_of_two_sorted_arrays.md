# Kth element of two sorted arrays

## Problem statement

Given two sorted arrays `arr1` and `arr2` of size `N` and `M` respectively and an element `K`. The task is to find the element that would be at the **k’th position** of the final sorted array.

## Approach 1

Time complexity : O(M+N)  
Space complexity : O(M+N)

```cpp
int kthElement(int arr1[], int arr2[], int n, int m, int k) {
    int arr[n+m], i=0, j=0, z=0;
    while(i<n && j<m) {
        if(arr1[i] <= arr2[j]) arr[z++] = arr1[i++];
        else arr[z++] = arr2[j++];
    }
    while(i<n) arr[z++] = arr1[i++];
    while(j<m) arr[z++] = arr2[j++];
    return arr[k-1];
}
```

## Approach 2

Time complexity : O(M+N)  
Space complexity : O(1)

```cpp
int kthElement(int arr1[], int arr2[], int n, int m, int k) {
    int i=0, j=0, z=0;
    while(i<n || j<m) {
        int a1 = i<n ? arr1[i] : INT_MAX;
        int a2 = j<m ? arr2[j] : INT_MAX;
        if(--k == 0) return min(a1, a2);
        if(a1 <= a2) i++;
        else j++;
    }
    return -1;
}
```

## Approach 3

Time complexity : O(log(min(M, N)))  
Space complexity : O(1)

```cpp
int kthElement(int arr1[], int arr2[], int n, int m, int k) {
    if(m > n) return kthElement(arr2, arr1, m, n, k);
    int l = max(0, k-m), r = min(k, n);
    while(l <= r) {
        int cut1 = (l+r)/2;
        int cut2 = (k - cut1);

        int left1 = cut1 == 0 ? INT_MIN : arr1[cut1-1];
        int left2 = cut2 == 0 ? INT_MIN : arr2[cut2-1];
        int right1 = cut1 == n ? INT_MAX : arr1[cut1];
        int right2 = cut2 == m ? INT_MAX : arr2[cut2];

        if(left1 <= right2 && left2 <= right1)
            return max(left1, left2);
        else if(left1 > right2)
            r = cut1-1;
        else
            l = cut1+1;
    }
    return -1;
}
```
