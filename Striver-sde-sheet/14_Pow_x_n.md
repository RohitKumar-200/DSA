# Pow(x, n)

## Problem statement

Implement `pow(x, n)`, which calculates `x` raised to the power `n` (i.e., x<sup>n</sup>).

## Approach 1 (Brute force)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
double myPow(double x, int n) {
    double ans = 1.0;
    long long nn = n;
    if(nn<0) nn = -1*nn;
    while(nn) {
        ans *= x;
        nn--;
    }
    if(n<0) ans = 1.0/ans;
    return ans;
}
```

## Approach 2 (Binary exponentiation)

Time complexity : O(long(N))  
Space complexity : O(1)

```cpp
double myPow(double x, int n) {
    double ans = 1.0;
    long long nn = n;
    if(nn<0) nn = -1*nn;
    while(nn) {
        if(nn&1) {
            ans = ans*x;
            nn--;
        } else {
            x = x * x;
            nn /= 2;
        }
    }
    if(n<0) ans = 1.0/ans;
    return ans;
}
```
