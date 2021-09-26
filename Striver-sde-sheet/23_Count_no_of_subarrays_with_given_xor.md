# Count the number of subarrays having a given XOR

## Problem statement

Given an array of integers `A` and an integer `B`.

Find the total number of subarrays having bitwise `XOR` of all elements equals to B.

## Approach 1 (Brute force, finding all subarrays)

Time complexity : O(N^3)  
Space complexity : O(1)

```cpp
int Solution::solve(vector<int> &A, int B) {
    int n=A.size(), cnt=0;
    for(int i=0; i<n; i++) {
        for(int j=i; j<n; j++) {
            int xorr = 0;
            for(int k=i; k<=j; k++)
                xorr = xorr^A[k];
            if(xorr == B)
                cnt++;
        }
    }
    return cnt;
}
```

## Approach 2 (Brute optimal)

Time complexity : O(N^2)  
Space complexity : O(1)

```cpp
int Solution::solve(vector<int> &A, int B) {
    int n=A.size(), cnt=0;
    for(int i=0; i<n; i++) {
        int xorr = 0;
        for(int j=i; j<n; j++) {
            xorr = xorr ^ A[j];
            if(xorr == B)
                cnt++;
        }
    }
    return cnt;
}
```

## Approach 3 (Hash map)

Time complexity : O(N\*log(N)) (or O(N) if used unordered map)  
Space complexity : O(N)

```cpp
int Solution::solve(vector<int> &A, int B) {
    map<int, int> mp;
    int xorr=0, cnt=0;
    for(auto it:A) {
        xorr = xorr^it;
        if(xorr == B) cnt++;
        if(mp.find(xorr^B) != mp.end()) {
            cnt += mp[xorr^B];
        }
        mp[xorr]++;
    }
    return cnt;
}
```
