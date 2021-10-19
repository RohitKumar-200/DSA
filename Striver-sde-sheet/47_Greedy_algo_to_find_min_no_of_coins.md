# Greedy algorithm to find minimum number of coins

## Problem statement

Given a value `V` and array `coins[]` of size M, the task is to make the change for `V` cents, given that you have an infinite supply of each of `coins{coins1, coins2, ..., coinsm}` valued coins. Find the minimum number of coins to make the change. If not possible to make change then return -1.

> The problem linked to this question requires dynamic programming.
> Consider this test case for greedy : 1, 2, 5, 10, 20, 50, 100, 500, 1000

## Solution

Time complexity : O(V)  
Space complexity : O(1)

```cpp
int minCoins(int coins[], int M, int V) {
    int res = 0;
    for(int i=M-1; i>=0; i--) {
        while(coins[i] <= V) {
            V -= coins[i];
            res++;
        }
    }
    return res;
}
```

---

> Follow up (Recursion and DP)

---

## Approach 1 (Recursion)

Time complexity : O(V^M)  
Space complexity : O(1)

```cpp
int findMinCoins(int coins[], int M, int V) {
    if(V==0) return 0;
    if(M==0) return INT_MAX-1;
    if(coins[M-1] <= V)
        return min(1+findMinCoins(coins, M, V-coins[M-1]), findMinCoins(coins, M-1, V));
    return findMinCoins(coins, M-1, V);
}
int minCoins(int coins[], int M, int V) {
    int res = findMinCoins(coins, M, V);
    return res == INT_MAX-1 ? -1 : res;
}
```

## Approach 2 (Recursive DP)

Time complexity : O(M\*V)  
Space complexity : O(M\*V)

```cpp
int findMinCoins(int coins[], int M, int V, vector<vector<int>> &dp) {
    if(V==0) return 0;
    if(M==0) return INT_MAX-1;
    if(dp[M][V] != -1) return dp[M][V];
    if(coins[M-1] <= V)
        dp[M][V] = min(1+findMinCoins(coins, M, V-coins[M-1], dp), findMinCoins(coins, M-1, V, dp));
    else
        dp[M][V] = findMinCoins(coins, M-1, V, dp);
    return dp[M][V];
}
int minCoins(int coins[], int M, int V) {
    vector<vector<int>> dp(M+1, vector<int>(V+1, -1));
    int res = findMinCoins(coins, M, V, dp);
    return res == INT_MAX-1 ? -1 : res;
}
```

## Approach 3 (Iterative DP)

Time complexity : O(M*V)  
Space complexity : O(M*V)

```cpp
int minCoins(int coins[], int M, int V) {
    int dp[M+1][V+1];
    for(int i=0; i<=M; i++) {
        for(int j=0; j<=V; j++) {
            if(j==0) dp[i][j] = 0;
            else if(i==0) dp[i][j] = INT_MAX-1;
            else if(coins[i-1] <= j)
                dp[i][j] = min(1+dp[i][j-coins[i-1]], dp[i-1][j]);
            else
                dp[i][j] = dp[i-1][j];
        }
    }
    return (dp[M][V] == INT_MAX-1 ? -1 : dp[M][V]);
}
```
