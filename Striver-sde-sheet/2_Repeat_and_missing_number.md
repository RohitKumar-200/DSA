# Find the repeating and the missing number in an array

## Problem statement

Given an unsorted array of size n. Array elements are in the range from 1 to n. One number from set {1, 2, …n} is missing and one number occurs twice in the array. Find these two numbers.

## Approach 1 (Brute force)

Time complexity : O(N\*log(n))  
Space complexity : O(1)

```cpp
int *findTwoElement(int *arr, int n) {
    int missingNum=n, duplicateNum;
    sort(arr, arr+n);
    for(int i=0, j=1, f=1; i<n; i++, j++) {
        if(i > 0 && arr[i] == arr[i-1])
            duplicateNum = arr[i], j--;
        else if(f && arr[i] != j)
            missingNum = j, f = 0;
    }
    int *res = new int[2];
    res[0] = duplicateNum;
    res[1] = missingNum;
    return res;
}
```

## Approach 2 (Extra array)

Time complexity : O(N)  
Space complexity : O(N)

```cpp
int *findTwoElement(int *arr, int n) {
    bool f[n+1] = {0};
    long missingNum, duplicateNum;
    for(int i=0; i<n; i++) {
        if(!f[arr[i]]) f[arr[i]]=true;
        else duplicateNum = arr[i];
    }
    for(int i=1; i<=n; i++)
        if(!f[i])
            missingNum = i;
    int *res = new int[2];
    res[0] = duplicateNum;
    res[1] = missingNum;
    return res;
}
```

## Approach 3 (Mathematics)

Time complexity : O(N)  
Space complexity : O(1)  
it requires long int to store large values

```cpp
int *findTwoElement(int *arr, int n) {
    long sum = 0, sqSum=0;
    for(int i=0; i<n; i++) {
        sum += arr[i];
        sqSum += arr[i]*arr[i];
    }
    // x = duplicate num, y = missing num
    long xminusy = sum - (long(n)*(n+1))/2;
    long xsqminusysq = sqSum - (long(n)*(n+1)*(2*n+1))/6;
    long xplusy = xsqminusysq / xminusy;
    int x = (int)((xminusy + xplusy) / 2);
    int y = (int)(xplusy - x);
    int * res = new int[2];
    res [0] = x;
    res[1] = y;
    return res;
}
```

## Approach 4 (Xor)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
int *findTwoElement(int *arr, int n) {
    int num = 0, i;
    for(i=0; i<n; i++)
        num = (num^arr[i]);
    for(i=1; i<=n; i++)
        num = (num^i);

    int setbit = num & ~(num-1);

    int x = 0, y = 0;
    for(i=0; i<n; i++) {
        if(arr[i] & setbit)
            x = (x^arr[i]);
        else
            y = (y^arr[i]);
    }
    for(i=1; i<=n; i++){
        if(i&setbit)
            x = (x^i);
        else
            y =(y^i);
    }
    int * res = new int[2];
    res[0] = x;
    res[1] = y;
    for(i=0; i<n; i++) {
        if(arr[i] == res[1]) {
            swap(res[0], res[1]);
            break;
        }
    }
    return res;
}
```
