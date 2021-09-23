#  Best Time to Buy and Sell Stock

## Problem statement

You are given an array prices where `prices[i]` is the price of a given stock on the i<sup>th</sup> day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return `0`.

## Approach 1 (Brute force)

Time complexity : O(N^2)  
Space complexity : O(1)

```cpp
int maxProfit(vector<int>& prices) {
    int res=0, n=prices.size();
    for(int i=0; i<n; i++) {
        for(int j=i+1; j<n; j++) {
            res = max(res, prices[j]-prices[i]);
        }
    }
    return res;
}
```

## Approach 2 (Optimal)

Time complexity : O(N)  
Space complexity : O(1)

```cpp
int maxProfit(vector<int>& prices) {
    int res=0, n=prices.size(), mn=prices[0];
    for(int i=1; i<n; i++) {
        res = max(res, prices[i]-mn);
        mn = min(mn, prices[i]);
    }
    return res;
}
```
