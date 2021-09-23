# Inversion of array

## Problem statement

Given an array of integers. Find the Inversion Count in the array. 

**Inversion Count**: For an array, inversion count indicates how far (or close) the array is from being sorted. If array is already sorted then the inversion count is 0. If an array is sorted in the reverse order then the inversion count is the maximum.
> Formally, two elements a[i] and a[j] form an inversion if a[i] > a[j] and i < j.

## Approach 1 (Brute force)

Time complexity : O(N^2)  
Space complexity : O(1)

```cpp
long long int inversionCount(long long arr[], long long N) {
    long long i, j, c=0;
    for(i=0; i<N; i++)
        for(j=i+1; j<N; j++)
            if(arr[i]>arr[j])
                c++;
    return c;
}
```

## Approach 2 (Merge sort)

Time complexity : O(N*long(N))  
Space complexity : O(N)

```cpp
long long mergeCount(long long arr[], long long temp[], long long start, long long end) {
    if(start == end) return 0;
    long long c, i, j, k, mid=start+(end-start)/2;
    c = mergeCount(arr, temp, start, mid) + mergeCount(arr, temp, mid+1, end);
    for(i=start, j=mid+1, k=0; i<=mid && j<=end; k++) {
        if(arr[i]<=arr[j]) temp[k]=arr[i++];
        else {
            c+=(mid-i+1);
            temp[k]=arr[j++];
        }
    }
    while(i<=mid) temp[k++] = arr[i++];
    while(j<=end) temp[k++] = arr[j++];
    for(i=start, k=0; i<=end; i++, k++) arr[i]=temp[k];
    return c;
}
long long int inversionCount(long long arr[], long long N) {
    long long temp[N], start=0, end=N-1;
    return mergeCount(arr, temp, start, end);
}
```
